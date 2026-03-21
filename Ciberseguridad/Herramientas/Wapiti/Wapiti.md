## Análisis con Wapiti

**Wapiti** es una herramienta de seguridad informática utilizada para evaluar vulnerabilidades en aplicaciones web.  
Su objetivo principal es detectar posibles agujeros de seguridad y vulnerabilidades en el código y la configuración.

Características principales:

1. Escaneo exhaustivo de aplicaciones web.
2. Soporte para múltiples lenguajes y frameworks (PHP, ASP.NET, Java, Ruby, etc.).
3. Detección de vulnerabilidades comunes (SQLi, XSS, inclusión de archivos locales).
4. Generación de informes detallados con sugerencias de remediación.
5. Personalización del alcance y parámetros del escaneo.

---

## Instalación

```bash
sudo apt-get install wapiti
```

---

## Uso

### Comando básico

```bash
sudo wapiti -u <url> -o <ubicacion>
```

### Ejemplo

```bash
sudo wapiti -u https://www.facebook.com/ -o /home/usuario
```

Esto generará un informe completo sobre la página web analizada.

<p align="center"> <img src="./Img/Ejemplo 1.png"> </p>

---
