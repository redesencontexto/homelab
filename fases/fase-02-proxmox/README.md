# Fase 2 — Proxmox

**Estado:** ✅ Completada
**Documentación:** Retrospectiva

## Objetivo

Instalar Proxmox VE directamente sobre la Dell Latitude E6430 y dejar operativo el primer nodo de virtualización del HomeLab.

Esta fase convierte el equipo previamente preparado en un servidor capaz de alojar máquinas virtuales y contenedores.

## Punto de partida

Al comenzar esta fase:

* la Dell Latitude E6430 había sido evaluada;
* los archivos necesarios habían sido respaldados;
* se había preparado una memoria USB booteable con Proxmox VE;
* el equipo estaba listo para iniciar desde el medio de instalación.

La Dell todavía debía pasar de ser un equipo preparado a convertirse formalmente en el nodo de virtualización del laboratorio.

## Hardware utilizado

### Dell Latitude E6430

* Intel Core i7-3720QM
* 16 GB de RAM
* SSD de 480 GB
* batería no funcional
* conexión a la red local

## Plataforma seleccionada

Se eligió **Proxmox VE** como plataforma principal de virtualización del HomeLab.

Proxmox permite administrar desde una interfaz centralizada:

* máquinas virtuales;
* contenedores;
* almacenamiento;
* networking virtual;
* snapshots;
* backups;
* usuarios;
* permisos;
* otros componentes de infraestructura.

No todas estas funciones se utilizarán inmediatamente.

Cada una se incorporará cuando corresponda dentro de la ruta del proyecto.

## Instalación bare metal

Proxmox VE se instaló directamente sobre el hardware de la Dell.

Esto significa que el equipo dejó de utilizar su sistema operativo anterior y pasó a ejecutar Proxmox como sistema principal.

```text
ANTES

Dell E6430
    │
    ▼
Sistema operativo anterior


DESPUÉS

Dell E6430
    │
    ▼
Proxmox VE
    │
    ├── Máquinas virtuales
    └── Contenedores
```

Esta forma de instalación se conoce habitualmente como instalación **bare metal**.

## Nombre del nodo

Durante la configuración se estableció el nodo:

```text
pve01
```

El nombre permite identificar el servidor dentro de la infraestructura.

La convención también deja abierta la posibilidad de incorporar otros nodos en el futuro, por ejemplo:

```text
pve01
pve02
pve03
```

Esto no significa que actualmente existan varios nodos.

En este momento el HomeLab dispone únicamente de `pve01`.

## Acceso de administración

Después de completar la instalación, Proxmox quedó disponible para administración mediante su interfaz web.

La arquitectura inicial pasó a ser:

```text
PC de administración
        │
        │ Navegador web
        ▼
      pve01
   Proxmox VE
        │
        ▼
Infraestructura virtual
```

Esto permite administrar el nodo sin trabajar permanentemente desde la pantalla y el teclado de la Dell.

## Consideración sobre direccionamiento

Para que un servidor pueda administrarse de manera predecible, su configuración de red debe permitir localizarlo de forma consistente.

Los detalles específicos de direccionamiento real no tienen que publicarse en esta documentación.

Cuando sea necesario utilizar ejemplos se emplearán valores ficticios.

## Separación con fases posteriores

Durante esta fase se instala y valida Proxmox.

No se adelantarán todavía temas correspondientes a otras fases:

### Primera máquina virtual Linux

Corresponde a:

**Fase 3 — Primera VM Linux**

### Backups y snapshots

Corresponde a:

**Fase 4 — Backups y snapshots**

### Networking virtual avanzado

Corresponde a:

**Fase 7 — Networking virtual**

### Firewall

Corresponde a:

**Fase 8 — Firewall**

Esto evita mezclar la instalación inicial con configuraciones que se estudiarán posteriormente en profundidad.

## Entradas de la bitácora

| Entrada | Tema                                       | Estado           |
| ------- | ------------------------------------------ | ---------------- |
| 01      | Arranque desde USB e inicio del instalador | ⬜ Por documentar |
| 02      | Instalación de Proxmox VE                  | ⬜ Por documentar |
| 03      | Configuración inicial de `pve01`           | ⬜ Por documentar |
| 04      | Acceso y verificación del nodo             | ⬜ Por documentar |

## Resultado esperado

Al completar esta fase, la Dell debía:

* ejecutar Proxmox VE directamente sobre el hardware;
* estar identificada como `pve01`;
* disponer de conectividad;
* permitir acceso desde la computadora de administración;
* estar preparada para crear la primera máquina virtual.

## Resultado obtenido

Proxmox VE quedó instalado y operativo en la Dell Latitude E6430.

El nodo `pve01` puede administrarse mediante la interfaz web y constituye actualmente la base de virtualización del HomeLab.

## Próxima fase

**Fase 3 — Primera VM Linux**
