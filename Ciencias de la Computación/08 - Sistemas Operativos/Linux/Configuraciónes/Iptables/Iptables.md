**IPTables** es una herramienta de línea de comandos en Linux utilizada para configurar reglas de **filtrado de paquetes** en el **firewall del kernel (Netfilter)**. Permite controlar el tráfico de red entrante, saliente y reenviado según ciertas reglas definidas por el usuario.

Antes de realizar cualquier cambio, es crucial hacer una copia de seguridad de las reglas de iptables existentes para evitar bloquearse accidentalmente del sistema

```bash 
sudo iptables-save > /ruta/del/archivo/backup_iptables.rules 
sudo iptables-restore < /ruta/del/archivo/backup_iptables.rules
```

## Guardar reglas

Una vez que esté satisfecho con las reglas de iptables, guárdelas

```bash 
iptables-save > /etc/iptables/rules.v4
```

## Eliminar reglas

```bash
iptables -D INPUT SEGUIDO DE LA REGLA
```

## Filtrado de tráfico

Permitir tráfico específico:

```bash 
iptables -A CHAIN -s IP_ORIGEN -d IP_DESTINO -p PROTOCOL --dport PUERTO -j ACCEPT
```

Bloquear tráfico específico:

```bash 
iptables -A CHAIN -s IP_ORIGEN -d IP_DESTINO -p PROTOCOL --dport PUERTO -j DROP
```

## Administración de Cadenas

Crear cadena personalizada:

```
iptables -N CUSTOM_CHAIN
```

Eliminar cadena personalizada

```
Iptables -X CUSTOM_CHAIN
```

Política predeterminada de una cadena:

```
Iptables -P CHAIN ACTION
```

## NAT (Network Address Translation)

Redirección de puertos:

```bash 
iptables -t nat -A PREROUTING -i INTERFACE -p PROTOCOL --dport PUERTO_ORIGEN -j DNAT --to-destination IP_DESTINO:PUERTO_DESTINO
```

Mascarado (SNAT):

```bash 
iptables -t nat -A POSTROUTING -o INTERFACE -s IP_ORIGEN -J SNAT --to-source TU_IP_PUBLICA
```

## Protección contra ataques

### SYN Flood

```bash 
iptables -A INPUT -p tcp --syn -m limit --limit 5/s -j ACCEPT
iptables -A INPUT -p tcp --syn -j DROP
```

Evitar escaneo de puertos:

```bash 
iptables -N SCANNER_PROTECTION
iptables -A SCANNER_PROTECTION -p tcp --tcp-flags ALL NONE -j DROP
iptables -A SCANNER_PROTECTION -p tcp --tcp-flags SYN,FIN -j DROP
```

## Log y Registros

Registrar paquetes denegados:

```bash
Iptables -A CHAIN -s IP DE ORIGEN -d IP DE DESTINO -p PROTOCOL --dport PUERTO -j LOG --log-prefix "DENIED: "
```

Establecer nivel de registro:

```bash
sudo iptables -A INPUT -j LOG --log-level4
```

## Bloquear paquetes no válidos

Evite que los paquetes inválidos lleguen a su sistema usando la siguiente regla:

```bash
iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
```

## Tráfico Establecido y Relacionado

Permita que continúen las conexiones establecidas y el tráfico relacionado:

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

## Permitir tráfico de bucle invertido

Habilite el tráfico de loopback, que es esencial para los servicios locales:

```bash
iptables -A INPUT -i lo -j ACCEPT
```

## Limite el acceso SSH

Si tiene un servidor SSH, limite el acceso a él desde direcciones IP o redes específicas:

```bash
iptables -A INPUT -p tcp --dport 22 -s IP DE CONFIANZA O RED -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```

## Prevenir ataques DoS

Cierre los puertos innecesarios para reducir la superficie de ataque

```bash
iptables -A INPUT -p tcp --syn --dport 80 -m connlimit --connlimit-above 20 -j DROP
```

## Bloquear puertos específicos:

Cierre los puertos innecesarios para reducir la superficie de ataque

```bash
iptables -A INPUT -p tcp --dport PUERTO -j DROP
```

## Conexiones de límite de velocidad

Limite la velocidad a la que se pueden establecer nuevas conexiones

```bash
iptables -A INPUT -p tcp --syn --dport PORT_NUMBER -m connlimit --connlimit-above 10 --connlimit-mask 32 -j DROP
```

## Registrar tráfico sospechoso

Registre ciertos tipos de paquetes para su revisión

```bash
iptables -A INPUT -p tcp --dport 80 -m limit -- 5/m --limit-burst 10 -j LOG --log-prefix "HTTP Traffic: "

iptables -A INPUT -p tcp --dport 80 -j DROP
```

## Habilite ICMP (Ping) de fuentes confiables

Si desea permitir solicitudes de ping (ICMP Echo) desde direcciones IP específicas

```bash
iptables -A INPUT -p tcp --dport 80 -m limit -- 5/m --limit-burst 10 -j LOG --log-prefix "HTTP Traffic: "

iptables -A INPUT -p tcp --dport 80 -j DROP
```

## Política predeterminada

Establezca la política predeterminada para el tráfico entrante y saliente en DROP. Esto garantizará que solo se acepte el tráfico permitido explícitamente y todo lo demás se descartará


```bash
iptables -P INPUT DROP

iptables -P FORWARD DROP

iptables -P OUTPUT DROP
```

## Interfaz de bucle invertido

Permita el tráfico en la interfaz de loopback. Esto es necesario para que los procesos locales se comuniquen entre sí

```bash
iptables -A INPUT -i lo -j ACCEPT

iptables -A OUTPUT -o lo -j ACCEPT
```

## Tráfico Establecido y Relacionado

Permita el tráfico entrante y saliente relacionado con las conexiones establecidas. Esto permite responder al tráfico saliente y evita interrumpir las conexiones existentes

```bash
iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT

iptables -A OUTPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
```

## Permitiendo Servicios Específicos

Ahora, permita el tráfico de servicios específicos a los que desee acceder desde Internet. Por ejemplo, para permitir el tráfico SSH, HTTP y HTTPS

```bash
# Allow SSH (reemplace <your_ssh_port> con su puerto SSH real)

iptables -A INPUT -p tcp --dport <your_ssh_port> -j ACCEPT

# Allow HTTP y HTTPS

iptables -A INPUT -p tcp --dport 80 -j ACCEPT

iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

## Protección contra ataques de denegación de servicio (DoS)

Para protegerse contra los ataques DoS, puede configurar reglas de limitación de velocidad para el tráfico entrante en ciertos puertos. Por ejemplo, para limitar la cantidad de conexiones entrantes al puerto 80 a 20 por minuto

```bash
iptables -A INPUT -p tcp --dport 80 -m limit -- 50/minute --limit-burst 30 -j ACCEPT
```

## Bloquear direcciones IP sospechosas

Si observa tráfico malicioso de direcciones IP específicas o rangos de IP, puede bloquearlos usando el destino DROP

```bash
# Reemplace X.X.X.X con la dirección IP maliciosa real

iptables -A INPUT -s X.X.X.X -j DROP
```

## Inicio sesión

Es una buena idea registrar los paquetes descartados, lo que puede ayudarlo a monitorear e investigar posibles amenazas

```bash
iptables -A INPUT -j LOG --log-prefix "IPTables-Dropped: " --log-level 7
```
