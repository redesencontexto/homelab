# 04 — Backup de `ubuntu-server-01` en Proxmox

**Fase:** Fase 4 — Backups y snapshots
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Crear una copia de seguridad de la máquina virtual `ubuntu-server-01` utilizando las herramientas de backup de Proxmox VE.

El propósito era disponer de una copia que pudiera utilizarse para recuperar la máquina virtual en caso de pérdida, corrupción o una configuración que impidiera continuar trabajando normalmente.

## 2. Contexto

Hasta este momento ya se habían creado snapshots de `ubuntu-server-01`.

Sin embargo, un snapshot no sustituye una copia de seguridad.

Por esta razón, el siguiente paso fue utilizar el mecanismo de backup de Proxmox.

```text
ubuntu-server-01
       │
       ├── Snapshots
       │     └── Recuperación rápida
       │
       └── Backup
             └── Copia restaurable
```

## 3. Máquina virtual protegida

La máquina utilizada fue:

```text
ubuntu-server-01
```

Esta corresponde a la primera VM Linux creada durante la Fase 3.

En ella se encuentra instalado Ubuntu Server.

## 4. Backup desde Proxmox

Proxmox VE dispone de herramientas integradas para generar copias de seguridad de máquinas virtuales.

Desde la interfaz de administración se seleccionó la VM y se accedió a las opciones correspondientes al backup.

Conceptualmente:

```text
pve01
   ↓
ubuntu-server-01
   ↓
Backup
   ↓
Crear copia
```

## 5. Almacenamiento

Para generar el backup fue necesario seleccionar un almacenamiento disponible en Proxmox que admitiera este tipo de contenido.

La ubicación exacta del almacenamiento utilizado forma parte de la configuración interna del HomeLab y puede verificarse directamente desde Proxmox.

Lo importante en esta fase fue comprender que:

> Una copia de seguridad necesita un destino donde almacenarse.

Esto será especialmente relevante más adelante cuando se diseñe una estrategia de respaldo más robusta.

## 6. Ejecución del backup

Una vez seleccionados los parámetros correspondientes, se inició la creación de la copia de seguridad de `ubuntu-server-01`.

Durante el proceso, Proxmox realizó las operaciones necesarias para generar una versión restaurable de la VM.

El flujo general fue:

```text
ubuntu-server-01
       ↓
Iniciar backup
       ↓
Proxmox procesa la VM
       ↓
Generar copia
       ↓
Almacenar backup
       ↓
Backup disponible
```

## 7. Verificación

Después de finalizar el proceso se comprobó que la copia apareciera disponible en Proxmox.

La existencia del backup permitía pasar al siguiente paso importante:

```text
Crear backup
     ↓
¿Existe la copia?
     ↓
Sí
     ↓
Probar restauración
```

Comprobar únicamente que un archivo de backup existe no demuestra todavía que pueda utilizarse correctamente.

Por esta razón se decidió realizar una prueba de restauración.

## 8. Diferencia con los snapshots creados

En esta fase se utilizaron ambos mecanismos.

### Snapshot

Ejemplos creados:

```text
post-instalación
antes de cambios
```

Se utilizaron como puntos de estado de la VM.

### Backup

Se creó una copia destinada a poder reconstruir una máquina virtual a partir del respaldo.

Esto permitió pasar de:

```text
"Tengo una copia"
```

a una pregunta más importante:

```text
"¿Puedo recuperar una VM utilizando esa copia?"
```

## 9. Por qué probar un backup

Una copia de seguridad que nunca ha sido probada introduce incertidumbre.

Puede existir un archivo de backup, pero todavía deben responderse preguntas como:

* ¿Proxmox puede leerlo?
* ¿Puede restaurarse?
* ¿Se crea correctamente una nueva VM?
* ¿Arranca el sistema restaurado?
* ¿Los datos y configuración están disponibles?
* ¿Es posible iniciar sesión?

Por esta razón, la fase no terminó simplemente después de crear el backup.

## 10. Estrategia de restauración utilizada

Para no poner en riesgo la VM original se decidió probar el backup creando una máquina virtual separada.

La idea fue:

```text
ubuntu-server-01
      │
      ▼
    Backup
      │
      ▼
Restaurar como otra VM
      │
      ▼
ubuntu-server-01-restore-test
```

Así se podía comprobar el respaldo sin sustituir inmediatamente la máquina original.

## 11. Importancia de conservar la VM original

Realizar la prueba sobre una VM independiente permite comparar:

```text
VM original
ubuntu-server-01
```

con:

```text
VM restaurada
ubuntu-server-01-restore-test
```

Esto reduce el riesgo durante una prueba de recuperación.

## 12. Estrategia inicial de backup

La experiencia permitió establecer una regla sencilla:

```text
Crear backup
      ↓
Comprobar que terminó
      ↓
Verificar que existe
      ↓
Restaurar una copia de prueba
      ↓
Arrancar
      ↓
Comprobar el sistema
```

El último paso es especialmente importante.

## 13. Limitaciones actuales

Esta implementación representa una estrategia inicial de aprendizaje.

Todavía será necesario evaluar en el futuro:

* almacenamiento físicamente separado;
* copias externas;
* frecuencia de backups;
* retención;
* capacidad disponible;
* automatización;
* protección ante fallo completo de `pve01`;
* estrategia de recuperación ante desastre.

Un backup almacenado únicamente dentro de la misma infraestructura física puede seguir siendo vulnerable ante determinados fallos del nodo.

## 14. Qué aprendí

* Un backup y un snapshot cumplen funciones diferentes.
* Proxmox permite crear copias de seguridad de máquinas virtuales.
* El backup necesita un almacenamiento de destino.
* Que un backup termine correctamente no demuestra por sí solo que la recuperación funciona.
* Las copias deben probarse.
* Una restauración puede realizarse como una VM independiente para no afectar la original.
* La recuperación forma parte de la estrategia de backup.

## 15. Resultado

* [x] `ubuntu-server-01` seleccionada para backup.
* [x] Backup iniciado desde Proxmox.
* [x] Proceso de backup completado.
* [x] Copia disponible para restauración.
* [x] Diferencia entre snapshot y backup aplicada en la práctica.
* [x] Necesidad de probar la restauración identificada.
* [x] VM original conservada.
* [x] Backup preparado para prueba de recuperación.

## 16. Próximo paso

Restaurar el backup como una máquina virtual independiente llamada `ubuntu-server-01-restore-test` y comprobar que el sistema recuperado pueda arrancar y utilizarse correctamente.

---

**Estado final:** 🟢 Completado
