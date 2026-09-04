## Introducción

**Contexto Estratégico** OCI ha dejado de ser un actor secundario para convertirse en un disruptor de las "Cloud Wars". Según rankings recientes de satisfacción e integración (Cloud Wars), Oracle ha escalado a la tercera posición, desplazando a Amazon (AWS) al cuarto lugar. Su propuesta se apoya en una herencia empresarial inigualable (Java y bases de datos robustas) y una expansión agresiva en Latinoamérica (regiones en Chile, Colombia, Brasil y México). A diferencia de sus competidores, Oracle ofrece precios consistentes globalmente, eliminando la volatilidad de costes entre regiones.

**Infraestructura Global** La arquitectura física se despliega en una jerarquía de alta disponibilidad:

- **Regiones:** Ubicaciones geográficas que albergan centros de datos.
- **Availability Domains (AD):** Centros de datos aislados y tolerantes a fallos dentro de una región.
- **Fault Domains (FD):** Agrupaciones de hardware (racks) **dentro de un AD** con suministro eléctrico y refrigeración independientes. Actúan como una "antiregla" de afinidad: al distribuir instancias en diferentes FDs, se evitan puntos únicos de fallo físico durante mantenimientos o averías de rack.

**Conectividad Multicloud** La alianza estratégica "Oracle Interconnect for Azure" permite latencias mínimas entre nubes. Esto facilita arquitecturas donde la base de datos crítica corre en OCI y la capa de aplicaciones en Microsoft Azure, operando como un entorno unificado.

Comprender esta base física es el requisito previo para estructurar los recursos lógicos de la Tenancy.

## Conceptos clave

**Definiciones Técnicas**

- **Tenancy:** Contenedor raíz y cuenta principal que representa el entorno aislado del cliente.
- **VCN (Virtual Cloud Network):** Red definida por software, privada y personalizable.
- **Compute Instance:** Servidores divididos en **Virtual Machines** (sobre hipervisor compartido) y **Bare Metal** (servidor físico dedicado).
- **Storage Tiers:** Incluye **Object Storage** (binarios), **Block Volume** (discos de alto rendimiento), **File Storage** (sistema de archivos compartido vía **NFS**) y **Archive** (almacenamiento histórico de bajo coste).

**Análisis de Valor: Bare Metal vs. Virtual Machine**

- **Bare Metal:** Se elige para cargas de trabajo que exigen acceso directo al hardware, cumplimiento regulatorio estricto o cuando se requiere eliminar el fenómeno de **"Noisy Neighbors"** (vecinos ruidosos), garantizando que el rendimiento no se vea afectado por otros inquilinos.
- **Virtual Machine (VM):** Ideal para la mayoría de aplicaciones por su flexibilidad y rapidez de despliegue, utilizando un hipervisor para aislar múltiples instancias en un solo hierro.

Estos componentes se orquestan mediante una topología de red que define su visibilidad y seguridad.

## Funcionamiento

**Dinámica de Red** El flujo de tráfico se gestiona mediante Gateways específicos:

- **Internet Gateway:** Conexión bidireccional para servicios públicos.
- **NAT Gateway:** Salida segura a internet para recursos privados (parches y actualizaciones) sin permitir tráfico entrante iniciado desde el exterior.
- **Service Gateway:** Permite que los recursos se comuniquen con servicios de Oracle (como Object Storage) de forma privada, **sin salir a la red pública**, reduciendo latencia y eliminando costes de tráfico de salida (egress fees).

**Lógica Regional de Subredes** A diferencia de otros proveedores, en OCI las **subredes son regionales**. Una única subred abarca todos los ADs de una región, simplificando el diseño de alta disponibilidad y la gestión de tablas de enrutamiento.

**Orquestación de Cómputo** El despliegue requiere definir un **Shape** (configuración de OCPU y RAM) y una **Imagen**. OCI destaca por ofrecer **Oracle Linux** (basado en Red Hat pero gratuito) y el uso de **Boot Volumes** que permiten persistencia de datos incluso si la instancia se termina.

El despliegue técnico cobra sentido cuando se aplica a un escenario productivo real.

## Ejemplo práctico

**Escenario de Arquitectura Real** Despliegue de una aplicación web escalable:

- **Subred Pública:** Aloja el servidor web accesible mediante Internet Gateway.
- **Subred Privada:** Aloja el volumen de datos o base de datos, protegida del acceso externo directo.

**Configuración de Almacenamiento** Para extender la capacidad, se utiliza un **Block Volume**:

1. **Creación:** El volumen debe residir en el mismo AD que la instancia.
2. **Asociación (Attachment):** Se vincula de forma **Paravirtualizada** (método recomendado y sencillo).
3. **Montaje en el OS:** Se accede vía SSH y se ejecutan comandos estándar de Linux:
    - `lsblk` para identificar el nuevo dispositivo.
    - `sudo mkfs.ext4` para dar formato al disco.
    - `sudo mount` para asociarlo a un directorio del sistema.

Este despliegue solo es profesional si se rige por un marco de seguridad robusto.

## Seguridad

