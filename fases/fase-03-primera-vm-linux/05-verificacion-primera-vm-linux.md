# 05 — Verificación de la primera VM Linux

**Fase:** Fase 3 — Primera VM Linux
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Comprobar que la primera máquina virtual Linux del HomeLab quedó correctamente instalada y operativa después de completar la instalación de Ubuntu Server 26.04.1 LTS.

## 2. Contexto

En los pasos anteriores se:

* cargó la ISO de Ubuntu Server en Proxmox;
* creó la primera máquina virtual;
* asignaron recursos virtuales;
* instaló Ubuntu Server;
* configuró la red;
* reinició la máquina después de la instalación.

El último paso de la fase consistía en verificar que el sistema invitado pudiera utilizarse normalmente.

## 3. Arranque después de la instalación

Una vez terminada la instalación, la máquina virtual fue reiniciada.

Ubuntu Server debía iniciar desde el disco virtual donde había sido instalado y no depender permanentemente de la imagen ISO.

Conceptualmente:

```text
Antes

ISO de Ubuntu
      ↓
Instalador
      ↓
Disco virtual


Después

Disco virtual
      ↓
Ubuntu Server
      ↓
Sistema operativo
```

El sistema arrancó correctamente después de la instalación.

## 4. Inicio de sesión

Desde la consola de Proxmox se accedió al sistema Ubuntu utilizando las credenciales creadas durante la instalación.

Esto permitió confirmar que:

* el sistema operativo estaba instalado;
* el usuario había sido creado correctamente;
* Ubuntu podía utilizarse desde su terminal;
* la VM estaba funcionando independientemente del instalador.

Las credenciales reales no se incluyen en la documentación pública.

## 5. Verificación del sistema

Una vez dentro de Ubuntu Server se pueden utilizar diferentes comandos para comprobar el estado del sistema.

### Identidad del servidor

```bash
hostname
```

Permite consultar el nombre asignado al sistema invitado.

### Información del sistema

```bash
uname -a
```

Permite obtener información sobre el kernel y la arquitectura del sistema.

### Dirección de red

```bash
ip addr
```

Permite comprobar que la interfaz de red dispone de la configuración esperada.

### Tabla de rutas

```bash
ip route
```

Permite verificar la existencia de la ruta por defecto y el gateway utilizado por el servidor.

## 6. Verificación de conectividad

La conectividad puede comprobarse progresivamente.

### Gateway

```bash
ping -c 4 DIRECCION_DEL_GATEWAY
```

Comprueba la comunicación con la puerta de enlace de la red.

### Conectividad IP externa

```bash
ping -c 4 8.8.8.8
```

Permite verificar si existe comunicación IP hacia el exterior.

### Resolución DNS

```bash
ping -c 4 ubuntu.com
```

Si el nombre puede resolverse y existe respuesta, se comprueba además el funcionamiento de DNS.

Las direcciones reales de la infraestructura no se publican en esta bitácora.

## 7. Relación entre Proxmox y Ubuntu

Una vez operativa la VM, la arquitectura del HomeLab quedó:

```text
Dell Latitude E6430
        │
        ▼
      pve01
   Proxmox VE
        │
        ▼
  Máquina virtual
        │
        ▼
Ubuntu Server 26.04.1 LTS
```

Existen ahora dos sistemas que deben distinguirse claramente:

### `pve01`

Es el **host**.

Su función es ejecutar Proxmox y proporcionar recursos a las máquinas virtuales.

### Ubuntu Server

Es el **guest** o sistema invitado.

Su función será ejecutar servicios y prácticas dentro del HomeLab.

## 8. Administración desde Proxmox

Desde la interfaz de Proxmox es posible controlar aspectos de la VM como:

* iniciar;
* apagar;
* reiniciar;
* abrir consola;
* revisar CPU;
* revisar memoria;
* consultar hardware virtual;
* modificar determinados recursos.

Esto no sustituye la administración del sistema operativo.

Proxmox administra la **máquina virtual**, mientras que Ubuntu se administra desde el propio sistema invitado.

