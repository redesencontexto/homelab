# 02 — Creación de la primera máquina virtual

**Fase:** Fase 3 — Primera VM Linux
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Crear en Proxmox VE la primera máquina virtual del HomeLab y prepararla para instalar Ubuntu Server 26.04.1 LTS.

## 2. Contexto

En el paso anterior se cargó en Proxmox la imagen:

```text
ubuntu-26.04.1-live-server-amd64.iso
```

Con la ISO disponible en `pve01`, ya era posible comenzar a crear una máquina virtual que utilizara parte de los recursos físicos de la Dell Latitude E6430.

## 3. Inicio del asistente

Desde la interfaz web de Proxmox se utilizó la opción:

```text
Create VM
```

El asistente permitió definir progresivamente los componentes virtuales que tendría la nueva máquina.

El proceso general fue:

```text
Create VM
   ↓
Identificación
   ↓
Sistema operativo / ISO
   ↓
Sistema
   ↓
Disco
   ↓
CPU
   ↓
Memoria RAM
   ↓
Red
   ↓
Confirmación
```

## 4. Identificación de la VM

Proxmox utiliza un identificador numérico para distinguir cada máquina virtual.

Cada VM dispone además de un nombre que permite reconocer fácilmente su función.

Conceptualmente:

```text
Proxmox
   │
   ├── VM 1
   ├── VM 2
   ├── VM 3
   └── ...
```

El identificador utilizado por nuestra VM puede consultarse actualmente desde la interfaz de Proxmox.

No es necesario inventarlo ni reconstruirlo de memoria.

## 5. Selección del sistema operativo

Como medio de instalación se seleccionó la ISO previamente cargada:

```text
ubuntu-26.04.1-live-server-amd64.iso
```

Esto permitió que, al iniciar la máquina virtual, Ubuntu Server pudiera arrancar como si tuviera conectado un medio de instalación físico.

## 6. Configuración del sistema virtual

Durante el asistente se revisaron las opciones relacionadas con el hardware virtual de la máquina.

Proxmox crea una representación virtual de componentes como:

* firmware;
* chipset;
* controlador de disco;
* unidad de instalación;
* tarjeta de red;
* otros dispositivos virtuales.

La VM no posee estos componentes físicamente.

Son proporcionados por el hipervisor.

## 7. Disco virtual

Se creó un disco virtual para instalar Ubuntu Server.

Conceptualmente:

```text
SSD físico de pve01
        │
        ▼
     Proxmox
        │
        ▼
   Disco virtual
        │
        ▼
 Ubuntu Server
```

El sistema invitado percibe este disco como si fuera una unidad de almacenamiento propia.

En realidad, el espacio procede del almacenamiento físico disponible en `pve01`.

## 8. CPU virtual

A la máquina se le asignaron recursos de procesamiento desde el procesador físico de la Dell Latitude E6430.

```text
Intel Core i7-3720QM
        │
        ▼
     Proxmox
        │
        ▼
     vCPU de VM
```

Asignar procesadores virtuales no significa que se creen nuevos núcleos físicos.

Proxmox administra el acceso de las máquinas virtuales a los recursos disponibles del host.

## 9. Memoria RAM

También se asignó memoria a la VM desde los 16 GB disponibles físicamente en `pve01`.

Conceptualmente:

```text
16 GB RAM física
        │
        ▼
     Proxmox
        │
        ├── Proxmox
        ├── VM Linux
        └── futuras VM
```

Esto hace importante evitar asignar todos los recursos físicos a una sola máquina virtual.

El nodo también necesita memoria para funcionar.

## 10. Interfaz de red virtual

La VM recibió una tarjeta de red virtual.

Esta interfaz permite conectar Ubuntu Server con la infraestructura de red a través de Proxmox.

Conceptualmente:

```text
Ubuntu Server
      │
      ▼
Tarjeta virtual
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

Esta fue nuestra primera utilización práctica de la relación entre una máquina virtual y el bridge de Proxmox.

El estudio más profundo de bridges, VLAN y networking virtual se realizará en la **Fase 7 — Networking virtual**.

## 11. Confirmación de la configuración

Después de revisar los parámetros del asistente se confirmó la creación de la VM.

Proxmox añadió entonces la nueva máquina a la estructura de `pve01`.

La arquitectura pasó de:

```text
pve01
└── Proxmox VE
```

a:

```text
pve01
└── Proxmox VE
    └── Primera VM Linux
```

## 12. Hardware virtual vs. hardware físico

Esta práctica permitió entender una diferencia fundamental.

### Hardware físico

Existe realmente dentro de la Dell:

* CPU;
* RAM;
* SSD;
* tarjeta de red.

### Hardware virtual

Es presentado por Proxmox a Ubuntu:

* vCPU;
* RAM asignada;
* disco virtual;
* tarjeta de red virtual.

```text
HARDWARE FÍSICO
Dell E6430
      │
      ▼
   Proxmox
      │
      ▼
HARDWARE VIRTUAL
      │
      ▼
Ubuntu Server
```

## 13. Recursos exactos de la VM

Los valores exactos actualmente configurados no necesitan reconstruirse de memoria.

Pueden verificarse directamente en Proxmox entrando en:

```text
pve01
   ↓
VM
   ↓
Hardware
```

Desde allí pueden consultarse, entre otros:

* Memory;
* Processors;
* Hard Disk;
* Network Device;
* CD/DVD Drive.

Esto permite que la bitácora utilice la configuración realmente existente en lugar de valores aproximados.

## 14. Consideración sobre asignación de recursos

`pve01` dispone de recursos limitados.

Por ello, cada VM debe dimensionarse según su función.

Asignar demasiados recursos puede impedir crear nuevas máquinas o afectar el funcionamiento del host.

Asignar muy pocos puede provocar bajo rendimiento dentro del sistema invitado.

La planificación de recursos será cada vez más importante conforme aumente el número de máquinas virtuales.

## 15. Verificación

La creación se consideró correcta cuando:

* la VM apareció dentro de `pve01`;
* la ISO de Ubuntu Server quedó asociada;
* existía un disco virtual;
* había CPU y RAM asignadas;
* la interfaz de red virtual estaba disponible;
* la máquina podía iniciarse.

## 16. Qué aprendí

* Una máquina virtual utiliza recursos del host físico.
* Proxmox presenta hardware virtual al sistema invitado.
* Una VM tiene su propio disco, RAM, CPU y tarjeta de red desde la perspectiva del sistema operativo invitado.
* Los recursos virtuales siguen dependiendo de las capacidades físicas de `pve01`.
* `vmbr0` permite conectar las máquinas virtuales con la red.
* Los valores de configuración pueden verificarse posteriormente desde la sección Hardware de Proxmox.
* Crear una VM no instala automáticamente el sistema operativo.

## 17. Resultado

* [x] Primera VM creada en Proxmox.
* [x] Ubuntu Server seleccionado como sistema a instalar.
* [x] ISO asociada a la VM.
* [x] Disco virtual creado.
* [x] Recursos de CPU asignados.
* [x] Memoria RAM asignada.
* [x] Interfaz de red virtual configurada.
* [x] VM preparada para iniciar el instalador.

## 18. Próximo paso

Iniciar la máquina virtual desde la ISO e instalar Ubuntu Server 26.04.1 LTS en el disco virtual.

---

**Estado final:** 🟢 Completado