**Modelo de Responsabilidad e IAM** El **IAM (Identity and Access Management)** gestiona la autenticación (quién eres) y la autorización (qué puedes hacer).

**Jerarquía Lógica: Compartments** Los **Compartments** son carpetas lógicas para organizar recursos. No son barreras físicas ni de red, sino el ámbito donde se aplican las políticas. Facilitan la administración delegada y el aislamiento administrativo.

**Políticas (Policies)** Utilizan una sintaxis declarativa: `Allow group <group_name> to <verb> <resource-type> in compartment <compartment_name>`.

- **Verbos de control:** **Inspect** (listar), **Read** (ver metadatos), **Use** (trabajar con recursos existentes) y **Manage** (privilegios totales).
- **Mínimo Privilegio:** Solo se otorga el acceso necesario. OCI aplica una **denegación por defecto** (Implicit Deny) si no hay una política explícita.

Incluso con políticas claras, la operativa diaria presenta retos que el arquitecto debe prever.

## Errores comunes

**Identificación de Fallos Críticos**

- **Aislamiento Erróneo:** Intentar aislar tráfico de red usando _Compartments_ (el aislamiento de red solo se logra con VCNs y subredes).
- **Filtros de Seguridad:** No abrir el **Puerto 22** en las _Security Lists_ o NSGs, bloqueando el acceso SSH.
- **Costes Inesperados en Free Tier:** Olvidar que las **IPs Públicas Reservadas** y los **NAT Gateways** pueden generar cargos si se mantienen activos y sin uso, incluso dentro del programa gratuito.

La prevención de estos errores se basa en la implementación de estándares de arquitectura.

## Buenas prácticas

**Recomendaciones del Arquitecto**

- **Presupuestos (Budgets):** Configurar una alerta de presupuesto a un nivel bajo (ej. **$5 USD**) para detectar consumos imprevistos de inmediato.
- **Etiquetado (Tagging):** Crucial para la gobernanza y la asignación de costes por proyecto o departamento.
- **Resiliencia en FD:** Distribuir siempre las instancias entre los tres **Fault Domains**, incluso si la región solo tiene un Availability Domain.

## Cheatsheet

|   |   |   |
|---|---|---|
|Componente|Función Técnica|Scope|
|**VCN**|Red privada virtual definida por software|Regional|
|**Internet Gateway**|Acceso público bidireccional|VCN|
|**NAT Gateway**|Salida privada a Internet (unidireccional)|VCN|
|**Service Gateway**|Acceso a servicios Oracle (no internet/sin egress fees)|VCN|
|**Object Storage**|Almacenamiento de datos (Standard vs Archive)|Regional|
|**Security List**|Reglas de firewall a nivel de subred|Regional|
|**NSG**|Reglas de firewall a nivel de tarjeta de red (VNIC)|Instancia|

**Herramienta OCI CLI:** El modo interactivo se invoca con `oci -i`, permitiendo autocompletado y exploración de comandos para gestionar la infraestructura.

## Puntos de examen

- **VCN Regional:** A diferencia de otros proveedores, la VCN en OCI es siempre un recurso regional.
- **AD vs FD:** El AD es un centro de datos; el FD es una agrupación de racks dentro del AD.
- **Always Free:** Incluye 5TB de almacenamiento y las potentes instancias **ARM (Ampere)**.
- **Autonomous Database:** Se define por la tríada: **Self-driving, self-repairing, self-patching** (se autogestiona, autorepara y autoparchea).

## Preguntas tipo examen

**1. Un arquitecto necesita que sus instancias en una subred privada accedan a Object Storage sin que el tráfico pase por el internet público para evitar costes de salida. ¿Qué componente debe usar?**

- A) Internet Gateway.
- B) NAT Gateway.
- C) Service Gateway.
- D) Dynamic Routing Gateway.
- **Respuesta correcta: C.** El Service Gateway permite el acceso privado a servicios de Oracle dentro de la red de Oracle, optimizando costes y seguridad.

**2. ¿Cuál es el beneficio de utilizar Fault Domains al desplegar instancias de cómputo?**

- A) Proporcionan redundancia entre distintas regiones geográficas.
- B) Protegen contra fallos de hardware o mantenimiento de racks dentro de un AD.
- C) Aumentan automáticamente la velocidad de la red entre instancias.
- D) Son necesarios para crear subredes regionales.
- **Respuesta correcta: B.** Los FDs aíslan fallos físicos (electricidad/refrigeración) a nivel de rack dentro de un mismo centro de datos.

**3. ¿Qué característica describe mejor a la base de datos autónoma (Autonomous Database)?**

- A) Requiere que el usuario aplique parches de seguridad manualmente cada mes.
- B) Es una base de datos que solo puede correr en servidores locales (on-premise).
- C) Es "self-driving", encargándose automáticamente del ajuste de rendimiento y parcheo.
- D) No permite el escalado de recursos de CPU.
- **Respuesta correcta: C.** La autonomía de la base de datos de Oracle se basa en su capacidad de autogestión, reparación y parcheo sin intervención manual.