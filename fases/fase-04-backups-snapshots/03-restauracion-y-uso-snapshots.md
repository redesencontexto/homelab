# 03 — Restauración y uso de snapshots

**Fase:** Fase 4 — Backups y snapshots
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva
**Rollback realizado:** No

---

## 1. Objetivo

Comprender cómo puede utilizarse un snapshot para devolver una máquina virtual a un estado anterior y conocer las precauciones que deben tomarse antes de realizar un rollback.

Durante esta fase **no fue necesario restaurar `ubuntu-server-01`**, por lo que el procedimiento se estudió sin ejecutar una recuperación real.

## 2. Contexto

En la entrada anterior se crearon puntos de recuperación para:

```text
ubuntu-server-01
```

Entre ellos:

```text
post-instalación
antes de cambios
```

Estos snapshots permiten disponer de estados anteriores de la VM en caso de que una modificación posterior provoque problemas.

## 3. ¿Qué significa hacer rollback?

Un rollback consiste en devolver la máquina virtual al estado representado por un snapshot.

Conceptualmente:

```text
Estado A
VM funcionando
    ↓
Crear snapshot
    ↓
Estado B
Realizar cambios
    ↓
Problema
    ↓
Rollback
    ↓
Volver al Estado A
```

Esto puede resultar muy útil durante un laboratorio.

## 4. Qué implica volver a un snapshot

Restaurar un snapshot no debe tratarse como una acción sin consecuencias.

Si después del snapshot se realizaron modificaciones, estas pueden perderse al volver al estado anterior.

Por ejemplo:

```text
Snapshot
   │
   ▼
Instalar paquete
Crear archivo
Cambiar configuración
   │
   ▼
Rollback
   │
   ▼
Los cambios posteriores
pueden dejar de existir
```

Por esta razón, antes de restaurar debe comprobarse qué información se creó o modificó después del snapshot.

## 5. Ejemplo con `ubuntu-server-01`

Supongamos que antes de instalar un servicio se utiliza:

```text
antes de cambios
```

Después se realiza una configuración que deja Ubuntu sin funcionar correctamente.

La recuperación podría plantearse como:

```text
ubuntu-server-01
       ↓
Configuración incorrecta
       ↓
Problema
       ↓
Snapshot: antes de cambios
       ↓
Rollback
       ↓
Estado anterior
```

Esto evita tener que reinstalar completamente Ubuntu por un cambio que pueda revertirse.

## 6. Uso desde Proxmox

La administración se realiza desde:

```text
pve01
   ↓
ubuntu-server-01
   ↓
Snapshots
```

Desde esta sección Proxmox permite seleccionar un punto existente y disponer de opciones relacionadas con su administración y recuperación.

Antes de ejecutar una restauración debe verificarse cuidadosamente:

* qué snapshot se ha seleccionado;
* qué fecha o estado representa;
* qué cambios se perderían;
* si existen datos recientes importantes;
* si sería conveniente realizar primero un backup.

## 7. Snapshot actual y estados anteriores

Los snapshots pueden entenderse como puntos dentro de la evolución de una VM.

Ejemplo:

```text
Ubuntu instalado
       ↓
post-instalación
       ↓
Cambios iniciales
       ↓
antes de cambios
       ↓
Configuración nueva
       ↓
Estado actual
```

Restaurar un punto anterior implica retroceder en esa evolución.

## 8. ¿Cuándo tendría sentido hacer rollback?

Un rollback puede resultar útil cuando:

* una actualización provoca problemas;
* una configuración deja un servicio inutilizable;
* se instala software que afecta al sistema;
* una práctica modifica demasiados elementos;
* se quiere repetir un laboratorio desde un estado conocido.

## 9. ¿Cuándo no conviene hacerlo inmediatamente?

Antes de hacer rollback conviene evaluar la situación si:

* existen archivos importantes creados después del snapshot;
* existen datos que deben conservarse;
* el problema puede solucionarse fácilmente;
* no se conoce exactamente qué estado representa el snapshot;
* existe riesgo de perder trabajo posterior.

La recuperación debe ser una decisión consciente.

## 10. Snapshot antes de experimentar

Una práctica útil para el HomeLab será:

```text
Estado estable
      ↓
Crear snapshot
      ↓
Realizar laboratorio
      ↓
¿Resultado?
   /         \
Correcto     Problema
   ↓            ↓
Continuar    Evaluar rollback
```

Esto será especialmente útil en fases posteriores donde se modificarán servicios y configuraciones.

## 11. Diferencia entre solucionar y restaurar

Disponer de snapshots no significa que debamos restaurar la VM ante cualquier error.

Dentro de un laboratorio, investigar un problema también aporta aprendizaje.

Por ejemplo:

```text
Aparece un error
      ↓
Diagnosticar
      ↓
¿Puedo comprenderlo y solucionarlo?
     /        \
   Sí          No
   ↓           ↓
Resolver    Evaluar rollback
```

El snapshot funciona como una red de seguridad, no como sustituto del troubleshooting.

## 12. Restauración realizada durante esta fase

Durante esta fase:

```text
Rollback ejecutado: NO
```

`ubuntu-server-01` permaneció funcional y no fue necesario devolverla a ninguno de los snapshots creados.

Por tanto, la bitácora no presenta una restauración real que no haya ocurrido.

El primer rollback efectivo que se realice en el futuro deberá documentarse en la fase o práctica donde sea necesario.

## 13. Qué aprendí

* Un rollback devuelve una VM al estado representado por un snapshot.
* Los cambios posteriores al snapshot pueden perderse.
* Antes de restaurar es necesario identificar correctamente el punto de recuperación.
* Puede ser conveniente realizar un backup antes de un rollback importante.
* Los snapshots son especialmente útiles para experimentar.
* Disponer de un snapshot no elimina la necesidad de diagnosticar problemas.
* En esta fase no fue necesario realizar una restauración real.

## 14. Resultado

* [x] Concepto de rollback comprendido.
* [x] Consecuencias de restaurar un snapshot identificadas.
* [x] Uso de snapshots como protección antes de cambios comprendido.
* [x] Diferencia entre troubleshooting y rollback identificada.
* [x] Procedimiento de recuperación localizado en Proxmox.
* [x] Se documentó correctamente que no se realizó un rollback real.

## 15. Próximo paso

Configurar y documentar una copia de seguridad de `ubuntu-server-01` mediante las herramientas de backup disponibles en Proxmox VE.

---

**Estado final:** 🟢 Completado