```text
Proxmox
   │
   └── Administra la VM
            │
            ▼
       Ubuntu Server
            │
            └── Administra servicios,
                usuarios, paquetes,
                archivos y red del SO
```

## 9. QEMU Guest Agent

Durante esta fase también se introdujo el concepto de **QEMU Guest Agent**.

El agente permite mejorar la comunicación entre Proxmox y el sistema operativo invitado.

Conceptualmente:

```text
Proxmox
   │
   │ comunicación
   ▼
QEMU Guest Agent
   │
   ▼
Ubuntu Server
```

Puede ayudar a Proxmox a obtener información y realizar determinadas operaciones de forma más coordinada con la VM.

Entre sus posibles utilidades se encuentran:

* informar direcciones IP del guest;
* mejorar ciertas operaciones de apagado;
* facilitar la comunicación entre hipervisor y sistema invitado;
* colaborar con determinadas operaciones de administración y respaldo.

Su presencia no convierte Ubuntu en parte de Proxmox; siguen siendo sistemas separados.

## 10. Máquina virtual vs. equipo físico

La primera VM permitió comprobar en la práctica que un sistema virtual puede comportarse como un servidor independiente.

Ubuntu dispone de:

* CPU;
* memoria;
* almacenamiento;
* tarjeta de red;
* hostname;
* usuarios;
* dirección IP;
* sistema operativo.

Sin embargo, sus recursos proceden del nodo físico `pve01`.

```text
RECURSOS FÍSICOS
Dell E6430
      │
      ▼
   Proxmox
      │
      ▼
RECURSOS VIRTUALES
      │
      ▼
Ubuntu Server
```

## 11. Estado alcanzado

Antes de esta fase:

```text
Dell
  ↓
Proxmox
```

Después de esta fase:

```text
Dell
  ↓
Proxmox
  ↓
VM
  ↓
Ubuntu Server
```

El HomeLab dispone ahora de su primer servidor virtual Linux.

## 12. Qué aprendí

* Crear una VM y tener un sistema operativo instalado son procesos diferentes.
* Una VM puede arrancar y funcionar como un servidor independiente.
* El host Proxmox y el guest Ubuntu cumplen funciones diferentes.
* Ubuntu dispone de sus propios usuarios, hostname y configuración de red.
* `ip addr` permite revisar las interfaces y direcciones.
* `ip route` permite comprobar la tabla de rutas.
* La conectividad debe verificarse por etapas.
* Proxmox administra el hardware virtual mientras Ubuntu administra el sistema operativo invitado.
* QEMU Guest Agent permite una mejor comunicación entre Proxmox y el sistema invitado.
* La virtualización permite reutilizar un único equipo físico para ejecutar múltiples sistemas.

## 13. Resultado

* [x] Ubuntu Server instalado.
* [x] VM reiniciada correctamente.
* [x] Sistema iniciado desde el disco virtual.
* [x] Inicio de sesión funcional.
* [x] Configuración de red disponible.
* [x] Primera VM Linux operativa.
* [x] Diferencia host/guest comprendida.
* [x] Concepto de QEMU Guest Agent introducido.
* [x] VM preparada para las siguientes fases del HomeLab.

## 14. Cierre de la Fase 3

Con Ubuntu Server funcionando correctamente dentro de Proxmox queda completada la primera implementación de un sistema operativo invitado del HomeLab.

```text
FASE 0 — Planificación ✅
        ↓
FASE 1 — Preparación física ✅
        ↓
FASE 2 — Proxmox ✅
        ↓
FASE 3 — Primera VM Linux ✅
```

El laboratorio dispone ahora de:

* un nodo físico;
* un hipervisor;
* una primera máquina virtual;
* un servidor Linux funcional.

## 15. Próximo paso

**Fase 4 — Backups y snapshots**

Antes de comenzar a instalar servicios adicionales dentro de la VM, se estudiarán mecanismos que permitan proteger su estado y recuperarla ante errores.

---

**Estado final:** 🟢 Fase 3 completada
