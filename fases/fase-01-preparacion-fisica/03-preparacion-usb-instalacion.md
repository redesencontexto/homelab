# 03 — Preparación del USB de instalación

**Fase:** Fase 1 — Preparación física
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Preparar una memoria USB booteable con el instalador de Proxmox VE para utilizarla como medio de instalación en la Dell Latitude E6430.

## 2. Contexto

Después de evaluar la Dell y respaldar la información necesaria, el siguiente paso fue preparar un medio desde el cual pudiera iniciarse el instalador de Proxmox.

La memoria USB permitiría arrancar el equipo desde un sistema externo, sin depender del sistema operativo instalado previamente en el SSD.

## 3. Elementos necesarios

Para preparar el medio de instalación fueron necesarios:

* una memoria USB;
* la imagen ISO de Proxmox VE;
* una computadora para preparar el USB;
* una herramienta capaz de grabar la imagen ISO en la memoria.

## 4. Descarga de la imagen ISO

Se obtuvo la imagen ISO de Proxmox VE desde la fuente oficial.

Una imagen ISO contiene la estructura necesaria para crear un medio de instalación arrancable.

Conceptualmente:

```text
Archivo ISO
    │
    ▼
Herramienta de grabación
    │
    ▼
Memoria USB booteable
```

## 5. Preparación de la memoria USB

La imagen ISO fue grabada en la memoria USB utilizando una herramienta destinada a crear medios booteables.

Este proceso no consiste simplemente en copiar el archivo `.iso` dentro de la memoria.

La herramienta escribe la imagen de forma que el equipo pueda arrancar desde ella.

## 6. Consideración importante

La preparación del USB puede eliminar el contenido que exista previamente en la memoria.

Antes de continuar conviene comprobar que el USB no contenga información importante.

## 7. Arranque desde USB

Una vez preparado el medio, la Dell Latitude E6430 debía ser configurada para arrancar desde la memoria USB.

El flujo esperado era:

```text
Encender Dell E6430
        ↓
Acceder al menú de arranque
        ↓
Seleccionar memoria USB
        ↓
Iniciar instalador
```

En esta fase se considera completada la preparación cuando el equipo dispone de un medio válido para comenzar la instalación.

El proceso de instalación de Proxmox pertenece a la siguiente fase.

## 8. Diferencia entre preparar e instalar

Es importante separar ambos procesos.

### Preparación del medio

Consiste en:

* obtener la ISO;
* preparar el USB;
* verificar que pueda utilizarse como medio de arranque.

### Instalación

Consiste en:

* iniciar el instalador;
* seleccionar el disco;
* configurar el sistema;
* instalar Proxmox VE;
* reiniciar y validar el nodo.

La instalación se documentará en la **Fase 2 — Proxmox**.

## 9. Verificación

La preparación se considera correcta cuando:

* la memoria USB contiene el medio de instalación;
* la Dell reconoce el dispositivo;
* el equipo puede seleccionarlo como opción de arranque.

## 10. Qué aprendí

* Una ISO no se utiliza igual que un archivo convencional.
* Para instalar un sistema desde USB es necesario crear un medio booteable.
* Preparar un USB puede borrar la información existente en él.
* El menú de arranque permite elegir temporalmente desde qué dispositivo iniciar un equipo.
* La preparación del medio y la instalación del sistema son etapas diferentes.

## 11. Resultado

* [x] Imagen ISO de Proxmox VE obtenida.
* [x] Memoria USB preparada.
* [x] Medio de instalación disponible.
* [x] Dell preparada para arrancar desde USB.
* [x] Equipo listo para comenzar la instalación de Proxmox.

## 12. Cierre de la Fase 1

Con la evaluación del equipo, el respaldo de la información y la preparación del medio de instalación, la Dell Latitude E6430 quedó lista para convertirse en el nodo de virtualización del HomeLab.

```text
Evaluación
    ↓
Respaldo
    ↓
USB booteable
    ↓
Equipo preparado
    ↓
FASE 2 — PROXMOX
```

## 13. Próximo paso

Iniciar la Dell desde la memoria USB e instalar Proxmox VE directamente sobre el SSD del equipo.

---

**Estado final:** 🟢 Fase 1 completada
