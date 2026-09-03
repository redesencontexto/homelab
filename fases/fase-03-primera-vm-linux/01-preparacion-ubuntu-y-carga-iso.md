# 01 — Preparación de Ubuntu Server y carga de la ISO

**Fase:** Fase 3 — Primera VM Linux
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Preparar la imagen de instalación de Ubuntu Server y dejarla disponible dentro de Proxmox para utilizarla en la creación de la primera máquina virtual Linux del HomeLab.

## 2. Contexto

Después de completar la instalación y configuración de Proxmox VE en `pve01`, el siguiente objetivo era crear la primera máquina virtual.

Para ello era necesario disponer de una imagen ISO de un sistema operativo Linux que pudiera utilizarse como medio de instalación virtual.

Se seleccionó Ubuntu Server.

## 3. Sistema operativo seleccionado

La versión utilizada fue:

**Ubuntu Server 26.04.1 LTS**

El archivo ISO utilizado fue:

```text
ubuntu-26.04.1-live-server-amd64.iso
```

La extensión `.iso` identifica una imagen de disco que contiene los archivos necesarios para iniciar e instalar el sistema operativo.

## 4. Ubicación original de la ISO

La imagen ya había sido descargada previamente en la computadora de administración.

Se encontraba en:

```text
D:\ISO VM
```

Por tanto, no fue necesario realizar nuevamente una descarga que ya se había completado.

## 5. Diferencia entre almacenar una ISO en la PC y utilizarla en Proxmox

Aunque el archivo existiera en la computadora de administración, Proxmox no podía utilizar directamente una ruta local de Windows como:

```text
D:\ISO VM
```

La ISO debía quedar disponible dentro de un almacenamiento accesible por `pve01`.

Conceptualmente:

```text
PC Windows
   │
   │ Archivo ISO
   ▼
D:\ISO VM
   │
   │ Carga
   ▼
Proxmox
   │
   ▼
Almacenamiento de imágenes ISO
```

## 6. Almacenamiento en Proxmox

Desde la interfaz web de Proxmox se seleccionó el almacenamiento destinado a imágenes ISO.

A continuación se utilizó la opción de carga para seleccionar desde la computadora:

```text
ubuntu-26.04.1-live-server-amd64.iso
```

y transferirla al nodo.

## 7. Proceso de carga

El flujo fue:

```text
Archivo ISO en Windows
        ↓
Seleccionar desde Proxmox
        ↓
Upload / Cargar
        ↓
Transferencia hacia pve01
        ↓
ISO disponible en Proxmox
```

La duración del proceso dependió del tamaño del archivo y de la velocidad de la red utilizada para transferirlo.

## 8. Verificación

Una vez completada la carga se comprobó que la imagen apareciera en el almacenamiento de Proxmox destinado a imágenes ISO.

La presencia del archivo permitió confirmar que podía utilizarse posteriormente en el asistente de creación de máquinas virtuales.

## 9. Concepto aprendido: ISO virtual

En un equipo físico se podría utilizar una memoria USB para instalar Ubuntu.

En una máquina virtual, Proxmox puede presentar una imagen ISO como si fuera un medio de instalación conectado al equipo virtual.

Comparación:

```text
Equipo físico

USB / DVD
    ↓
Instalador
    ↓
Sistema operativo


Máquina virtual

Archivo ISO
    ↓
Unidad virtual
    ↓
Instalador
    ↓
Sistema operativo
```

Esto permite crear servidores sin necesitar una memoria USB física para cada máquina virtual.

## 10. Relación entre PC, Proxmox e ISO

Después de completar este paso, la arquitectura era:

```text
PC de administración
        │
        │ Carga de ISO
        ▼
      pve01
   Proxmox VE
        │
        ▼
ubuntu-26.04.1-live-server-amd64.iso
        │
        ▼
Disponible para crear VM
```

## 11. Consideración de almacenamiento

Las imágenes ISO ocupan espacio en el almacenamiento de Proxmox.

A medida que el HomeLab crezca será conveniente:

* eliminar imágenes que ya no sean necesarias;
* conservar las que se utilicen frecuentemente;
* controlar el espacio disponible;
* evitar almacenar múltiples copias innecesarias.

## 12. Consideración de seguridad

Antes de utilizar imágenes de sistemas operativos conviene obtenerlas de fuentes confiables.

También pueden utilizarse mecanismos de verificación de integridad cuando sea necesario.

La ISO utilizada para el HomeLab debe tratarse como parte del software base de la infraestructura.

## 13. Qué aprendí

* Una ISO contiene una imagen de instalación de un sistema operativo.
* Tener una ISO en la computadora no significa que Proxmox pueda utilizarla directamente.
* El archivo debe estar disponible en un almacenamiento accesible por el nodo.
* Proxmox puede utilizar una ISO como medio de instalación virtual.
* Una misma ISO puede utilizarse para crear múltiples máquinas virtuales.
* Las imágenes ISO también consumen espacio del almacenamiento del nodo.

## 14. Resultado

* [x] Ubuntu Server seleccionado como primer sistema Linux.
* [x] ISO localizada en la computadora de administración.
* [x] Archivo `ubuntu-26.04.1-live-server-amd64.iso` identificado.
* [x] ISO cargada en Proxmox.
* [x] Imagen disponible para crear la primera VM.

## 15. Próximo paso

Crear la primera máquina virtual en Proxmox y definir los recursos virtuales que utilizará para ejecutar Ubuntu Server.

---

**Estado final:** 🟢 Completado
