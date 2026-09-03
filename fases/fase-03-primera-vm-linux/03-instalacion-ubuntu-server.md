# 03 — Instalación de Ubuntu Server

**Fase:** Fase 3 — Primera VM Linux
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Instalar Ubuntu Server 26.04.1 LTS dentro de la primera máquina virtual creada en Proxmox.

## 2. Contexto

En el paso anterior se creó la primera VM del HomeLab y se asoció la imagen:

```text
ubuntu-26.04.1-live-server-amd64.iso
```

La máquina virtual ya disponía de:

* CPU virtual;
* memoria RAM;
* disco virtual;
* interfaz de red virtual;
* medio de instalación.

El siguiente paso consistía en iniciar la VM e instalar el sistema operativo invitado.

## 3. Inicio de la máquina virtual

Desde la interfaz web de Proxmox se inició la máquina virtual.

La VM arrancó utilizando la imagen ISO de Ubuntu Server como medio de instalación.

El flujo fue:

```text
Proxmox
   ↓
Iniciar VM
   ↓
Arranque desde ISO
   ↓
Instalador Ubuntu Server
```

## 4. Acceso a la consola

La instalación se realizó utilizando la consola de la máquina virtual desde Proxmox.

La consola permite interactuar con la VM aunque todavía no disponga de acceso remoto por red.

Esto es especialmente importante durante la instalación inicial de un sistema operativo.

## 5. Instalador de Ubuntu Server

Ubuntu Server utiliza un instalador principalmente orientado al teclado.

Durante el proceso fue necesario desplazarse utilizando teclas como:

* flechas;
* `Tab`;
* `Shift + Tab`;
* `Enter`;
* barra espaciadora cuando correspondía.

Esta experiencia permitió familiarizarse con una interfaz diferente a los instaladores gráficos tradicionales.

## 6. Selección de idioma

Durante el instalador se seleccionó el idioma correspondiente para continuar con la instalación.

La selección del idioma afecta principalmente la experiencia durante el proceso de instalación y determinadas configuraciones regionales.

## 7. Configuración del teclado

También se revisó la distribución del teclado.

Esta configuración es importante porque una distribución incorrecta puede provocar que símbolos y caracteres especiales no coincidan con las teclas físicas utilizadas.

Esto resulta especialmente relevante al escribir:

* contraseñas;
* comandos;
* símbolos;
* direcciones;
* caracteres especiales.

## 8. Configuración de red

Durante la instalación se llegó a la sección de configuración de red.

La VM dispone de una interfaz de red virtual proporcionada por Proxmox.

Conceptualmente:

```text
Ubuntu Server
      │
      ▼
Interfaz virtual
      │
      ▼
    vmbr0
      │
      ▼
Red del HomeLab
```

Durante esta parte se trabajó con los parámetros necesarios para configurar correctamente la conectividad del servidor.

Entre ellos:

* dirección IP;
* prefijo de red;
* gateway;
* DNS.

Los valores reales utilizados no se publican en este repositorio.

## 9. Configuración estática

Para un servidor resulta útil disponer de una dirección conocida y predecible.

Por ello se trabajó con configuración estática en lugar de depender exclusivamente de una dirección asignada dinámicamente.

Ejemplo documental:

```text
Dirección: 192.168.10.20
Prefijo:   /24
Gateway:   192.168.10.1
DNS:       1.1.1.1
```

Estos valores son únicamente de ejemplo y no representan necesariamente la red real del HomeLab.

## 10. Configuración del almacenamiento

El instalador detectó el disco virtual creado previamente en Proxmox.

Desde la perspectiva de Ubuntu, ese disco aparece como si fuera almacenamiento físico propio.

Sin embargo, realmente existe sobre el almacenamiento de `pve01`.

```text
SSD físico de pve01
        ↓
     Proxmox
        ↓
   Disco virtual
        ↓
 Ubuntu Server
```

