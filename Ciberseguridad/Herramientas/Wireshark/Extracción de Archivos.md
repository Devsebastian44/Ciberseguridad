## Métodos de Extracción

### 1. Extracción Automática de Objetos HTTP

Wireshark puede extraer automáticamente archivos transferidos vía HTTP.

---

#### Pasos para Extraer

**Proceso:**

1. Abrir una captura con tráfico HTTP
2. Ir a **File → Export Objects → HTTP**
3. Revisar lista de objetos disponibles
4. Seleccionar los objetos a exportar
5. Hacer clic en **Save** (individual) o **Save All** (todos)

**Información visible:**

- **Packet number** - Número de paquete
- **Hostname** - Servidor de origen
- **Content Type** - Tipo MIME del archivo
- **Size** - Tamaño del archivo
- **Filename** - Nombre del archivo

---

#### Tipos de Archivos Extraíbles

**Imágenes:**

- JPG, PNG, GIF, BMP, ICO

**Documentos:**

- PDF, DOC, DOCX, XLS, XLSX, PPT

**Archivos de texto:**

- HTML, CSS, JS, XML, JSON

**Archivos multimedia:**

- MP3, MP4, AVI, FLV, WAV

**Ejecutables:**

- EXE, DLL, MSI

---

### 2. Extracción de Objetos de Otros Protocolos

#### **SMB/CIFS**

**Pasos:**

1. Ir a **File → Export Objects → SMB**
2. Seleccionar archivos transferidos
3. Guardar

---

#### **FTP**

**Pasos:**

1. Filtrar tráfico FTP-DATA: `ftp-data`
2. Seleccionar paquete del archivo
3. Clic derecho → **Follow → TCP Stream**
4. Cambiar a **Raw**
5. **Save As** con extensión correcta

---

#### **TFTP**

**Pasos:**

1. Ir a **File → Export Objects → TFTP**
2. Seleccionar archivo
3. Guardar

---

### 3. Extracción Manual usando Follow Stream

**Cuándo usar:**

- Protocolo no soportado por Export Objects
- Necesidad de ver contexto completo
- Transferencias por protocolos personalizados

**Pasos:**

1. Filtrar el tráfico deseado
2. Seleccionar un paquete del flujo
3. Clic derecho → **Follow → TCP Stream** (o UDP/HTTP)
4. Cambiar formato a **Raw** en menú desplegable
5. Click en **Save As**
6. Asignar nombre y extensión correcta

**Formatos de visualización:**

- **ASCII** - Texto legible
- **EBCDIC** - Codificación IBM
- **Hex Dump** - Hexadecimal
- **C Arrays** - Array de C
- **Raw** - Datos binarios sin procesar

---

## Extracción de Credenciales

### Protocolos No Seguros (Texto Plano)

**Filtros para detectar credenciales:**

```bash
# HTTP POST con password
http.request.method == "POST" and http contains "password"

# Autenticación FTP
ftp.request.command == "USER" or ftp.request.command == "PASS"

# Telnet (todo en texto plano)
telnet

# SMTP AUTH
smtp.req.command == "AUTH"

# POP3
pop.request.command == "USER" or pop.request.command == "PASS"

# IMAP
imap.request contains "LOGIN"
```

---

### Análisis de Formularios HTTP

**Pasos para encontrar credenciales:**

**1. Filtrar POST requests:**

```bash
http.request.method == "POST"
```

**2. Buscar campos comunes:**

```bash
# Username/email
http contains "username"
http contains "email"
http contains "user"

# Password
http contains "password"
http contains "passwd"
http contains "pass"

# Login forms
http contains "login"
```

**3. Examinar payload:**

- Panel inferior (Packet Details)
- Expandir **Line-based text data**
- Buscar parámetros `username=`, `password=`, etc.

---

### HTTP Basic Authentication

**Filtro:**

```bash
http.authorization
```

**Decodificar Base64:**

1. Localizar header `Authorization: Basic ...`
2. Copiar string Base64
3. Decodificar:

```bash
echo "dXNlcjpwYXNz" | base64 -d
# Resultado: user:pass
```

---

## Extracción de Archivos Específicos

### Filtros por Tipo de Contenido

#### **Imágenes**

```bash
# Cualquier imagen
http.content_type contains "image"

# Tipos específicos
http.content_type == "image/jpeg"
http.content_type == "image/png"
http.content_type == "image/gif"
http.content_type == "image/svg+xml"
```

---

#### **Documentos**

```bash
# PDF
http.content_type == "application/pdf"

# Microsoft Office (modernos)
http.content_type contains "application/vnd.openxmlformats"

# Word
http.content_type contains "application/msword"

# Excel
http.content_type contains "application/vnd.ms-excel"

# PowerPoint
http.content_type contains "application/vnd.ms-powerpoint"
```

---

#### **Archivos Multimedia**

