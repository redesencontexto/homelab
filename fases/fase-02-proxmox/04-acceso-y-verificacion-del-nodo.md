# 04 — Acceso y verificación del nodo

**Fase:** Fase 2 — Proxmox
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Acceder a la interfaz web de Proxmox VE desde la computadora de administración y comprobar que el nodo `pve01` estuviera operativo y listo para comenzar a crear máquinas virtuales.

## 2. Contexto

Después de instalar Proxmox VE y validar la configuración inicial de red, el siguiente paso era comprobar que el servidor pudiera administrarse remotamente desde otro equipo de la red local.

Esto permite trabajar con el HomeLab sin depender permanentemente del teclado y la pantalla conectados físicamente a la Dell Latitude E6430.

## 3. Arquitectura de administración

El acceso inicial quedó planteado de la siguiente manera:

```text
PC de administración
        │
        │ Navegador web
        ▼
      pve01
   Proxmox VE
```

La Dell funciona como servidor y la computadora principal como estación de administración.

## 4. Interfaz web de Proxmox

Proxmox VE dispone de una interfaz gráfica accesible desde un navegador web.

Desde esta interfaz se pueden administrar progresivamente elementos como:

* nodos;
* máquinas virtuales;
* contenedores;
* almacenamiento;
* redes;
* usuarios;
* permisos;
* backups;
* snapshots;
* tareas;
* registros.

No todas estas funciones forman parte de la Fase 2.

## 5. Acceso desde el navegador

Desde la computadora de administración se utilizó la dirección de administración configurada para `pve01`.

La interfaz web de Proxmox utiliza normalmente HTTPS y el puerto:

```text
8006
```

Conceptualmente, el acceso tiene la forma:

```text
https://DIRECCION-DE-PVE01:8006
```

En esta bitácora no se publica la dirección real del nodo.

## 6. Advertencia inicial del navegador

Al acceder por primera vez a Proxmox puede aparecer una advertencia relacionada con el certificado HTTPS.

Esto puede ocurrir porque el nodo utiliza inicialmente un certificado que el navegador no reconoce como emitido por una autoridad pública de confianza.

La aparición de esta advertencia en un entorno local no significa automáticamente que Proxmox esté funcionando incorrectamente.

La gestión de certificados podrá estudiarse posteriormente cuando sea relevante para la infraestructura.

## 7. Inicio de sesión

Para acceder a la administración fue necesario utilizar las credenciales configuradas durante la instalación.

Las credenciales reales:

* no se documentan públicamente;
* no deben aparecer en capturas;
* no se almacenan en este repositorio.

Después de autenticarse correctamente fue posible acceder al panel principal de Proxmox VE.

## 8. Elementos observados en la interfaz

La interfaz permitió identificar inicialmente:

* Datacenter;
* nodo `pve01`;
* almacenamiento local;
* información de recursos;
* estado del nodo;
* opciones para crear máquinas virtuales y contenedores.

Esto confirmó que Proxmox reconocía correctamente el nodo instalado.

## 9. Verificación del nodo

Se comprobó que:

* `pve01` apareciera disponible;
* el nodo estuviera activo;
* la interfaz web respondiera;
* la administración desde otro equipo funcionara;
* Proxmox mostrara los recursos del servidor;
* no existiera un problema crítico que impidiera continuar.

## 10. Estado de los recursos

Desde la interfaz de Proxmox se pueden revisar recursos como:

* CPU;
* memoria RAM;
* almacenamiento;
* actividad del nodo;
* interfaces;
* tareas.

Esta información será especialmente útil cuando comiencen a ejecutarse máquinas virtuales.

## 11. Administración remota

Separar servidor y estación de administración permite trabajar de esta forma:

```text
Usuario
   │
   ▼
PC de administración
   │
   ▼
Interfaz web / SSH
   │
   ▼
pve01
   │
   ▼
Máquinas virtuales y servicios
```

Esto representa un cambio importante respecto a utilizar la Dell como computadora convencional.

Ahora el equipo cumple una función de infraestructura.

## 12. Consideración de seguridad

La interfaz administrativa de un hipervisor es un componente sensible.

Se deben evitar prácticas como:

* exponerla directamente a Internet sin necesidad;
* utilizar contraseñas débiles;
* compartir credenciales;
* publicar capturas con información sensible;
* otorgar permisos administrativos innecesarios.

Las configuraciones de seguridad se ampliarán progresivamente durante el desarrollo del HomeLab.

## 13. Qué aprendí

* Proxmox puede administrarse mediante una interfaz web.
* El puerto `8006` se utiliza normalmente para acceder a la interfaz web de Proxmox VE.
* Un servidor no necesita utilizarse directamente desde su pantalla para ser administrado.
* La administración remota permite separar la estación de trabajo de la infraestructura.
* Las advertencias de certificado deben entenderse antes de ignorarse.
* La interfaz de administración de un hipervisor debe protegerse adecuadamente.

## 14. Resultado

* [x] Interfaz web accesible.
* [x] Autenticación realizada correctamente.
* [x] Nodo `pve01` visible.
* [x] Recursos del servidor disponibles.
* [x] Administración remota funcional.
* [x] Nodo preparado para comenzar a crear máquinas virtuales.

## 15. Cierre de la Fase 2

Con Proxmox VE instalado, configurado y accesible desde la computadora de administración, el nodo `pve01` quedó operativo.

```text
Dell Latitude E6430
        │
        ▼
      pve01
   Proxmox VE
        │
        ▼
Nodo operativo
        │
        ▼
FASE 3 — Primera VM Linux
```

La infraestructura de virtualización base está preparada para comenzar a alojar sistemas invitados.

## 16. Próximo paso

Crear la primera máquina virtual Linux del HomeLab, comprender los recursos que deben asignarse y realizar la primera instalación de un sistema invitado sobre Proxmox.

---

**Estado final:** 🟢 Fase 2 completada