Durante la instalación se utilizó este disco virtual como destino del sistema operativo.

## 11. Perfil del servidor

El instalador solicitó información para crear el perfil inicial del sistema.

Esto incluye elementos como:

* nombre del servidor;
* nombre de usuario;
* contraseña.

Los valores sensibles utilizados realmente no se documentan públicamente.

La contraseña nunca debe incluirse en:

* GitHub;
* capturas;
* documentación;
* archivos de configuración públicos.

## 12. Nombre del servidor

El hostname permite identificar el servidor Linux dentro del entorno.

Este nombre es distinto de:

```text
pve01
```

porque `pve01` identifica al host Proxmox.

La VM Ubuntu constituye otro sistema independiente.

Conceptualmente:

```text
pve01
│
└── VM Linux
    └── hostname propio
```

Esto introduce una diferencia importante entre:

* nombre del hipervisor;
* nombre de una máquina virtual;
* nombre del sistema operativo invitado.

## 13. Instalación de OpenSSH

Durante la instalación de un servidor Linux puede habilitarse OpenSSH para permitir administración remota posteriormente.

SSH permitirá trabajar desde otra computadora utilizando una terminal, sin depender de la consola gráfica de Proxmox.

Conceptualmente:

```text
PC de administración
        │
        │ SSH
        ▼
Ubuntu Server VM
```

La configuración y verificación del acceso remoto se documentará dentro de la configuración inicial del servidor.

## 14. Instalación del sistema

Una vez completadas las opciones necesarias, Ubuntu comenzó a instalarse en el disco virtual.

Durante este proceso se copiaron y configuraron los componentes necesarios del sistema.

La VM pasó progresivamente de:

```text
VM vacía
   ↓
ISO de instalación
```

a:

```text
VM
 ↓
Ubuntu Server instalado
```

## 15. Finalización

Al terminar la instalación fue necesario reiniciar la máquina virtual.

Después del reinicio, Ubuntu debía arrancar desde el disco virtual en lugar de volver a iniciar permanentemente desde la ISO.

## 16. Diferencia entre ISO y sistema instalado

Antes:

```text
ISO
 ↓
Instalador
 ↓
Disco virtual vacío
```

Después:

```text
Disco virtual
 ↓
Ubuntu Server
 ↓
Sistema operativo funcional
```

La ISO funciona como medio de instalación, no como ubicación permanente del sistema operativo.

## 17. Verificación

La instalación se consideró correcta cuando:

* Ubuntu finalizó el proceso de instalación;
* la VM pudo reiniciarse;
* el sistema arrancó desde el disco virtual;
* apareció la pantalla de inicio de sesión;
* fue posible utilizar las credenciales creadas.

## 18. Qué aprendí

* Una VM puede instalar un sistema operativo utilizando una ISO virtual.
* La consola de Proxmox permite administrar una VM incluso antes de tener acceso por red.
* Ubuntu Server utiliza una interfaz de instalación principalmente basada en teclado.
* El sistema operativo se instala sobre un disco virtual, no directamente en el SSD físico.
* El host Proxmox y la VM Linux son sistemas distintos.
* Cada VM puede disponer de su propio hostname, usuarios y configuración de red.
* La ISO deja de ser el elemento principal una vez instalado el sistema operativo.

## 19. Resultado

* [x] VM iniciada.
* [x] Instalador de Ubuntu Server cargado.
* [x] Idioma configurado.
* [x] Teclado configurado.
* [x] Red configurada.
* [x] Disco virtual seleccionado.
* [x] Perfil inicial creado.
* [x] Ubuntu Server instalado.
* [x] VM reiniciada.
* [x] Sistema preparado para configuración inicial.

## 20. Próximo paso

Verificar la configuración inicial del servidor Ubuntu, comprobar su red y confirmar que la VM pueda comunicarse correctamente dentro del HomeLab.

---

**Estado final:** 🟢 Completado
