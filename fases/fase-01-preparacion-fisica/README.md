# Fase 1 — Preparación física

**Estado:** ✅ Completada
**Documentación:** Retrospectiva

## Objetivo

Preparar la Dell Latitude E6430 para convertirla posteriormente en el primer nodo de virtualización del HomeLab.

Esta fase comprende las acciones necesarias antes de comenzar la instalación de Proxmox VE.

## Punto de partida

Al comenzar esta fase se disponía de una Dell Latitude E6430 con las siguientes características:

* Intel Core i7-3720QM
* 16 GB de memoria RAM
* SSD de 480 GB
* Batería no funcional
* Información personal almacenada en el equipo
* Sistema operativo existente que sería sustituido posteriormente

Durante la Fase 0 se había decidido reutilizar este equipo como nodo principal de virtualización.

Antes de modificarlo era necesario preparar el hardware y proteger la información existente.

## Actividades realizadas

### Revisión del equipo

Se confirmó que la Dell disponía de recursos suficientes para comenzar el laboratorio y que sería utilizada como equipo dedicado al HomeLab.

También se mantuvo identificada una limitación importante:

> La batería no funciona, por lo que el equipo depende completamente de la alimentación eléctrica.

### Respaldo de información

Antes de reemplazar el sistema operativo existente se realizó un respaldo de los archivos que debían conservarse.

Esta acción era necesaria porque la instalación posterior de Proxmox utilizaría el SSD del equipo y eliminaría el sistema anterior.

### Preparación del medio de instalación

Se preparó una memoria USB para utilizarla como medio de instalación de Proxmox VE.

El objetivo era poder iniciar la Dell desde el USB en lugar del sistema almacenado en el SSD.

### Preparación para el arranque desde USB

Se verificó que el equipo pudiera iniciar desde el medio USB preparado.

El inicio efectivo del instalador y la instalación de Proxmox corresponden a la **Fase 2 — Proxmox**.

## Separación entre Fase 1 y Fase 2

La Fase 1 termina cuando el equipo queda preparado para iniciar la instalación.

```text
FASE 1
Preparar equipo
     ↓
Respaldar información
     ↓
Preparar USB
     ↓
Dejar el equipo listo para instalar
     │
     ▼
FASE 2
Instalar Proxmox
```

Esto permite separar claramente:

* **preparación del equipo**, de
* **instalación y configuración del hipervisor**.

## Consideración de seguridad

El respaldo previo es especialmente importante cuando un equipo existente será reutilizado.

Antes de instalar un sistema operativo o hipervisor directamente sobre un disco debe comprobarse qué información necesita conservarse.

Una instalación destructiva puede provocar la pérdida de los datos existentes.

## Limitación eléctrica

La batería no funcional continúa siendo una limitación del nodo.

En esta fase no se resolvió todavía el problema.

Se mantiene como mejora futura:

* reemplazar la batería;
* incorporar un UPS;
* mejorar la protección eléctrica del laboratorio.

## Entradas de la bitácora

| Entrada | Tema                                      | Estado           |
| ------- | ----------------------------------------- | ---------------- |
| 01      | Evaluación y preparación de la Dell E6430 | ⬜ Por documentar |
| 02      | Respaldo de la información                | ⬜ Por documentar |
| 03      | Preparación del USB de instalación        | ⬜ Por documentar |

## Resultado esperado

Al completar esta fase, la Dell Latitude E6430 debía:

* estar identificada como equipo dedicado al HomeLab;
* tener respaldada la información necesaria;
* disponer de un medio USB preparado para la instalación;
* estar lista para iniciar la instalación de Proxmox VE.

## Resultado obtenido

La información necesaria fue respaldada y el equipo quedó preparado para iniciar desde el medio USB destinado a la instalación de Proxmox.

La instalación del hipervisor quedó reservada para la siguiente fase.

## Próxima fase

**Fase 2 — Proxmox**
