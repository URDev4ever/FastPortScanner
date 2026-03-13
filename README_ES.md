<h1 align="center">FastPortScanner</h1>
<p align="center">
  🇺🇸 <a href="README.md"><b>English</b></a> |
  🇪🇸 <a href="README_ES.md">Español</a>
</p>
<h3 align="center">Un escáner de puertos TCP de alto rendimiento escrito en Java usando I/O no bloqueante (java.nio).</h3>

Diseñado para escanear miles de puertos rápidamente mientras recopila **banners básicos de servicios y fingerprints**.

El escáner utiliza una **arquitectura de pipeline con sockets asíncronos y selectors**, permitiendo una gran cantidad de conexiones concurrentes mientras mantiene un uso de recursos relativamente bajo.

---

## Features

* ⚡ **Escaneo asíncrono rápido** usando Java NIO
* 🔗 **Hasta 2000 conexiones concurrentes**
* 📡 **Banner grabbing** para identificación de servicios
* 🧠 **Fingerprinting básico de servicios**
* 🎯 **Modo de escaneo rápido de los Top-25 puertos**
* 📊 **Barra de progreso en vivo**
* 🎨 **Salida de terminal con colores**
* 📋 **Detección automática de servicios**

---

## Cómo Funciona

En lugar de escanear puertos secuencialmente, el escáner utiliza un **modelo de pipeline no bloqueante**:

1. Los puertos se colocan en una cola para escaneo.
2. Múltiples conexiones se abren de forma asíncrona.
3. Cuando una conexión tiene éxito, el escáner:

   * opcionalmente envía un **service probe**
   * espera una **respuesta de banner**
4. La respuesta es analizada para **identificar el servicio**.

Esto permite escanear miles de puertos simultáneamente.

---

## Detección de Servicios Soportada

El escáner detecta servicios comunes usando:

### Mapeo de Puertos Conocidos

Ejemplos:

| Port  | Service    |
| ----- | ---------- |
| 21    | FTP        |
| 22    | SSH        |
| 25    | SMTP       |
| 80    | HTTP       |
| 443   | HTTPS      |
| 3306  | MySQL      |
| 5432  | PostgreSQL |
| 6379  | Redis      |
| 27017 | MongoDB    |

---

### Fingerprinting por Banner

El escáner también revisa banners buscando identificadores comunes como:

* `OpenSSH`
* `Apache`
* `nginx`
* `HTTP/1.1`
* `MySQL`
* `PostgreSQL`
* `Redis`

---

## Instalación

Compilar el programa con:

```bash
javac FastPortScanner.java
```

---

## Uso

Escaneo básico:

```bash
java FastPortScanner <host>
```

Ejemplo:

```bash
java FastPortScanner scanme.nmap.org
```

---

### Escaneo Rápido (Top 25 Puertos)

```bash
java FastPortScanner <host> --top
```

Ejemplo:

```bash
java FastPortScanner 192.168.1.1 --top
```

Esto escanea solo los **25 puertos más comunes**, lo cual es significativamente más rápido.

---

## Ejemplo de Salida

```
OPEN PORTS FOUND:

┌────────┬──────────────────┬────────────────────────────────────────────┐
│ Port   │ Service          │ Banner                                     │
├────────┼──────────────────┼────────────────────────────────────────────┤
│ 22     │ ssh              │ SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.5    │
│ 80     │ http             │ HTTP/1.1 200 OK                            │
│ 443    │ https            │ HTTP/1.1 400 Bad Request                   │
└────────┴──────────────────┴────────────────────────────────────────────┘

Summary:
► Found 3 open ports
► Scan finished in 2.1s
```

---

## Detalles Técnicos

Tecnologías clave utilizadas:

* **Java NIO**

  * `SocketChannel`
  * `Selector`
  * `SelectionKey`
* **I/O de red no bloqueante**
* **Gestión de conexiones concurrentes**
* **Banner probing**
* **Fingerprint matching simple**

Conexiones concurrentes máximas:

```
2000
```

---

## Limitaciones

Esta herramienta está pensada para **aprendizaje y experimentación**.

No implementa técnicas avanzadas como:

* Escaneo SYN
* Escaneo UDP
* Detección de sistema operativo
* Fingerprinting avanzado de servicios
* Técnicas de evasión

Para escaneos profesionales usá herramientas como **Nmap**.

---

## Disclaimer

Esta herramienta está destinada únicamente a **fines educativos y pruebas de seguridad autorizadas**.

No escanees sistemas sin permiso.

---

Hecho con <3 por URDev.
