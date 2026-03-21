## Introducción a Hydra

**Hydra** es una herramienta de fuerza bruta que soporta múltiples protocolos de red, incluyendo SSH, FTP, HTTP y muchos otros.

---

### Usos Principales

- **Pentesting:** evaluación de la fortaleza de contraseñas
- **Auditorías de seguridad:** identificación de cuentas vulnerables
- **Pruebas de resistencia:** verificación de políticas de contraseñas

---

## Instalación

### Linux

```bash
# Ubuntu/Debian
sudo apt-get install hydra

# CentOS/RHEL
sudo yum install hydra

# Arch Linux
sudo pacman -S hydra
```

---

### Verificación

```bash
hydra -h
```

---

## Sintaxis General

```bash
hydra [opciones] servidor protocolo
```

---

## Ataques SSH Básicos

### Usuario Específico + Lista de Contraseñas

```bash
hydra -l admin -P passwords.txt ssh://192.168.1.100
```

**Con threads limitados:**

```bash
hydra -l admin -P passwords.txt -t 4 ssh://192.168.1.100
```

---

### Lista de Usuarios + Lista de Contraseñas

```bash
hydra -L users.txt -P passwords.txt ssh://192.168.1.100
```

---

### Usuario y Contraseña Específicos

```bash
hydra -l root -p toor ssh://192.168.1.100
```

---

## Técnicas Avanzadas

### Configuración de Parámetros

```bash
hydra -l admin -P passwords.txt -t 4 -w 30 -f ssh://192.168.1.100
```

**Opciones:**

- `-t 4` = 4 threads paralelos
- `-w 30` = timeout de 30 segundos
- `-f` = parar después del primer login exitoso

---

### Ataques con Patrones Generados

**Con Crunch:**

```bash
crunch 6 8 -t admin@@@ | hydra -l admin -P - ssh://192.168.1.100
```

**Números generados:**

```bash
hydra -l admin -P <(crunch 4 6 0123456789) ssh://192.168.1.100
```

---

## Evasión y Optimización

### Evasión de Detección

**Reducir velocidad:**

```bash
hydra -l admin -P passwords.txt -t 1 -w 60 ssh://192.168.1.100
```

**Opciones adicionales:**

```bash
hydra -l admin -P passwords.txt -s 22 -e nsr ssh://192.168.1.100
```

**Flags `-e`:**

- `n` = null password
- `s` = login como password
- `r` = reversed login

---

### Optimización de Rendimiento

**Aumentar threads:**

```bash
hydra -l admin -P passwords.txt -t 16 ssh://192.168.1.100
```

**Múltiples objetivos:**

```bash
hydra -l admin -P passwords.txt -M targets.txt ssh
```

---

## Contramedidas y Defensa

### Configuración SSH Segura

**Editar `/etc/ssh/sshd_config`:**

```bash
MaxAuthTries 3
LoginGraceTime 60
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

**Reiniciar servicio:**

```bash
sudo systemctl restart sshd
```

---

### Fail2Ban

**Configurar `/etc/fail2ban/jail.local`:**

```bash
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
```

**Iniciar servicio:**

```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

## Mejores Prácticas

### Ataque Responsable

- Usar **-t 4** o menos para no saturar el servicio
- Implementar **delays** con `-w` para evasión
- Usar **-f** para detenerse al encontrar credenciales
- **Guardar resultados** con `-o archivo.txt`

---

### Defensa Efectiva

- **Deshabilitar** autenticación por contraseña
- Usar **autenticación de clave pública**
- Implementar **Fail2Ban** o similar
- **Monitorear** `/var/log/auth.log`
- Cambiar **puerto SSH** por defecto (opcional)

---

## Consideraciones

- **Solo** usar en auditorías autorizadas
- **Documentar** permisos obtenidos
- Respetar **rate limits** del sistema
- **No** realizar ataques en producción sin autorización

---