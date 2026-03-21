## Introducción

**Tor (The Onion Router)** es una red de comunicaciones anónimas que permite a los usuarios navegar por internet de forma privada y acceder a servicios ocultos.

---

## Historia de Tor

### Origen y Evolución

**Línea temporal:**

- **Años 90:** desarrollado por la Marina de EE.UU.
- **Propósito inicial:** proteger comunicaciones militares
- **2006:** proyecto de código abierto
- **Financiamiento:** organizaciones de derechos humanos, fundaciones
- **Actualidad:** red global con miles de nodos voluntarios

---

## Arquitectura de Tor

### Principio de Funcionamiento

**Flujo de conexión:**

```
Usuario → Nodo de Entrada → Nodo Intermedio → Nodo de Salida → Destino
```

**Características:**

- **Enrutamiento** en capas (onion routing)
- **Mínimo 3 nodos** en cada circuito
- Cambio de circuito cada **10 minutos**
- Ningún nodo conoce la **ruta completa**

---

### Capas de Cifrado

**Sistema de cifrado múltiple:**

1. **Capa 1:** cifrado del usuario al nodo de entrada
2. **Capa 2:** cifrado del nodo de entrada al intermedio
3. **Capa 3:** cifrado del nodo intermedio al de salida

**Analogía:** como capas de una cebolla, cada nodo **descifra** una capa

---

### Tipos de Nodos

**Nodo de Entrada (Guard):**

- **Primer punto** de conexión a Tor
- Conoce tu **IP real** pero no el destino
- Seleccionado y mantenido por **3 meses**
- **Crítico** para seguridad

---

**Nodo Intermedio (Middle):**

- **Enruta** el tráfico cifrado
- **No conoce** origen ni destino
- Máximo **anonimato** en la cadena
- Mayor número de nodos en la red

---

**Nodo de Salida (Exit):**

- **Último punto** antes del destino
- Puede ver tráfico **no cifrado** (HTTP)
- Conoce el **destino** pero no el origen
- Mayor **riesgo** de compromiso

---

## Servicios Ocultos (.onion)

### Características

**Propiedades principales:**

- Dominio termina en **`.onion`**
- Acceso **solo a través de Tor**
- **Anonimato bidireccional:** servidor y usuario
- Cifrado **extremo a extremo**
- No requieren **DNS** tradicional
- Dirección derivada de **clave pública**

---

### Versiones de Direcciones

**V2 (obsoletas):**

- Longitud: **16 caracteres**
- Ejemplo: `3g2upl4pq6kufc4m.onion`
- **Deprecadas** desde 2021

**V3 (actuales):**

- Longitud: **56 caracteres**
- Ejemplo: `thehiddenwiki...abcdef123456.onion`
- Mayor **seguridad** criptográfica
- Resistente a **colisiones**

---

### Ejemplos Legítimos

**Servicios conocidos:**

- **Facebook:** `facebookcorewwwi.onion`
- **ProPublica:** `p53lf57qovyuvwsc6xnrppddxpr23otqjafxdnt8i.onion`
- **DuckDuckGo:** `3g2upl4pq6kufc4m.onion`
- **The New York Times:** `nytimes...onion`
- **BBC News:** `bbcnewsv2vjtpsuy.onion`

---

## Tor Browser

### Características Principales

**Especificaciones:**

- Basado en **Firefox ESR** (Extended Support Release)
- Configuración **preestablecida** para privacidad
- **Actualizaciones automáticas** de seguridad
- Extensiones **limitadas** para prevenir fingerprinting
- **NoScript** integrado
- **HTTPS Everywhere** incluido

---

### Niveles de Seguridad

**Estándar:**

- JavaScript **habilitado**
- Navegación normal con protección básica
- Mejor **compatibilidad** con sitios web
- **Menor seguridad**

---

**Safer (Más Seguro):**

- JavaScript **desactivado** en sitios no HTTPS
- Algunos elementos multimedia **deshabilitados**
- Balance entre seguridad y **usabilidad**

---

**Safest (Muy Seguro):**

- JavaScript **completamente desactivado**
- Imágenes y fuentes **restringidas**
- **Máxima seguridad**
- Algunos sitios pueden **no funcionar**

---

## Ventajas de Tor

### Anonimato y Privacidad

**Beneficios principales:**

- **Oculta** tu dirección IP real
- **Protege** contra análisis de tráfico
- **Evita** rastreo de navegación
- **Bypass** de censura y bloqueos
- **Acceso** a contenido geográficamente restringido

---

### Libertad de Información

**Aplicaciones importantes:**

- **Periodismo** de investigación
- **Activismo** en países represivos
- **Whistleblowing** seguro
- Comunicación **confidencial**
- Investigación **académica**

---

## Limitaciones de Tor

### Desventajas Técnicas

**Restricciones importantes:**

- **Velocidad reducida** por múltiples saltos
- **Incompatibilidad** con torrents
- **Latencia** elevada (300-1000ms)
- No protege contra **malware**
- Algunos sitios **bloquean** nodos de salida

---

### Limitaciones de Seguridad

**Vulnerabilidades conocidas:**

- **Nodos de salida** pueden monitorear tráfico no cifrado
- **Ataques de correlación** si se controlan múltiples nodos
- **JavaScript** puede revelar información
- No protege contra **compromiso del endpoint**
- Vulnerable a **ataques globales** de vigilancia

---

## Funcionamiento Técnico

### Establecimiento de Circuito

**Proceso paso a paso:**

1. Cliente descarga **directorio de consenso** de nodos
2. Selecciona **3 nodos** (guard, middle, exit)
3. Establece **conexión cifrada** con cada nodo
4. Crea **circuito** de 3 saltos
5. Envía datos a través del **circuito cifrado**

---

### Protocolo de Comunicación

**Características técnicas:**

- Protocolo: **TCP** sobre TLS
- Cifrado: **AES** y criptografía de curva elíptica
- Tamaño de celda: **512 bytes**
- Puerto por defecto: **9001** (relay), **9030** (directory)
- Puerto cliente: **9050** (SOCKS proxy)

---

## Configuración Avanzada

### Opciones de torrc

**Configuraciones útiles:**

```
# Usar puente (bridge) para bypass de bloqueos
UseBridges 1
Bridge obfs4 [dirección:puerto] [fingerprint]

# Selección de país de salida
ExitNodes {us},{ca},{de}
StrictNodes 1

# Excluir países específicos
ExcludeExitNodes {cn},{ru},{ir}
```

---

### Bridges (Puentes)

**Características:**

- **Ocultan** el uso de Tor a ISP
- No listados en el **directorio público**
- Útiles en países con **censura**
- Tipos: **obfs4, meek, snowflake**

---

## Mejores Prácticas

**Recomendaciones esenciales:**

- Usar nivel de seguridad **Safer o Safest**
- **Nunca** descargar torrents a través de Tor
- No **maximizar** la ventana del navegador
- Usar **HTTPS** siempre que sea posible
- No instalar **extensiones** adicionales
- **Verificar** circuito regularmente
- Cambiar **identidad** después de actividades sensibles
- No revelar **información personal**
- Mantener el navegador **actualizado**
- Usar con **VPN** para mayor anonimato (opcional)

---