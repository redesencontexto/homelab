# 02 — Respaldo de la información

**Fase:** Fase 1 — Preparación física
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Proteger la información almacenada en la Dell Latitude E6430 antes de reutilizar su SSD para la instalación de Proxmox VE.

## 2. Contexto

La Dell Latitude E6430 todavía contenía archivos y un sistema operativo utilizado anteriormente.

Como el equipo sería dedicado al HomeLab, se planificó una instalación de Proxmox directamente sobre el hardware.

Este tipo de instalación podía sobrescribir el contenido existente del SSD.

Por esta razón, antes de continuar era necesario realizar un respaldo de la información que debía conservarse.

## 3. Riesgo identificado

El principal riesgo era perder archivos importantes durante la instalación del nuevo sistema.

Conceptualmente:

```text
SSD con información existente
          │
          ▼
Instalación del nuevo sistema
          │
          ▼
Posible sobrescritura del disco
          │
          ▼
Pérdida de datos
```

El respaldo debía realizarse antes de modificar particiones o comenzar la instalación.

## 4. Acción realizada

Se revisaron los archivos almacenados en la Dell y se realizó una copia de la información que debía conservarse.

Una vez completado el respaldo, el equipo podía reutilizarse sin depender del contenido existente en el SSD.

## 5. Importancia del respaldo previo

Este procedimiento aplica no solamente a Proxmox.

Antes de realizar operaciones como:

* instalar un sistema operativo;
* reformatear un disco;
* modificar particiones;
* reemplazar almacenamiento;
* realizar cambios destructivos;

debe comprobarse si existe información que necesite preservarse.

La preparación correcta puede evitar una pérdida de datos irreversible.

## 6. Diferencia entre respaldo y snapshot

En esta etapa se realizó un **respaldo de archivos existentes en un equipo físico**.

Esto no debe confundirse con los snapshots que se utilizarán más adelante en las máquinas virtuales.

```text
Respaldo previo
    │
    └── Protege información antes de cambiar el sistema

Snapshot
    │
    └── Captura posteriormente el estado de una VM
```

Los mecanismos formales de backups y snapshots del HomeLab se abordarán en la **Fase 4 — Backups y snapshots**.

## 7. Verificación

Antes de continuar se comprobó que la información necesaria estuviera disponible fuera del equipo que iba a ser modificado.

Esto permitió continuar con la preparación del nodo sin depender del sistema anterior.

## 8. Consideración de seguridad

Los respaldos también deben protegerse.

Dependiendo del contenido, conviene considerar:

* ubicación segura;
* control de acceso;
* cifrado cuando sea necesario;
* evitar copias innecesarias;
* comprobar que los archivos respaldados puedan abrirse correctamente.

La existencia de una copia no garantiza por sí sola que el respaldo sea útil.

## 9. Qué aprendí

* Un cambio de sistema operativo puede implicar pérdida de datos.
* Los respaldos deben realizarse antes de comenzar cambios destructivos.
* No basta con copiar archivos; también conviene comprobar que la copia sea accesible.
* Un respaldo previo y un snapshot de una máquina virtual son conceptos diferentes.
* La preparación de un servidor comienza antes de instalar el software.

## 10. Resultado

* [x] Información existente revisada.
* [x] Archivos necesarios respaldados.
* [x] Riesgo de pérdida de datos mitigado.
* [x] Dell preparada para continuar con su reutilización.
* [x] Sistema anterior dejado sin dependencia para el proyecto.

## 11. Próximo paso

Preparar una memoria USB booteable con el instalador de Proxmox VE para poder iniciar la Dell desde un medio externo.

---

**Estado final:** 🟢 Completado
