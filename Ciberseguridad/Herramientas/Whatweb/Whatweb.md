## Escaneo con Whatweb

**Whatweb** puede recolectar información como:

- Plataforma en la que se construyó el sitio
- Tipo de script utilizado
- Google Analytics
- Dirección IP o país
- Plataforma de servidor web

Whatweb utiliza tanto **escaneo activo** como **pasivo**:

- Activo: extrae más profundamente con varias tecnologías
- Pasivo: obtiene datos de los encabezados HTTP

---

## Instalación

```bash
sudo apt-get install whatweb
```

---

## Uso

### Ejemplo básico

```bash
whatweb ajedrezpinal.com
```

<p align="center"> <img src="./Img/Ejemplo 1.png"> </p>

Resultado: dirección IP, país, cookies, tipo de script y encabezados HTTP.

---

### Análisis detallado

```bash
whatweb -v ajedrezpinal.com
```

**-v** = análisis detallado, explora el sitio con mayor profundidad.

<p align="center"> <img src="./Img/Ejemplo 2.png"> </p>

<p align="center"> <img src="./Img/Ejemplo 3.png"> </p>

<p align="center"> <img src="./Img/Ejemplo 4.png"> </p>

Después del análisis detallado, se muestran cadenas y descripciones de plugins detectados.

---
