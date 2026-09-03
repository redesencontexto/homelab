# 02 — Instalación de Proxmox VE

**Fase:** Fase 2 — Proxmox
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Instalar Proxmox VE directamente sobre el SSD de la Dell Latitude E6430 para convertir el equipo en el primer nodo de virtualización del HomeLab.

## 2. Contexto

En el paso anterior se consiguió iniciar correctamente la Dell desde la memoria USB que contenía el instalador de Proxmox VE.

La información importante del equipo ya había sido respaldada durante la Fase 1, por lo que era posible continuar con una instalación que sustituiría el sistema operativo anterior.

## 3. Entorno utilizado

### Hardware

| Característica | Información          |
| -------------- | -------------------- |
| Equipo         | Dell Latitude E6430  |
| Procesador     | Intel Core i7-3720QM |
| Memoria RAM    | 16 GB                |
| Almacenamiento | SSD de 480 GB        |
| Batería        | No funcional         |

### Software

* Proxmox VE
* Instalador iniciado desde memoria USB

## 4. Tipo de instalación

Se decidió instalar Proxmox VE directamente sobre el hardware de la Dell.

La arquitectura resultante sería:

```text
Dell Latitude E6430
        │
        ▼
     Proxmox VE
        │
   ┌────┴────┐
   │         │
   ▼         ▼
  VM        LXC
```

Esto significa que Proxmox no se ejecutaría dentro de Windows ni dentro de otra máquina virtual.

El equipo quedaría dedicado principalmente al HomeLab.

## 5. Inicio de la instalación

Una vez cargado el instalador desde el USB, se seleccionó la opción correspondiente para instalar Proxmox VE.

A partir de ese momento comenzó el proceso de instalación sobre el equipo físico.

## 6. Selección del almacenamiento

Se seleccionó el SSD interno de 480 GB como destino de la instalación.

Esta era una decisión importante porque el contenido anterior del disco dejaría de utilizarse.

Conceptualmente:

```text
SSD antes
   │
   ├── Sistema operativo anterior
   └── Archivos existentes

        ↓ Instalación

SSD después
   │
   └── Proxmox VE
```

El respaldo realizado previamente permitió continuar sin depender de la información almacenada originalmente en el SSD.

## 7. Configuración durante la instalación

Durante el proceso se completaron los parámetros requeridos por el instalador para dejar preparado el nodo.

Entre ellos se incluyeron configuraciones relacionadas con:

* ubicación;
* zona horaria;
* teclado;
* credenciales administrativas;
* hostname;
* red de administración.

Los valores sensibles utilizados realmente no se incluyen en la documentación pública.

## 8. Nombre del nodo

Se estableció como nombre del nodo:

```text
pve01
```

Este nombre permite identificar claramente el servidor de Proxmox dentro del HomeLab.

La convención utilizada también facilita una posible expansión futura:

```text
pve01
pve02
pve03
```

Actualmente solamente existe `pve01`.

## 9. Credenciales administrativas

Durante la instalación fue necesario establecer credenciales para administrar Proxmox.

Estas credenciales:

* no se documentan públicamente;
* no se almacenan en este repositorio;
* no deben aparecer en capturas;
* no deben compartirse junto con la documentación.

La bitácora registra que fueron configuradas, pero no sus valores.

## 10. Configuración de red

También se establecieron los parámetros necesarios para que `pve01` pudiera conectarse a la red y posteriormente ser administrado desde otro equipo.

La documentación pública no necesita mostrar necesariamente los valores reales utilizados.

Cuando se requieran ejemplos se utilizarán datos ficticios o anonimizados.

## 11. Instalación sobre el SSD

Una vez confirmadas las opciones, el instalador escribió Proxmox VE en el SSD interno.

Este fue el punto en el que la Dell dejó definitivamente de utilizar su sistema operativo anterior y pasó a funcionar como nodo dedicado del HomeLab.

```text
Dell E6430
     │
     │ Instalación completada
     ▼
   pve01
Proxmox VE
```

## 12. Finalización y reinicio

Al completar la instalación, el equipo fue reiniciado.

La memoria USB utilizada para la instalación dejó de ser necesaria para el arranque normal.

A partir de este momento, la Dell debía iniciar Proxmox directamente desde su SSD.

## 13. Concepto aprendido: bare metal

Una instalación **bare metal** significa que el hipervisor se instala directamente sobre el hardware físico.

En este caso:

```text
Hardware
   ↓
Proxmox VE
   ↓
VM / Contenedores
```

Esto se diferencia de ejecutar un hipervisor como aplicación dentro de otro sistema operativo.

Por ejemplo:

```text
Hardware
   ↓
Windows
   ↓
VirtualBox
   ↓
Máquina virtual
```

En el HomeLab se eligió la primera alternativa para dedicar la Dell a la virtualización.

## 14. Consideración importante sobre los datos

La instalación de un hipervisor directamente sobre un disco debe considerarse una operación potencialmente destructiva.

Antes de realizarla es importante:

1. identificar el disco correcto;
2. comprobar si contiene información necesaria;
3. realizar un respaldo;
4. verificar el respaldo;
5. confirmar el destino antes de instalar.

Esta práctica fue aplicada previamente durante la Fase 1.

## 15. Verificación inicial

La instalación se consideró completada cuando:

* Proxmox finalizó sin errores críticos;
* la Dell pudo reiniciarse;
* el sistema comenzó a arrancar desde el SSD;
* apareció el entorno de Proxmox;
* el nodo quedó preparado para su configuración y administración.

## 16. Qué aprendí

* Proxmox VE puede instalarse directamente sobre hardware físico.
* Una instalación bare metal sustituye el sistema operativo anterior.
* El disco de destino debe verificarse cuidadosamente.
* Un respaldo previo es fundamental antes de una instalación destructiva.
* El hostname permite identificar un nodo dentro de la infraestructura.
* Las credenciales y parámetros sensibles no deben incluirse en documentación pública.
* Instalar el hipervisor es solo el inicio; todavía es necesario verificar red y acceso administrativo.

## 17. Resultado

* [x] Proxmox VE instalado sobre el SSD.
* [x] Sistema operativo anterior sustituido.
* [x] Dell dedicada al HomeLab.
* [x] Nodo `pve01` definido.
* [x] Configuración inicial introducida.
* [x] Equipo reiniciado desde el SSD.
* [x] Nodo listo para verificación.

## 18. Próximo paso

Comprobar la configuración inicial de `pve01`, validar su conectividad y dejar preparado el acceso administrativo al nodo.

---

**Estado final:** 🟢 Completado
