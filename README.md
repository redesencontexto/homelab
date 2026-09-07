# Redes en Contexto — HomeLab

Bitácora práctica de aprendizaje sobre redes, sistemas, virtualización y ciberseguridad.

Este repositorio documenta la construcción progresiva de un HomeLab desde cero, incluyendo planificación, implementación, problemas encontrados, soluciones y aprendizajes obtenidos durante el proceso.

---

## Objetivo

Construir un laboratorio práctico que permita aprender, experimentar y desarrollar habilidades en:

* Redes
* Linux
* Windows Server
* Virtualización
* Contenedores
* Ciberseguridad
* Firewalls
* Monitoreo
* Automatización
* Administración de infraestructura

El proyecto busca ir más allá de la teoría:

```text
Aprender
   ↓
Implementar
   ↓
Probar
   ↓
Equivocarse
   ↓
Investigar
   ↓
Solucionar
   ↓
Comprender
   ↓
Documentar
```

---

# Ruta del HomeLab

## Ruta del HomeLab

La construcción del laboratorio está organizada en las siguientes fases:

| Fase | Tema                | Estado       |
| ---- | ------------------- | ------------ |
| 0    | Planificación       | ✅ Completada |
| 1    | Preparación física  | ✅ Completada |
| 2    | Proxmox             | ✅ Completada |
| 3    | Primera VM Linux    | ✅ Completada |
| 4    | Backups y snapshots | ✅ Completada |
| 5    | Docker              | ⏭️ Siguiente |
| 6    | Raspberry Pi        | ⬜ Pendiente  |
| 7    | Networking virtual  | ⬜ Pendiente  |
| 8    | Firewall            | ⬜ Pendiente  |
| 9    | Windows Server      | ⬜ Pendiente  |
| 10   | Cyber Range         | ⬜ Pendiente  |
| 11   | Observabilidad      | ⬜ Pendiente  |
| 12   | Automatización      | ⬜ Pendiente  |
| 13   | Redes en Contexto   | ⬜ Pendiente  |

## Estado actual

Actualmente se encuentran completadas:

```text
Fase 0 — Planificación
        ↓
Fase 1 — Preparación física
        ↓
Fase 2 — Proxmox
        ↓
Fase 3 — Primera VM Linux
        ↓
Fase 4 — Backups y snapshots
        ↓
Fase 5 — Docker
             ↑
          SIGUIENTE
```

El HomeLab dispone actualmente de un nodo Proxmox operativo, una primera máquina virtual Ubuntu Server funcional y mecanismos básicos de snapshot, backup y recuperación verificados.


---

# Infraestructura inicial

El HomeLab comenzó reutilizando hardware disponible.

## Nodo principal

**Dell Latitude E6430**

* Intel Core i7-3720QM
* 16 GB RAM
* SSD de 480 GB
* Proxmox VE
* Hostname: `pve01`

La Dell fue reutilizada como nodo principal de virtualización.

Antes de instalar Proxmox se realizó un respaldo de la información existente en el equipo.

Proxmox fue posteriormente instalado directamente sobre el hardware.

## Raspberry Pi

Se dispone también de una Raspberry Pi con almacenamiento de 64 GB.

Su integración se realizará formalmente durante:

**Fase 6 — Raspberry Pi**

## Estación de administración

La administración del HomeLab se realiza desde una computadora independiente utilizada para acceder a Proxmox y posteriormente administrar las máquinas virtuales y servicios.

---

# Organización de la documentación

La documentación se organizará siguiendo exactamente las fases de la ruta oficial.

```text
homelab/
│
├── README.md
│
├── fases/
│   ├── fase-00-planificacion/
│   ├── fase-01-preparacion-fisica/
│   ├── fase-02-proxmox/
│   ├── fase-03-primera-vm-linux/
│   ├── fase-04-backups-snapshots/
│   ├── fase-05-docker/
│   ├── fase-06-raspberry-pi/
│   ├── fase-07-networking-virtual/
│   ├── fase-08-firewall/
│   ├── fase-09-windows-server/
│   ├── fase-10-cyber-range/
│   ├── fase-11-observabilidad/
│   ├── fase-12-automatizacion/
│   └── fase-13-redes-en-contexto/
│
├── imagenes/
├── recursos/
└── plantillas/
```

Las carpetas serán creadas progresivamente conforme se documenten o comiencen las fases correspondientes.

---

# Qué contendrá cada práctica

Cuando corresponda, una entrada podrá incluir:

* Objetivo
* Contexto
* Conceptos previos
* Hardware utilizado
* Software utilizado
* Procedimiento
* Comandos
* Capturas
* Diagramas
* Verificaciones
* Problemas encontrados
* Causas
* Soluciones
* Aprendizajes
* Resultado
* Próximos pasos

No todas las prácticas necesitarán todas las secciones.

---

# Los errores también forman parte del laboratorio

Esta bitácora no pretende mostrar únicamente configuraciones exitosas.

Los errores, pruebas fallidas y problemas encontrados forman parte del proceso de aprendizaje y serán documentados cuando aporten valor técnico.

Una entrada puede incluir:

```text
Problema
   ↓
Síntoma
   ↓
Investigación
   ↓
Causa
   ↓
Solución
   ↓
Aprendizaje
```

---

# Seguridad de la documentación

El repositorio es público, pero la infraestructura del HomeLab no tiene por qué serlo completamente.

Antes de publicar contenido se revisará que no incluya:

* Contraseñas
* Tokens
* Claves privadas
* Credenciales
* IP públicas
* Correos administrativos
* Números de serie
* Información sensible de la infraestructura

Cuando sea necesario se utilizarán valores de ejemplo o información anonimizada.

Las capturas de pantalla también serán revisadas antes de publicarse.

---

# Principios del proyecto

## Aprender antes de automatizar

Primero comprender qué hace una tecnología o configuración.

Después considerar su automatización.

## Entender antes de ampliar

No se incorporarán tecnologías únicamente para aumentar la complejidad del laboratorio.

Cada componente debe tener un objetivo.

## Reutilizar antes de comprar

Primero se aprovechará el hardware disponible.

Las nuevas adquisiciones deberán responder a necesidades identificadas durante el proyecto.

## Documentar mientras se aprende

La documentación forma parte del laboratorio y no será una tarea independiente realizada únicamente al final.

---

# Redes en Contexto

Este HomeLab también funcionará como entorno práctico de **Redes en Contexto**.

La experiencia adquirida podrá convertirse posteriormente en:

* documentación técnica;
* laboratorios;
* artículos;
* tutoriales;
* diagramas;
* contenido educativo.

La integración formal del laboratorio con el proyecto se abordará en:

**Fase 13 — Redes en Contexto**

---

**Estado del proyecto:** 🟡 En desarrollo
