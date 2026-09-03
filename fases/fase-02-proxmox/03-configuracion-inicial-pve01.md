# 03 — Configuración inicial de `pve01`

**Fase:** Fase 2 — Proxmox
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Verificar y documentar la configuración inicial del nodo `pve01` después de instalar Proxmox VE, asegurando que el equipo pudiera identificarse correctamente y comunicarse con la red local.

## 2. Contexto

Después de instalar Proxmox VE directamente sobre el SSD de la Dell Latitude E6430, el equipo pasó a funcionar como nodo de virtualización del HomeLab.

El siguiente paso consistía en confirmar que la configuración básica del sistema fuera coherente y que `pve01` pudiera ser administrado desde otro equipo.

## 3. Identidad del nodo

El servidor fue configurado con el hostname:

```text
pve01
```

Este nombre identifica el nodo dentro de la infraestructura del HomeLab.

La convención permite una posible expansión futura:

```text
pve01
pve02
pve03
```

Actualmente solo existe `pve01`.

## 4. Función de `pve01`

`pve01` funciona como:

* nodo principal de virtualización;
* host de futuras máquinas virtuales;
* host de futuros contenedores;
* base inicial de la infraestructura virtual del HomeLab.

Conceptualmente:

```text
Dell Latitude E6430
        │
        ▼
      pve01
   Proxmox VE
        │
   ┌────┴────┐
   │         │
   ▼         ▼
  VM        LXC
```

## 5. Configuración de red

Durante la instalación se definieron los parámetros necesarios para que `pve01` pudiera comunicarse con la red local.

Una configuración de red de administración requiere normalmente elementos como:

* dirección IP;
* máscara o prefijo de red;
* puerta de enlace;
* servidor DNS;
* interfaz física;
* bridge utilizado por Proxmox.

Los valores reales no se publican en esta bitácora.

## 6. Importancia de una dirección estable

Un servidor debe poder encontrarse de forma predecible dentro de la red.

Si la dirección cambia constantemente, la administración puede resultar más difícil.

Conceptualmente:

```text
PC de administración
        │
        ▼
Dirección conocida de pve01
        │
        ▼
Interfaz de administración
```

Por ello, la configuración de red del nodo debe mantenerse controlada y documentada internamente.

## 7. Bridge de Proxmox

Proxmox utiliza bridges de red para conectar el host y las futuras máquinas virtuales con la infraestructura de red.

El bridge principal suele aparecer con un nombre como:

```text
vmbr0
```

Conceptualmente:

```text
Red física
    │
    ▼
Interfaz física
    │
    ▼
  vmbr0
    │
    ├── pve01
    ├── VM Linux
    ├── VM Windows
    └── otras VM futuras
```

En esta fase solo se valida la configuración base.

El estudio detallado de bridges, VLAN y redes virtuales corresponde a la:

**Fase 7 — Networking virtual**

## 8. Verificaciones básicas

Después del reinicio se comprobó que:

* Proxmox iniciara correctamente;
* el hostname fuera `pve01`;
* el nodo tuviera conectividad;
* la interfaz de red estuviera activa;
* el equipo pudiera ser alcanzado desde la red local;
* la información de acceso administrativo estuviera disponible.

## 9. Comandos útiles de verificación

Algunos comandos que pueden utilizarse en un sistema Linux para revisar la configuración son:

```bash
hostname
```

Muestra el nombre del equipo.

```bash
ip addr
```

Muestra las interfaces y direcciones configuradas.

```bash
ip route
```

Muestra la tabla de rutas.

```bash
ping DIRECCION
```

Permite comprobar conectividad con otro equipo o destino.

En una documentación pública se recomienda sustituir direcciones reales por valores de ejemplo.

## 10. Seguridad de la configuración

No deben publicarse innecesariamente:

* contraseñas;
* dirección IP pública;
* credenciales;
* correos administrativos;
* claves privadas;
* información que permita acceder al nodo.

Las capturas deben revisarse antes de ser añadidas al repositorio.

## 11. Limitación eléctrica pendiente

La batería de la Dell continúa sin funcionar.

Por tanto, `pve01` sigue dependiendo completamente de la corriente eléctrica.

Este riesgo permanece abierto y deberá mitigarse en el futuro mediante:

* reemplazo de batería;
* UPS;
* estrategia de apagado controlado.

## 12. Qué aprendí

* El hostname identifica un servidor dentro de la infraestructura.
* Un nodo de virtualización necesita conectividad estable para administrarse.
* Proxmox utiliza bridges para conectar redes físicas y virtuales.
* `vmbr0` será importante cuando comiencen a crearse máquinas virtuales.
* La configuración de red real no necesita exponerse para documentar el aprendizaje.
* Un servidor operativo puede seguir teniendo riesgos físicos pendientes.

## 13. Resultado

* [x] Hostname `pve01` verificado.
* [x] Nodo iniciado correctamente.
* [x] Conectividad inicial validada.
* [x] Configuración de red base disponible.
* [x] Nodo preparado para administración remota.
* [x] Información sensible excluida de la documentación pública.

## 14. Próximo paso

Acceder a la interfaz web de Proxmox desde la computadora de administración y comprobar que el nodo `pve01` pueda administrarse correctamente.

---

**Estado final:** 🟢 Completado
