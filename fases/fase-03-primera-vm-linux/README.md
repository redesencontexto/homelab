# Fase 3 — Primera VM Linux

**Estado:** ✅ Completada
**Documentación:** Retrospectiva

## Objetivo

Crear e instalar la primera máquina virtual Linux del HomeLab sobre el nodo Proxmox `pve01`.

Esta fase representa el paso desde disponer únicamente del hipervisor hacia comenzar a utilizar realmente la infraestructura de virtualización.

## Punto de partida

Al comenzar esta fase:

* Proxmox VE ya estaba instalado en la Dell Latitude E6430.
* El nodo `pve01` estaba operativo.
* La interfaz web de Proxmox era accesible desde la computadora de administración.
* Todavía no se había creado la primera máquina virtual Linux.

El siguiente objetivo era desplegar un servidor Linux virtualizado.

## Sistema operativo seleccionado

Se eligió:

**Ubuntu Server 26.04.1 LTS**

La imagen utilizada fue:

```text
ubuntu-26.04.1-live-server-amd64.iso
```

La ISO ya se encontraba descargada en la computadora de administración, concretamente en:

```text
D:\ISO VM
```

Por esta razón no fue necesario descargar nuevamente la imagen.

## Incorporación de la ISO a Proxmox

Para que Proxmox pudiera utilizar la imagen de instalación, fue necesario incorporarla al almacenamiento del nodo.

El proceso conceptual fue:

```text
PC de administración
        │
        │ ubuntu-26.04.1-live-server-amd64.iso
        ▼
      Proxmox
        │
        ▼
 Almacenamiento ISO
        │
        ▼
Creación de la VM
```

Una vez disponible dentro de Proxmox, la ISO pudo seleccionarse como medio de instalación de la nueva máquina virtual.

## Creación de la primera máquina virtual

Desde la interfaz web de Proxmox se inició el asistente de creación de una nueva VM.

Durante el proceso se configuraron progresivamente elementos como:

* identificación de la VM;
* imagen ISO;
* sistema operativo;
* disco virtual;
* CPU;
* memoria RAM;
* interfaz de red.

La máquina virtual utilizaría recursos proporcionados por `pve01`.

Conceptualmente:

```text
Dell Latitude E6430
        │
        ▼
      pve01
   Proxmox VE
        │
        ▼
   Primera VM Linux
        │
        ▼
Ubuntu Server 26.04.1 LTS
```

## Inicio de la máquina virtual

Una vez creada la VM, se inició desde Proxmox.

La imagen ISO de Ubuntu Server actuó como medio de instalación virtual.

Esto es equivalente conceptualmente a utilizar un USB de instalación en un equipo físico, pero en este caso el medio está asociado virtualmente a la VM.

```text
Equipo físico                    Máquina virtual

USB booteable                    ISO
     │                            │
     ▼                            ▼
Instalador                 Instalador Ubuntu
     │                            │
     ▼                            ▼
Disco físico                Disco virtual
```

## Instalación de Ubuntu Server

La máquina virtual inició correctamente el instalador de Ubuntu Server.

Durante el proceso se recorrieron las diferentes pantallas de configuración del sistema.

Entre los elementos tratados estuvieron:

* idioma;
* teclado;
* red;
* almacenamiento;
* configuración del servidor;
* usuario;
* instalación del sistema.

## Configuración de red

Durante el instalador se trabajó con la configuración de red de Ubuntu Server.

Se utilizó una dirección de ejemplo como guía para comprender qué valores debían sustituirse por los correspondientes al entorno real.

Este ejercicio permitió trabajar conceptos como:

* dirección IP;
* prefijo de red;
* gateway;
* DNS;
* configuración estática.

Los valores reales utilizados en el HomeLab no necesitan publicarse en la documentación.

Cuando sea necesario mostrar configuraciones de ejemplo se utilizarán datos ficticios.

## Uso del instalador de Ubuntu Server

La instalación también sirvió para familiarizarse con la interfaz basada principalmente en teclado de Ubuntu Server.

Durante el proceso fue necesario aprender a desplazarse entre:

* campos;
* botones;
* opciones;
* menús.

Esto es diferente de un instalador gráfico tradicional y forma parte de la experiencia inicial de administración de servidores Linux.

## Diferencia entre host y máquina virtual

Esta fase introduce una distinción fundamental.

### Host

El equipo que proporciona los recursos:

```text
Dell Latitude E6430
        ↓
      pve01
    Proxmox VE
```

### Guest o sistema invitado

El sistema que se ejecuta dentro del entorno virtualizado:

```text
Máquina virtual
        ↓
Ubuntu Server
```

Por tanto, Ubuntu Server no está instalado directamente en la Dell.

La arquitectura queda:

```text
Hardware físico
      │
      ▼
 Proxmox VE
      │
      ▼
Máquina virtual
      │
      ▼
Ubuntu Server
```

## Recursos virtuales

Los recursos de una VM no son nuevos componentes físicos.

Proxmox asigna parte de los recursos disponibles en `pve01` a la máquina virtual.

Por ejemplo:

```text
pve01
├── CPU física
├── 16 GB RAM física
└── SSD físico
        │
        ▼
      Proxmox
        │
        ▼
VM Linux
├── CPU virtual
├── RAM asignada
└── Disco virtual
```

Esto permitirá posteriormente ejecutar otras máquinas virtuales mientras los recursos físicos del nodo sean suficientes.

## Primera experiencia de virtualización completa

Hasta esta fase el HomeLab tenía:

```text
Hardware
   ↓
Proxmox
```

Después de esta fase pasa a tener:

```text
Hardware
   ↓
Proxmox
   ↓
Máquina virtual
   ↓
Linux
```

Este es un cambio importante porque a partir de ahora podemos comenzar a desplegar servicios dentro del laboratorio sin instalar cada sistema directamente sobre un equipo físico independiente.

## Consideraciones de seguridad

La documentación pública de la VM no debe mostrar innecesariamente:

* contraseñas;
* direcciones IP reales;
* credenciales;
* claves;
* datos personales;
* información sensible de la red.

Las capturas utilizadas en futuras entradas deberán revisarse antes de incorporarse al repositorio.

## Entradas de la bitácora

| Entrada | Tema                                           | Estado           |
| ------- | ---------------------------------------------- | ---------------- |
| 01      | Preparación de Ubuntu Server y carga de la ISO | ⬜ Por documentar |
| 02      | Creación de la primera máquina virtual         | ⬜ Por documentar |
| 03      | Instalación de Ubuntu Server                   | ⬜ Por documentar |
| 04      | Configuración inicial de red y servidor        | ⬜ Por documentar |
| 05      | Verificación de la primera VM Linux            | ⬜ Por documentar |

## Resultado esperado

Al completar esta fase se debía disponer de:

* una ISO de Ubuntu Server disponible en Proxmox;
* una máquina virtual creada;
* Ubuntu Server instalado;
* configuración básica del sistema realizada;
* conectividad preparada;
* primera VM Linux disponible para continuar el HomeLab.

## Resultado obtenido

Se creó la primera máquina virtual Linux del HomeLab utilizando Ubuntu Server 26.04.1 LTS sobre Proxmox VE.

Con esta implementación, `pve01` pasó de ser únicamente un hipervisor operativo a comenzar a alojar sistemas invitados.

## Próxima fase

**Fase 4 — Backups y snapshots**

Antes de incorporar nuevos servicios, se estudiará cómo proteger las máquinas virtuales mediante mecanismos de recuperación.
