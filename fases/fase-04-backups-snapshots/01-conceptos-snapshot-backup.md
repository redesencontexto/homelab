# 01 — Conceptos de snapshot y backup

**Fase:** Fase 4 — Backups y snapshots
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Comprender la diferencia entre un snapshot y un backup antes de utilizarlos sobre la primera máquina virtual Linux del HomeLab.

## 2. Contexto

Después de completar la instalación y verificación de `ubuntu-server-01`, el siguiente paso consistía en proteger la VM antes de comenzar a realizar cambios más importantes.

La idea principal era contar con mecanismos que permitieran reducir el impacto de una configuración incorrecta, una actualización fallida o una práctica que modificara el sistema de forma no deseada.

## 3. ¿Qué es un snapshot?

Un snapshot representa un punto de estado de una máquina virtual en un momento determinado.

Puede utilizarse antes de realizar cambios importantes.

Ejemplo:

```text
Ubuntu funcionando
       ↓
Crear snapshot
       ↓
Modificar configuración
       ↓
      ¿Falla?
      /    \
    No      Sí
    ↓       ↓
Continuar  Restaurar
```

Su principal utilidad dentro del HomeLab es facilitar un rollback rápido durante pruebas y experimentos.

## 4. ¿Qué es un backup?

Un backup es una copia de seguridad que permite conservar una versión recuperable de una máquina virtual.

Conceptualmente:

```text
Máquina virtual
      ↓
Generar backup
      ↓
Archivo o copia de respaldo
      ↓
Restauración futura
```

El backup está pensado para recuperación, no únicamente para volver atrás después de un cambio inmediato.

## 5. Diferencia principal

Aunque ambos mecanismos ayudan a recuperarse de errores, no deben considerarse equivalentes.

| Snapshot                                      | Backup                                                       |
| --------------------------------------------- | ------------------------------------------------------------ |
| Guarda un punto de estado                     | Crea una copia de seguridad                                  |
| Muy útil antes de cambios                     | Útil para recuperación posterior                             |
| Facilita rollback rápido                      | Permite restaurar la VM                                      |
| Depende del entorno y almacenamiento de la VM | Puede conservarse como copia separada según la configuración |
| No sustituye un backup                        | Forma parte de la estrategia de respaldo                     |

## 6. Ejemplo práctico

Supongamos que se va a instalar un nuevo servicio dentro de Ubuntu.

### Con snapshot

```text
VM estable
   ↓
Snapshot
   ↓
Instalar servicio
   ↓
Algo falla
   ↓
Rollback
```

### Con backup

```text
VM
   ↓
Backup
   ↓
Problema grave o pérdida
   ↓
Restaurar copia
```

## 7. ¿Por qué no basta con snapshots?

Un snapshot resulta muy útil para pruebas, pero no debe ser la única estrategia de recuperación.

Si ocurre un problema serio con:

* el almacenamiento;
* el nodo;
* la propia VM;
* la infraestructura física;

un snapshot puede no ofrecer el mismo nivel de protección que una copia de seguridad independiente.

Por eso se adoptó la regla:

> Snapshot para cambios y rollback rápido; backup para recuperación.

## 8. ¿Por qué aprender esto antes de Docker?

La siguiente fase del HomeLab corresponde a Docker.

Instalar Docker y comenzar a desplegar servicios modificará el estado actual de `ubuntu-server-01`.

Antes de avanzar conviene disponer de una base conocida y recuperable.

```text
Ubuntu limpio y funcional
        ↓
Protección
        ↓
Docker
        ↓
Contenedores
        ↓
Servicios
```

Esto permite experimentar con menor riesgo.

## 9. Estrategia inicial del HomeLab

Para esta etapa se adoptó una estrategia sencilla:

### Antes de cambios importantes

Evaluar si conviene crear un snapshot.

### De forma periódica

Mantener backups de la VM.

### Antes de una nueva fase

Comprobar que exista un estado conocido y recuperable.

## 10. Limitaciones de esta estrategia

La estrategia actual es adecuada para aprendizaje, pero todavía no representa una solución completa de respaldo.

Más adelante será necesario considerar aspectos como:

* almacenamiento separado del nodo;
* copias fuera del equipo principal;
* frecuencia;
* retención;
* capacidad;
* pruebas de restauración;
* automatización;
* protección ante pérdida física del servidor.

## 11. Qué aprendí

* Snapshot y backup no son lo mismo.
* Un snapshot facilita volver rápidamente a un estado anterior.
* Un backup está orientado a recuperación.
* Los snapshots no sustituyen una estrategia de copias de seguridad.
* Es conveniente proteger una VM antes de realizar cambios importantes.
* Una copia de seguridad solo es realmente útil si puede restaurarse.

## 12. Resultado

* [x] Concepto de snapshot comprendido.
* [x] Concepto de backup comprendido.
* [x] Diferencias principales identificadas.
* [x] Uso de snapshots definido para cambios importantes.
* [x] Uso de backups definido para recuperación.
* [x] Estrategia inicial del HomeLab establecida.

## 13. Próximo paso

Crear snapshots de `ubuntu-server-01` para conservar puntos de recuperación antes de continuar modificando el servidor.

---

**Estado final:** 🟢 Completado