```bash
# Audio
http.content_type contains "audio"
http.content_type == "audio/mpeg"
http.content_type == "audio/mp4"

# Video
http.content_type contains "video"
http.content_type == "video/mp4"
http.content_type == "video/x-msvideo"
```

---

#### **Archivos Comprimidos**

```bash
# ZIP
http.content_type == "application/zip"

# RAR
http.content_type == "application/x-rar-compressed"

# 7z
http.content_type == "application/x-7z-compressed"
```

---

#### **Ejecutables**

```bash
# Windows
http.content_type == "application/x-msdownload"
http.content_type == "application/octet-stream"

# Por extensión en URL
http.request.uri contains ".exe"
```

---

## Reconstrucción de Archivos

### Archivos Fragmentados

**Situación:** Archivo dividido en múltiples paquetes TCP

**Pasos:**

1. Identificar **primer paquete** del archivo
2. Usar **Follow TCP Stream**
3. Verificar que el stream esté **completo**
4. Guardar en formato **Raw**
5. Asignar extensión correcta

**Verificar completitud:**

- Revisar que no falten paquetes (gaps)
- Comprobar longitud esperada vs recibida

---

### Archivos en Múltiples Flujos

**Situación:** Archivo transferido en varias sesiones TCP

**Pasos:**

1. Identificar todos los flujos relacionados
2. Extraer cada segmento
3. Concatenar archivos manualmente:

```bash
cat parte1.bin parte2.bin parte3.bin > archivo_completo.bin
```

---

### Verificación de Integridad

**Métodos de verificación:**

**1. Comparar tamaños:**

- Tamaño esperado vs tamaño extraído
- Visible en Export Objects dialog

**2. Verificar checksums:**

```bash
# MD5
md5sum archivo_extraido
md5sum archivo_original

# SHA256
sha256sum archivo_extraido
```

**3. Comprobar headers:**

- **PDF:** Comienza con `%PDF`
- **JPEG:** Comienza con `FF D8 FF`
- **PNG:** Comienza con `89 50 4E 47`
- **ZIP:** Comienza con `50 4B 03 04`

**4. Intentar abrir:**

- Usar aplicación apropiada
- Verificar que se abre correctamente

---

## Análisis Forense de Archivos

### Malware y Archivos Sospechosos

**Precauciones:**

- **Nunca** ejecutar archivos sospechosos directamente
- Extraer en **máquina virtual** aislada
- Usar **sandbox** para análisis inicial

**Análisis:**

```bash
# Ver tipo de archivo
file archivo_extraido

# Calcular hash
sha256sum archivo_extraido

# Verificar en VirusTotal
# (subir hash, no el archivo si es sensible)

# Strings para análisis inicial
strings archivo_extraido | less
```

---

### Metadatos de Archivos

**Extraer metadatos:**

```bash
# Para imágenes
exiftool imagen.jpg

# Para PDFs
pdfinfo documento.pdf

# Para Office
exiftool documento.docx
```

---

## Herramientas Complementarias

### NetworkMiner

**Ventajas:**

- Extracción automática de archivos
- Interfaz más amigable
- Organización por hosts

**Uso:**

1. Abrir PCAP en NetworkMiner
2. Ir a pestaña **Files**
3. Ver archivos extraídos automáticamente

---

### Tcpflow

**Extracción desde línea de comandos:**

```bash
# Extraer todos los flujos
tcpflow -r captura.pcap

# Extraer a directorio específico
tcpflow -r captura.pcap -o output_dir/
```

---

### Binwalk

**Buscar archivos embebidos:**

```bash
# Analizar archivo extraído
binwalk archivo_extraido

# Extraer archivos encontrados
binwalk -e archivo_extraido
```

---

## Mejores Prácticas

### Durante la Extracción

**Organización:**

- Crear **carpeta dedicada** por captura
- Nombrar archivos **descriptivamente**
- Documentar **origen** de cada archivo

**Seguridad:**

- Trabajar en **entorno aislado**
- **No ejecutar** archivos sin análisis previo
- **Cifrar** carpetas con archivos sensibles

---

### Documentación

**Información a registrar:**

- **Timestamp** de transferencia
- **IP origen y destino**
- **Protocolo** utilizado
- **Hash** del archivo
- **Observaciones** sobre el archivo

---

## Limitaciones

**Protocolos cifrados:**

- **HTTPS** - No se pueden extraer archivos (cifrado TLS)
- **SFTP** - No se pueden extraer archivos
- **FTPS** - No se pueden extraer archivos

**Solución:** Necesario descifrar tráfico (requiere claves privadas)

**Archivos corruptos:**

- Pérdida de paquetes
- Captura incompleta
- Fragmentación IP no resuelta

---

## Consideraciones Legales

- **Solo** extraer archivos de capturas autorizadas
- **Respetar** privacidad y leyes locales
- **No distribuir** archivos extraídos sin autorización
- Mantener **cadena de custodia** en análisis forense
- **Documentar** todo el proceso de extracción

---