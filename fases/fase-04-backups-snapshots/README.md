# Fase 4 — Backups y snapshots

**Estado:** ✅ Completada
**Documentación:** Retrospectiva

## Objetivo

Aprender a proteger una máquina virtual antes de comenzar a realizar cambios más importantes dentro del HomeLab.

Esta fase introduce dos mecanismos fundamentales de protección en Proxmox:

* snapshots;
* backups.

El objetivo no es solamente saber dónde hacer clic, sino comprender qué protege cada mecanismo y cuándo utilizarlo.

## Punto de partida

Al comenzar esta fase ya se disponía de:

* nodo Proxmox `pve01`;
* primera máquina virtual Linux creada;
* Ubuntu Server instalado;
* VM `ubuntu-server-01` operativa;
* acceso funcional al servidor.

La arquitectura era:

```text
Dell Latitude E6430
        │
        ▼
      pve01
   Proxmox VE
        │
        ▼
ubuntu-server-01
   Ubuntu Server
```

Antes de comenzar a instalar nuevos servicios era conveniente disponer de mecanismos de recuperación.

## ¿Por qué proteger la VM?

A medida que el laboratorio avance se realizarán cambios como:

* instalación de paquetes;
* modificaciones de configuración;
* Docker;
* servicios de red;
* actualizaciones;
* pruebas de seguridad;
* automatizaciones.

Alguno de estos cambios puede provocar errores.

Por ello es conveniente poder volver a un estado funcional.

```text
VM funcionando
      │
      ▼
Realizar cambio
      │
      ├── Funciona ✅
      │
      └── Falla ❌
              │
              ▼
          Recuperación
```

## Snapshot

Un snapshot permite conservar un punto determinado del estado de una máquina virtual.

Puede utilizarse antes de realizar cambios importantes.

Ejemplo:

```text
VM funcionando
      │
      ▼
Crear snapshot
      │
      ▼
Modificar sistema
      │
      ├── Todo funciona
      │       ↓
      │    Continuar
      │
      └── Algo falla
              ↓
         Restaurar snapshot
```

Durante esta fase se crearon snapshots de `ubuntu-server-01` para disponer de puntos de recuperación asociados a momentos importantes del laboratorio.

## Snapshots creados

Entre los puntos de recuperación utilizados estuvieron estados como:

```text
antes de cambios
```

y:

```text
post-instalación
```

Los nombres permiten identificar rápidamente qué representaba el estado guardado.

Esto es preferible a utilizar nombres poco descriptivos como:

```text
snapshot1
prueba
nuevo
```

## Backup

También se introdujo el concepto de copia de seguridad de una máquina virtual.

Un backup busca conservar una copia recuperable de la VM.

Conceptualmente:

```text
ubuntu-server-01
       │
       ▼
     Backup
       │
       ▼
Copia recuperable
```

A diferencia de trabajar únicamente con snapshots, una estrategia de respaldo debe permitir recuperar la máquina incluso después de determinados problemas que afecten su estado habitual.

## Snapshot vs. backup

Aunque ambos permiten recuperarse de problemas, no cumplen exactamente la misma función.

| Snapshot                                         | Backup                                                            |
| ------------------------------------------------ | ----------------------------------------------------------------- |
| Punto de estado de una VM                        | Copia de seguridad                                                |
| Útil antes de cambios                            | Útil para recuperación                                            |
| Normalmente asociado a la VM y su almacenamiento | Puede almacenarse como copia independiente según la configuración |
| Excelente para rollback rápido                   | Pensado para protección más duradera                              |
| No sustituye una estrategia de backup            | Forma parte de una estrategia de respaldo                         |

Por esta razón:

> Un snapshot no debe considerarse sustituto de un backup.

## Flujo utilizado en el HomeLab

La estrategia inicial quedó planteada de esta forma:

```text
VM estable
   │
   ▼
Snapshot
   │
   ▼
Realizar cambios
   │
   ▼
Verificar
   │
   ▼
Backup
```

No significa que siempre tenga que realizarse exactamente en ese orden.

El mecanismo utilizado dependerá del riesgo y del tipo de cambio.

## Uso de Proxmox

Proxmox permite administrar estos mecanismos desde su interfaz web.

Para una VM se pueden encontrar opciones relacionadas con:

* snapshots;
* backup;
* restore;
* tareas programadas;
* almacenamiento.

Esto permite administrar la protección de las máquinas virtuales desde el mismo hipervisor.

## Importancia del almacenamiento

Un backup necesita un lugar donde almacenarse.

Por ello, la estrategia de copias de seguridad depende también del almacenamiento disponible en la infraestructura.

A medida que el HomeLab evolucione será conveniente evaluar:

* almacenamiento separado;
* capacidad disponible;
* retención;
* frecuencia;
* copias externas;
* recuperación ante fallo completo del nodo.

La primera implementación de esta fase representa una base de aprendizaje, no todavía una estrategia empresarial completa de respaldo.

## Regla de trabajo adoptada

Antes de realizar cambios importantes en una VM:

```text
¿El cambio puede romper algo?
        │
        ├── No → continuar
        │
        └── Sí
             ↓
      Evaluar snapshot/backup
             ↓
        Realizar cambio
```

Esta práctica reduce el riesgo durante los experimentos del HomeLab.

## Entradas de la bitácora

| Entrada | Tema                                              | Estado           |
| ------- | ------------------------------------------------- | ---------------- |
| 01      | Conceptos de snapshot y backup                    | ⬜ Por documentar |
| 02      | Creación de snapshots de `ubuntu-server-01`       | ⬜ Por documentar |
| 03      | Restauración y uso de snapshots                   | ⬜ Por documentar |
| 04      | Configuración del backup en Proxmox               | ⬜ Por documentar |
| 05      | Verificación y estrategia inicial de recuperación | ⬜ Por documentar |

## Resultado esperado

Al completar esta fase se debía:

* comprender la diferencia entre snapshot y backup;
* crear puntos de recuperación para la primera VM;
* conocer dónde gestionar snapshots en Proxmox;
* configurar un mecanismo inicial de backup;
* comprender la importancia de verificar la recuperación;
* establecer una práctica de protección antes de cambios importantes.

## Resultado obtenido

`ubuntu-server-01` quedó protegida mediante puntos de recuperación y se comenzó a implementar una estrategia básica de backup desde Proxmox.

Esta fase establece una base importante antes de comenzar a instalar nuevos servicios dentro de la VM.

## Próxima fase

**Fase 5 — Docker**
