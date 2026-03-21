## Requisitos Previos

### Hardware Mínimo

- **RAM** - 2GB mínimo (recomendado **4GB**)
- **USB** - 8GB mínimo (recomendado **16GB**)
- **Procesador** - x86_64 de **64 bits**
- **BIOS/UEFI** - Compatible con arranque USB

### Materiales Necesarios

- USB confiable de **marca reconocida**
- Conexión a internet estable
- Otro sistema operativo para crear el USB booteable

---

## Descarga y Verificación

### Paso 1: Descargar Tails

- Visitar `https://tails.boum.org/install/`
- Seleccionar **versión más reciente**
- Descargar archivo **ISO** y archivo de **firma digital**

---

### Paso 2: Verificar Integridad

Confirmar que el archivo descargado no está corrupto o alterado.

- Usar herramientas gráficas o **PowerShell** en Windows
- Confirmar que el **hash SHA256** coincide con el oficial

---

### Paso 3: Verificar Autenticidad

Confirmar que el archivo proviene de los desarrolladores oficiales de Tails.

- Usar **claves públicas oficiales** de Tails
- Confirmar **firma digital** de la ISO

---

## Creación del USB Booteable

### Opción 1: Tails Installer (Recomendado)

Herramienta oficial diseñada específicamente para Tails.

- Descargar **Tails Installer** para Windows
- Seleccionar archivo ISO
- Seleccionar USB destino
- Iniciar proceso de instalación

---

### Opción 2: Balena Etcher

Herramienta multiplataforma fácil de usar.

- Descargar desde `https://www.balena.io/etcher/`
- Seleccionar archivo **ISO**
- Seleccionar **USB destino**
- Clic en **"Flash"**

---

### Opción 3: Rufus

Útil para BIOS antiguos y configuraciones específicas.

- Descargar Rufus
- Configurar **modo de partición** apropiado
- Seleccionar ISO y USB
- Configurar opciones de arranque específicas

---

## Configuración del BIOS/UEFI

### Acceso al BIOS/UEFI

#### Método 1: Al Iniciar

- Reiniciar y presionar **F2, F12, DEL o ESC** (varía según fabricante)

#### Método 2: Desde Windows

- **Configuración → Recuperación → Reinicio avanzado → Firmware UEFI**

---

### Configuraciones Necesarias

#### **Boot Order (Orden de Arranque)**

- Colocar **USB primero** en la lista

#### **Secure Boot**

- **Deshabilitar** si es necesario para compatibilidad

#### **Legacy Boot**

- **Habilitar** en equipos antiguos

#### **Fast Boot**

- **Deshabilitar** para asegurar arranque desde USB

---

### Guardar Cambios

- Seleccionar **"Save and Exit"** o presionar **F10**
- Confirmar cambios

---

## Primer Arranque

### Proceso de Arranque

1. **Insertar USB** en el puerto
2. **Reiniciar** el equipo
3. **Seleccionar arranque** desde USB (si no arranca automáticamente)
4. **Esperar carga** del sistema Tails

---

### Pantalla de Bienvenida (Tails Greeter)

#### Configuraciones Básicas

- **Idioma** - Seleccionar idioma del sistema
- **Teclado** - Configurar distribución del teclado
- **Formatos** - Fecha, hora, números

#### Configuraciones Opcionales

- **Contraseña admin** - Para instalación de software adicional
- **MAC address spoofing** - Ocultar dirección MAC real
- **Configuración de red** - Proxy, bridge
- **Unsafe Browser** - Para portales cautivos

---

### Inicio del Sistema

- Clic en **"Start Tails"**
- Esperar carga del escritorio

---

## Configuración Inicial

### Verificar Conexión Tor

#### Proceso de Verificación

1. **Tor Browser** abre automáticamente
2. Visitar `https://check.torproject.org/`
3. Confirmar mensaje de **éxito** y nueva **IP anónima**

---

### Configurar Persistencia (Opcional)

La **persistencia** permite guardar datos entre sesiones de Tails.

#### Crear Volumen Persistente

- Acceder desde **menú de aplicaciones**
- Crear contraseña fuerte
- Seleccionar datos a guardar:
    - **Documentos personales**
    - **Marcadores del navegador**
    - **Configuración WiFi**
    - **Software adicional**

---

### Configurar Aplicaciones Principales

#### **Thunderbird**

- Cliente de correo electrónico seguro
- Configurar con cuentas anónimas

#### **KeePassXC**

- Gestor de contraseñas cifrado
- Almacenamiento seguro de credenciales

#### **OnionShare**

- Compartir archivos anónimamente
- Crear servicios onion temporales

---

## Uso Seguro de Tails

### Mejores Prácticas

- **Evitar usuario administrador** - Usar solo cuando sea necesario
- **Verificar conexión Tor regularmente** - Confirmar anonimato
- **Mantener actualizado** - Descargar nuevas versiones
- **Usar solo aplicaciones incluidas** - Software pre-verificado
- **Trabajar offline** para documentos sensibles

---

### Gestión de Archivos

#### **Archivos Temporales**

- Carpeta **amnesia** - Se borran automáticamente al reiniciar
- Uso para datos sensibles sin persistencia

#### **Archivos Persistentes**

- Carpeta **Persistent** - Guardados entre sesiones
- Solo si está configurada la persistencia

---

### Compartir Archivos

- Usar **OnionShare** para crear enlaces `.onion` temporales
- Compartir de forma anónima sin servidores terceros

---

## Troubleshooting Común

### Problemas de Arranque

#### Soluciones

- Verificar **conexión física** del USB
- Probar **puertos USB 2.0** (más compatibles)
- **Deshabilitar Secure Boot** en BIOS
- **Actualizar BIOS/UEFI** a última versión
- **Re-formatear USB** y reinstalar Tails

---

### Problemas de Red

#### Soluciones

- Verificar **conexión física** (cable ethernet)
- Usar **Unsafe Browser** en portales cautivos
- Configurar **proxy manual** si es necesario
- **Reiniciar servicio de red** desde terminal

---

### Problemas de Rendimiento

#### Soluciones

- **Aumentar RAM** si se usa en máquina virtual
- Usar **USB 3.0 rápido** de calidad
- **Cerrar aplicaciones innecesarias**
- **Reiniciar regularmente** para liberar memoria

---

### Problemas de Compatibilidad

#### Soluciones

- Revisar **lista oficial de hardware** compatible
- Usar **drivers genéricos** cuando sea posible
- **Reportar problemas** a la comunidad de Tails
- Usar **hardware estándar** y común

---