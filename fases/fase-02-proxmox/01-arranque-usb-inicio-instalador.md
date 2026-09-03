# 01 — Arranque desde USB e inicio del instalador

**Fase:** Fase 2 — Proxmox
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Iniciar la Dell Latitude E6430 desde la memoria USB preparada previamente y acceder al instalador de Proxmox VE.

## 2. Contexto

Al finalizar la Fase 1, la Dell ya estaba preparada para dejar de utilizar su sistema anterior y convertirse en el nodo principal de virtualización del HomeLab.

La memoria USB con Proxmox VE estaba lista, por lo que el siguiente paso consistía en arrancar el equipo desde ese medio externo.

## 3. Flujo de arranque

El proceso esperado era:

```text
Dell apagada
    ↓
USB conectado
    ↓
Encender equipo
    ↓
Abrir menú de arranque
    ↓
Seleccionar USB
    ↓
Cargar instalador de Proxmox
```

El objetivo era evitar que el equipo iniciara nuevamente desde el SSD interno.

## 4. Selección del dispositivo de arranque

Durante el encendido se accedió al menú de arranque de la Dell.

Desde allí se seleccionó la memoria USB que contenía el instalador de Proxmox VE.

Esto permitió modificar temporalmente el dispositivo desde el cual iniciaría el equipo.

No fue necesario utilizar todavía el sistema almacenado en el SSD.

## 5. Inicio del instalador

Después de seleccionar correctamente el USB, el equipo cargó el entorno de instalación de Proxmox VE.

A partir de este punto, la Dell estaba lista para comenzar la instalación del hipervisor sobre el SSD interno.

## 6. Concepto aprendido: orden de arranque

Los equipos pueden disponer de varios dispositivos capaces de iniciar un sistema, por ejemplo:

* SSD;
* HDD;
* memoria USB;
* unidad óptica;
* red.

El firmware del equipo determina desde cuál de ellos intenta arrancar.

El menú de arranque permite seleccionar manualmente un dispositivo para una sesión determinada.

## 7. Diferencia entre BIOS/UEFI y sistema operativo

Antes de que Windows, Linux o Proxmox comiencen a ejecutarse, el firmware del equipo realiza las tareas iniciales de hardware y determina desde qué dispositivo arrancar.

Por ello, seleccionar un USB booteable ocurre antes de que exista un sistema operativo activo.

Conceptualmente:

```text
Encendido
   ↓
BIOS / UEFI
   ↓
Dispositivo de arranque
   ↓
Bootloader
   ↓
Sistema o instalador
```

## 8. Verificación

El paso se consideró exitoso cuando:

* la Dell reconoció la memoria USB;
* fue posible seleccionarla como dispositivo de arranque;
* apareció el entorno de instalación de Proxmox VE.

## 9. Problemas encontrados

No se documentó ningún problema crítico que impidiera iniciar el instalador.

Si en futuras reinstalaciones el USB no aparece como opción de arranque, será necesario revisar aspectos como:

* preparación correcta del USB;
* puerto USB utilizado;
* configuración de BIOS/UEFI;
* modo de arranque;
* integridad de la imagen ISO.

## 10. Qué aprendí

* Un medio booteable debe seleccionarse como dispositivo de arranque.
* El menú de arranque actúa antes de que cargue el sistema operativo.
* BIOS/UEFI y sistema operativo cumplen funciones distintas.
* Poder iniciar el instalador desde USB confirma que la preparación de la Fase 1 fue correcta.

## 11. Resultado

* [x] USB conectado.
* [x] Memoria reconocida por la Dell.
* [x] Dispositivo USB seleccionado para arrancar.
* [x] Instalador de Proxmox VE iniciado.
* [x] Equipo listo para comenzar la instalación.

## 12. Próximo paso

Instalar Proxmox VE sobre el SSD de 480 GB de la Dell Latitude E6430 y convertir el equipo en el nodo `pve01`.

---

**Estado final:** 🟢 Completado
