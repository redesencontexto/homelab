# 03 — Arquitectura planificada

**Fase:** Fase 0 — Planificación
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Definir una arquitectura conceptual inicial para el HomeLab utilizando los recursos disponibles y dejando espacio para incorporar progresivamente nuevas tecnologías.

En esta etapa se describe **cómo se planeó utilizar la infraestructura**, no su implementación final.

## 2. Principio de diseño

La arquitectura inicial debía cumplir varios criterios:

* aprovechar el hardware disponible;
* mantener una estructura sencilla;
* permitir virtualización;
* facilitar futuras ampliaciones;
* permitir practicar redes y ciberseguridad;
* evitar incorporar complejidad innecesaria desde el principio.

La intención fue comenzar con una infraestructura pequeña pero escalable.

## 3. Arquitectura conceptual inicial

Durante la planificación se planteó una arquitectura similar a la siguiente:

```text
                         Internet
                            │
                            ▼
                     Router / red local
                            │
              ┌─────────────┼─────────────┐
              │             │             │
              ▼             ▼             ▼
      PC de administración  │       Raspberry Pi
                            │
                            ▼
                  Dell Latitude E6430
                  Nodo de virtualización
                            │
                      ┌─────┴─────┐
                      │           │
                      ▼           ▼
                     VM       Contenedores
```

Esta arquitectura representa únicamente el diseño inicial.

Las funciones específicas se incorporarían progresivamente según las fases del proyecto.

## 4. Dell Latitude E6430

Durante la planificación se decidió utilizar la Dell Latitude E6430 como equipo principal para virtualización.

Su función prevista sería:

```text
Dell Latitude E6430
        │
        ▼
Plataforma de virtualización
        │
   ┌────┴────┐
   │         │
   ▼         ▼
Máquinas   Contenedores
virtuales
```

Esto permitiría ejecutar múltiples sistemas y servicios sin necesitar un equipo físico independiente para cada uno.

La instalación concreta de la plataforma de virtualización corresponde a una fase posterior.

## 5. PC de administración

La computadora principal se mantendría separada de los servidores del HomeLab.

Su función prevista sería servir como estación de administración.

Desde ella se realizarían tareas como:

* acceso a interfaces web;
* conexiones SSH;
* administración remota;
* documentación;
* preparación de archivos;
* configuración de máquinas virtuales;
* supervisión de servicios.

Esta separación permite diferenciar entre:

```text
Equipo desde el que administro
            │
            ▼
Infraestructura que estoy administrando
```

## 6. Raspberry Pi

La Raspberry Pi se mantendría inicialmente como dispositivo físico independiente.

No se decidió asignarle desde la Fase 0 un servicio definitivo.

La intención fue reservarla para una etapa posterior donde pudiera cumplir funciones como:

* servicios ligeros;
* monitoreo;
* automatización;
* DNS;
* herramientas auxiliares;
* servicios independientes del nodo principal.

Su implementación formal se reservó para la **Fase 6 — Raspberry Pi**.

## 7. Evolución de la red

La red inicial se mantendría sencilla.

Posteriormente se prevé evolucionar hacia una arquitectura con mayor segmentación:

```text
                         Internet
                            │
                            ▼
                     Router / Firewall
                            │
                            ▼
                  Switch administrable
                            │
         ┌──────────────────┼──────────────────┐
         │                  │                  │
         ▼                  ▼                  ▼
 Administración         Servidores        Laboratorios
         │                  │                  │
         └──────────── VLAN / segmentación ────┘
```

Esta evolución permitirá posteriormente practicar:

* VLAN;
* routing;
* firewalls;
* aislamiento;
* políticas de acceso;
* troubleshooting;
* análisis de tráfico.

Estas implementaciones no forman parte de la Fase 0.

## 8. Virtualización como núcleo inicial

La virtualización fue identificada como una pieza central del diseño.

En lugar de disponer de múltiples equipos físicos para cada servidor, se plantea utilizar un nodo capaz de alojar diferentes sistemas:

```text
Nodo físico
    │
    ▼
Hipervisor
    │
    ├── Linux Server
    ├── Windows Server
    ├── Firewall virtual
    ├── Docker
    ├── Servicios de red
    └── Laboratorios de seguridad
```

No todos estos sistemas se ejecutarían al mismo tiempo ni serían implementados inmediatamente.

Su incorporación dependería de las siguientes fases.

## 9. Separación por funciones

La arquitectura planificada busca separar progresivamente diferentes funciones.

Ejemplo conceptual:

```text
Administración
     │
     ├── Gestión del laboratorio
     │
Servidores
     │
     ├── Linux
     ├── Windows
     └── Servicios
     │
Seguridad
     │
     ├── Firewall
     ├── Monitoreo
     └── Cyber Range
```

Esta separación permitirá comprender mejor la función de cada componente.

## 10. Arquitectura física vs. arquitectura lógica

### Arquitectura física

Representa los dispositivos reales:

```text
PC
Dell Latitude E6430
Raspberry Pi
Router
Switch futuro
UPS futuro
```

### Arquitectura lógica

Representa los servicios y funciones que pueden existir sobre esos dispositivos:

```text
Hipervisor
Máquinas virtuales
Contenedores
Firewall
DNS
Windows Server
Docker
Monitoreo
Cyber Range
```

Un único dispositivo físico puede alojar múltiples componentes lógicos.

Comprender esta diferencia será importante en las fases posteriores.

## 11. Crecimiento previsto

La arquitectura fue pensada para evolucionar de forma gradual.

```text
Infraestructura básica
        ↓
Virtualización
        ↓
Servidor Linux
        ↓
Backups
        ↓
Contenedores
        ↓
Raspberry Pi
        ↓
Networking virtual
        ↓
Firewall
        ↓
Windows Server
        ↓
Cyber Range
        ↓
Observabilidad
        ↓
Automatización
```

Cada ampliación deberá realizarse únicamente después de comprender y validar la etapa anterior.

## 12. Consideraciones de seguridad

Desde la planificación se establece que el HomeLab no debe tratarse como una infraestructura aislada de las buenas prácticas de seguridad.

La evolución del diseño deberá considerar progresivamente:

* segmentación;
* mínimos privilegios;
* administración segura;
* copias de seguridad;
* monitoreo;
* actualización de sistemas;
* reducción de exposición innecesaria;
* separación de laboratorios ofensivos del resto de la red.

## 13. Resultado

* [x] Arquitectura conceptual definida.
* [x] Nodo de virtualización previsto.
* [x] Estación de administración separada.
* [x] Raspberry Pi reservada para una fase posterior.
* [x] Evolución de networking contemplada.
* [x] Virtualización establecida como núcleo inicial.
* [x] Diferencia entre arquitectura física y lógica identificada.

## 14. Próximo paso

Definir la ruta completa de implementación y los criterios que determinarán cómo crecerá el HomeLab a medida que aparezcan nuevas necesidades.

---

**Estado final:** 🟢 Completado
