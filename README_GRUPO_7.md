# README_GRUPO_7.md

## 📘 Resumen del Repositorio

El repositorio [Articulos](https://github.com/bl4ck44/Articulos) reúne una lista de herramientas relacionadas con pruebas de penetración (pentesting) y evaluación de vulnerabilidades. Su utilidad principal es servir como una guía rápida o repositorio de consulta para profesionales y estudiantes interesados en la ciberseguridad ofensiva. 

Aunque no contiene descripciones profundas de cada vulnerabilidad, su valor está en la recopilación de herramientas específicas asociadas a distintos tipos de ataques y vulnerabilidades, como XSS, SQL Injection, LFI, RFI, entre otros. Funciona como un índice práctico para comenzar una investigación o una prueba controlada.

---

## ✅ Justificación Técnica

Nuestro grupo escogió este repositorio por varias razones técnicas:

1. **Relevancia en Ciberseguridad Actual**  
   La identificación y explotación de vulnerabilidades es una de las competencias más buscadas en el campo de la ciberseguridad. Repositorios como este proporcionan una base útil para conocer qué herramientas son comúnmente utilizadas por analistas de seguridad. Según el *OWASP Top 10* (2023), las vulnerabilidades como XSS, Inyección y fallos de configuración de seguridad siguen estando entre las más críticas [[OWASP](https://owasp.org/Top10/)].

2. **Curación de Herramientas Populares**  
   El repositorio menciona herramientas ampliamente reconocidas en el ámbito de la seguridad, como SQLMap, XSStrike, Nikto o Burp Suite. Estas herramientas son comúnmente utilizadas tanto en entornos académicos como profesionales, como se puede observar en libros como *The Web Application Hacker's Handbook* (Stuttard & Pinto, 2011).

3. **Facilidad de Acceso y Organización Temática**  
   Aunque el repositorio no describe detalladamente las vulnerabilidades, sí permite identificar rápidamente qué herramientas podrían usarse frente a determinadas amenazas. Esto lo hace útil como punto de partida para estudiantes y nuevos analistas que quieren investigar más a fondo.

4. **Complementariedad con Recursos Teóricos**  
   El hecho de que este repositorio sea una lista de herramientas sin descripción profunda lo convierte en un excelente complemento de estudios formales. Por ejemplo, al estudiar una vulnerabilidad como "Remote Code Execution", se puede recurrir a este repositorio para encontrar con qué herramientas se podría experimentar en laboratorios controlados.

5. **Motivación del Grupo**  
   Nos pareció interesante poder complementar este repositorio con conceptos clave de cada vulnerabilidad, ya que muchos solo están mencionados por nombre. Esto nos permite aportar contenido educativo adicional, y profundizar nuestro entendimiento de las técnicas y mecanismos involucrados.

---

## 📚 Referencias

- OWASP Top 10 – https://owasp.org/Top10/
- Stuttard, D., & Pinto, M. (2011). *The Web Application Hacker’s Handbook*.
- HackTricks – https://book.hacktricks.xyz/
- Kali Linux Tools – https://tools.kali.org/tools-listing
- Foros especializados: Reddit r/netsec, StackOverflow, Medium (secciones de ciberseguridad).

---

Grupo 7  
Maestría en Ciberseguridad  
2025

---
### APORTE ALEJANDRO MAYA

# 🛡️ Análisis de Vulnerabilidades y Técnicas de Seguridad - GRUPO 7

## 📌 Análisis de Malware:

El análisis de malware es el proceso de examinar software malicioso para entender su comportamiento, propósito y posibles efectos en un sistema o red. Este análisis puede ser:

- **Estático**: Evaluación del malware sin ejecutarlo (por ejemplo, análisis de binarios, cadenas y código).
- **Dinámico**: Observación del comportamiento del malware en tiempo de ejecución, normalmente en entornos aislados como sandboxes.

El análisis permite a los equipos de ciberseguridad identificar nuevas amenazas, generar firmas para antivirus y entender cómo prevenir futuros ataques.

### 🧰 Herramientas para análisis de malware

- **Estático**:
  - [Ghidra](https://ghidra-sre.org): Desensamblador y herramienta de ingeniería inversa.
  - [Radare2](https://rada.re/n/): Framework de análisis binario.
  - **Strings (Linux)**: Extrae texto legible desde archivos binarios.
  - [Binwalk](https://github.com/ReFirmLabs/binwalk): Análisis de firmware y extracción de datos embebidos.

- **Dinámico**:
  - [Cuckoo Sandbox](https://cuckoosandbox.org): Sandbox automatizado para análisis de comportamiento.
  - [ProcMon (Process Monitor)](https://learn.microsoft.com/en-us/sysinternals/downloads/procmon): Monitoreo de procesos en tiempo real.
  - [Wireshark](https://www.wireshark.org/): Análisis de tráfico de red.
  - [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon): Monitoreo de eventos detallados del sistema.

---

## 🔐 Criptografía y Esteganografía

### 🔒 Criptografía

La criptografía es la ciencia de proteger la información mediante técnicas matemáticas que la transforman en datos ilegibles sin una clave de acceso. Se utiliza para garantizar la **confidencialidad**, **integridad**, **autenticación** y **no repudio** de la información.

#### 🧰 Herramientas de criptografía

- **OpenSSL**: Herramienta de línea de comandos para operaciones criptográficas.
- **GPG (GNU Privacy Guard)**: Encriptación de archivos y correos con claves públicas y privadas.
- **Hashcat**: Recuperación de contraseñas mediante ataques de fuerza bruta y diccionario.

### 🕵️‍♂️ Esteganografía

La esteganografía es el arte de ocultar información dentro de otro archivo (como imágenes, audio o video), de forma que su existencia pase desapercibida. A diferencia de la criptografía, su objetivo es la **ocultación**, no la encriptación.

#### 🧰 Herramientas de esteganografía

- **Steghide**: Inserta y extrae datos ocultos en imágenes o archivos de audio.
- **zsteg**: Extrae datos ocultos de imágenes PNG y BMP.
- **ExifTool**: Inspección y manipulación de metadatos donde puede ocultarse información.

---

## Referencias:

- Sikorski, M., & Honig, A. (2012). *Practical Malware Analysis*. No Starch Press.
- Paar, C., & Pelzl, J. (2010). *Understanding Cryptography*. Springer.
- [OWASP Malware Analysis Project](https://owasp.org/www-project-malware-analysis/)
- [Malware Unicorn RE101 Workshop](https://www.malwareunicorn.org/workshops/re101.html)
- [Ghidra SRE](https://ghidra-sre.org/)
- [Cuckoo Sandbox Docs](https://cuckoosandbox.readthedocs.io/)
- [NSA Ghidra GitHub](https://github.com/NationalSecurityAgency/ghidra)
- [OpenSSL Documentation](https://www.openssl.org/docs/)
- [GNU Privacy Guard (GPG)](https://gnupg.org/)
- [Steghide GitHub](https://github.com/StefanoDeVuono/steghide)
- [ExifTool Documentation](https://exiftool.org/)

---
