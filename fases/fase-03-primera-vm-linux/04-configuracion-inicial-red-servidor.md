# 04 — Configuración inicial de red y servidor

**Fase:** Fase 3 — Primera VM Linux
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Configurar y verificar los parámetros básicos de red de Ubuntu Server para que la primera máquina virtual Linux pudiera comunicarse correctamente dentro del HomeLab.

## 2. Contexto

Durante la instalación de Ubuntu Server fue necesario configurar la interfaz de red de la máquina virtual.

La VM no se conecta físicamente al router mediante un cable propio.

Su conectividad depende de la infraestructura virtual proporcionada por Proxmox.

Conceptualmente:

```text
Ubuntu Server
      │
      ▼
Interfaz de red virtual
      │
      ▼
    vmbr0
      │
      ▼
Interfaz física de pve01
      │
      ▼
   Red local
```

Por tanto, una configuración incorrecta dentro de Ubuntu podía impedir que la máquina virtual se comunicara con otros dispositivos.

## 3. Elementos de una configuración IP

Durante esta práctica se trabajó con varios parámetros fundamentales.

### Dirección IP

Identifica la máquina dentro de una red.

Ejemplo:

```text
192.168.10.20
```

### Prefijo de red

Permite determinar qué parte de la dirección identifica la red.

Ejemplo:

```text
/24
```

Un `/24` corresponde normalmente a:

```text
255.255.255.0
```

### Gateway

Es la dirección del dispositivo que permite alcanzar otras redes.

Ejemplo:

```text
192.168.10.1
```

### DNS

Permite traducir nombres como:

```text
ubuntu.com
```

en direcciones IP.

Ejemplo de DNS público:

```text
1.1.1.1
```

Los valores mostrados aquí son únicamente educativos y no representan necesariamente la configuración real del HomeLab.

## 4. Relación entre subnet y dirección IP

Uno de los puntos importantes durante la configuración fue comprender que Ubuntu Server distingue entre la **red** y la **dirección del equipo**.

Por ejemplo:

```text
Subnet:
192.168.10.0/24

Address:
192.168.10.20
```

No significan lo mismo.

La primera representa la red:

```text
192.168.10.0/24
```

mientras que la segunda identifica específicamente al servidor:

```text
192.168.10.20
```

Conceptualmente:

```text
Red
192.168.10.0/24
│
├── 192.168.10.1
├── 192.168.10.10
├── 192.168.10.20  ← servidor
├── 192.168.10.30
└── ...
```

## 5. Configuración estática

Para la primera VM Linux se trabajó con una configuración de red predecible.

Esto resulta especialmente útil para servidores porque posteriormente necesitaremos saber dónde encontrarlos.

Ejemplo:

```text
IP cambiante
    ↓
Más difícil administrar servicios

IP conocida
    ↓
Servidor localizable
```

Esto será importante cuando el HomeLab empiece a incorporar:

* SSH;
* Docker;
* DNS;
* monitoreo;
* Windows Server;
* servicios internos.

## 6. Introducción de los parámetros

Durante el instalador de Ubuntu Server se editarón la configuración IPv4 de la interfaz virtual.

Fue necesario completar correctamente los campos correspondientes a:

* subnet;
* address;
* gateway;
* name servers.

La interfaz del instalador obligó a prestar atención a la diferencia entre cada parámetro.

## 7. Interfaz de red de la VM

Ubuntu detectó una interfaz de red proporcionada por Proxmox.

Aunque desde el sistema operativo invitado parece una tarjeta normal, realmente es un dispositivo virtual.

```text
Ubuntu
   ↓
NIC virtual
   ↓
Proxmox
   ↓
NIC física
```

Este modelo permite que varias máquinas virtuales compartan la conectividad física del nodo.

## 8. Configuración del servidor

Además de la red, durante la instalación se definió la identidad básica del sistema.

Ubuntu Server dispone de:

* hostname propio;
* usuario administrativo inicial;
* contraseña;
* configuración de red independiente.

Esto significa que la VM funciona como un servidor separado de `pve01`.

```text
pve01
Proxmox VE
│
└── VM Ubuntu
    │
    ├── hostname propio
    ├── usuario propio
    ├── contraseña propia
    └── dirección IP propia
```

## 9. Host y guest

Esta fase permitió reforzar una distinción fundamental.

### Host

```text
pve01
```

Es el servidor físico que ejecuta Proxmox.

### Guest

```text
Ubuntu Server
```

Es el sistema operativo que se ejecuta dentro de la máquina virtual.

Un problema de red dentro de Ubuntu no significa necesariamente que Proxmox tenga un problema de red.

Cada nivel debe diagnosticarse por separado.

## 10. Verificaciones posteriores

Una vez iniciado Ubuntu Server, algunos comandos útiles para comprobar la configuración son:

### Ver las interfaces

```bash
ip addr
```

Permite revisar:

* interfaces;
* direcciones IPv4;
* direcciones IPv6;
* estado de cada interfaz.

### Ver las rutas

```bash
ip route
```

Permite comprobar la tabla de enrutamiento y localizar la ruta por defecto.

Un resultado conceptual sería:

```text
default via 192.168.10.1
```

Esto indica qué gateway utiliza el servidor.

### Comprobar conectividad con el gateway

```bash
ping 192.168.10.1
```

Utilizando en la práctica la dirección correspondiente al entorno real.

### Comprobar conectividad externa

```bash
ping 8.8.8.8
```

Si responde, existe conectividad IP hacia el exterior.

### Comprobar resolución DNS

```bash
ping ubuntu.com
```

Si puede resolver el nombre, DNS está funcionando además de la conectividad IP.

## 11. Diagnóstico por capas

Una forma útil de diagnosticar problemas es comprobar progresivamente:

```text
1. ¿La interfaz está activa?
        ↓
2. ¿Tiene dirección IP?
        ↓
3. ¿Existe gateway?
        ↓
4. ¿Puedo alcanzar el gateway?
        ↓
5. ¿Puedo alcanzar una IP externa?
        ↓
6. ¿Puedo resolver nombres DNS?
```

Esto evita cambiar configuraciones al azar cuando aparece un problema.

## 12. Importancia de no publicar la red real

La bitácora puede explicar perfectamente el procedimiento sin revelar todos los detalles reales de la infraestructura.

Por esta razón:

```text
IP real del HomeLab
        ↓
No necesariamente pública

IP ficticia equivalente
        ↓
Utilizada en documentación
```

Lo importante es comprender el concepto y poder reproducir el procedimiento.

## 13. Qué aprendí

* Subnet y dirección IP representan conceptos diferentes.
* El gateway permite salir de la red local.
* DNS permite resolver nombres.
* Una VM tiene su propia configuración IP.
* La interfaz de Ubuntu es virtual aunque el sistema la perciba como una tarjeta de red.
* `ip addr` permite comprobar las interfaces y direcciones.
* `ip route` permite revisar las rutas configuradas.
* Los problemas de conectividad deben diagnosticarse progresivamente.
* El host Proxmox y el guest Ubuntu deben tratarse como sistemas separados.

## 14. Resultado

* [x] Interfaz virtual identificada.
* [x] Configuración IPv4 realizada.
* [x] Subnet definida.
* [x] Dirección del servidor definida.
* [x] Gateway configurado.
* [x] DNS configurado.
* [x] Servidor preparado para verificar conectividad.
* [x] Información sensible excluida de la documentación pública.

## 15. Próximo paso

Verificar que Ubuntu Server arranque correctamente después de la instalación, iniciar sesión y comprobar que la primera VM Linux se encuentre completamente operativa.

---

**Estado final:** 🟢 Completado
