# 02 — Creación de snapshots de `ubuntu-server-01`

**Fase:** Fase 4 — Backups y snapshots
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Crear puntos de recuperación de la máquina virtual `ubuntu-server-01` antes de continuar realizando cambios sobre el sistema.

## 2. Contexto

Después de instalar y verificar Ubuntu Server, la máquina virtual se encontraba en un estado funcional.

Antes de comenzar nuevas configuraciones se decidió utilizar snapshots para conservar estados conocidos de la VM.

La máquina protegida en esta fase es:

```text
ubuntu-server-01
```

## 3. Acceso a snapshots en Proxmox

Desde la interfaz web de Proxmox se seleccionó la máquina virtual:

```text
pve01
   ↓
ubuntu-server-01
```

Dentro de las opciones de la VM se accedió a:

```text
Snapshots
```

Desde esta sección es posible:

* visualizar snapshots existentes;
* crear nuevos snapshots;
* identificar cuándo fueron creados;
* restaurar un estado anterior;
* eliminar snapshots cuando ya no sean necesarios.

## 4. Primer snapshot

Se creó un punto de recuperación identificado como:

```text
antes de cambios
```

El propósito de este snapshot era conservar un estado funcional antes de realizar modificaciones adicionales sobre Ubuntu Server.

Conceptualmente:

```text
ubuntu-server-01
      │
      ▼
Estado funcional
      │
      ▼
Snapshot
"antes de cambios"
      │
      ▼
Realizar pruebas
```

Si posteriormente un cambio causaba problemas, existía un punto al cual volver.

## 5. Segundo snapshot

También se creó un snapshot identificado como:

```text
post-instalación
```

Este punto representa el estado de la VM después de completar la instalación y dejar Ubuntu Server operativo.

Su utilidad es conservar una referencia cercana al estado inicial del servidor.

```text
Instalación de Ubuntu
        ↓
Configuración inicial
        ↓
VM funcional
        ↓
Snapshot
"post-instalación"
```

## 6. Importancia de nombres descriptivos

El nombre de un snapshot debe permitir comprender qué estado representa.

Por ejemplo:

```text
post-instalación
antes de cambios
antes-de-docker
antes-de-actualizacion
```

son más útiles que nombres como:

```text
snapshot1
prueba
nuevo
test
```

Un nombre descriptivo facilita la recuperación cuando existen varios puntos disponibles.

## 7. Orden temporal de los snapshots

Los snapshots permiten visualizar diferentes estados de la VM a lo largo del tiempo.

Conceptualmente:

```text
Instalación
    ↓
VM funcional
    ↓
post-instalación
    ↓
Configuraciones
    ↓
antes de cambios
    ↓
Nuevas pruebas
```

La existencia de varios puntos permite seleccionar el estado más apropiado según el problema que se quiera resolver.

## 8. ¿Qué protege un snapshot?

El snapshot está asociado al estado de la máquina virtual.

Dependiendo de las opciones utilizadas y de la infraestructura, puede incluir elementos relacionados con:

* discos virtuales;
* configuración de la VM;
* estado de ejecución.

No debe asumirse que funciona igual que una copia independiente almacenada fuera del nodo.

Por esa razón continúa siendo necesario disponer de backups.

## 9. Uso previsto en el HomeLab

Los snapshots se utilizarán principalmente antes de:

* instalar software importante;
* modificar servicios;
* realizar cambios de red;
* cambiar configuraciones críticas;
* comenzar una práctica con posibilidad de afectar el sistema.

Por ejemplo, antes de instalar Docker podría resultar útil conservar un estado estable de Ubuntu Server.

## 10. Precaución con los snapshots

Aunque son muy útiles, no conviene acumular snapshots indefinidamente sin necesidad.

A medida que se mantengan cambios asociados a ellos pueden:

* consumir almacenamiento;
* complicar la administración;
* dejar puntos antiguos que ya no aportan valor.

Por ello deben utilizarse de forma intencional.

## 11. Verificación

Después de crear los snapshots se comprobó que aparecieran en la sección correspondiente de `ubuntu-server-01`.

Los puntos identificados fueron:

* `antes de cambios`
* `post-instalación`

Esto confirmó que Proxmox había registrado correctamente los estados seleccionados.

## 12. Qué aprendí

* Los snapshots se crean desde la propia VM en Proxmox.
* Un snapshot permite conservar un punto de recuperación.
* Es importante utilizar nombres que describan claramente el estado guardado.
* Los snapshots son especialmente útiles antes de cambios importantes.
* Tener varios snapshots permite conservar diferentes momentos de la evolución de una VM.
* No deben mantenerse snapshots innecesarios indefinidamente.
* Un snapshot sigue sin sustituir un backup.

## 13. Resultado

* [x] VM `ubuntu-server-01` identificada.
* [x] Se accedió a la sección Snapshots.
* [x] Snapshot `antes de cambios` creado.
* [x] Snapshot `post-instalación` creado.
* [x] Puntos de recuperación verificados.
* [x] Uso de nombres descriptivos aplicado.
* [x] VM preparada para realizar cambios con mayor seguridad.

## 14. Próximo paso

Comprender cómo se utiliza un snapshot para volver a un estado anterior y qué implicaciones tiene realizar un rollback sobre una máquina virtual.

---

**Estado final:** 🟢 Completado
