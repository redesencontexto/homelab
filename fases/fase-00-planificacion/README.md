# Fase 0 — Planificación

**Estado:** ✅ Completada
**Documentación:** Retrospectiva

## Objetivo

Definir el propósito, alcance y diseño inicial del HomeLab antes de realizar cambios físicos en los equipos o instalar plataformas y servicios.

Esta fase responde principalmente a las preguntas:

* ¿Para qué se construirá el HomeLab?
* ¿Qué quiero aprender con él?
* ¿Qué equipos tengo disponibles?
* ¿Qué limitaciones existen?
* ¿Qué función podría cumplir cada equipo?
* ¿Cómo debería crecer el laboratorio?
* ¿Qué componentes será necesario incorporar progresivamente?

## Punto de partida

El proyecto parte del objetivo de construir un laboratorio propio para desarrollar conocimientos prácticos en:

* Linux
* Redes
* Ciberseguridad
* Virtualización

La intención es aprender mediante implementación real y no únicamente mediante teoría.

También se busca aprovechar inicialmente el hardware ya disponible antes de realizar nuevas adquisiciones.

## Hardware considerado durante la planificación

Durante esta fase se identificaron como recursos disponibles:

### Dell Latitude E6430

* Intel Core i7-3720QM
* 16 GB de RAM
* SSD de 480 GB
* Batería no funcional

Se consideró como equipo principal para comenzar la infraestructura de virtualización.

> En esta fase solamente se documenta la decisión de utilizar el equipo. Su preparación física corresponde a la Fase 1 y la instalación de Proxmox corresponde a la Fase 2.

### Raspberry Pi

* Almacenamiento de 64 GB
* Disponible para futuras funciones dentro del laboratorio

Su implementación se reservó para una fase específica posterior.

### Computadora de administración

Se contempla una computadora independiente para acceder, administrar y documentar la infraestructura del HomeLab.

## Limitaciones identificadas

Durante la planificación se detectaron varias limitaciones iniciales.

### Energía

La batería de la Dell Latitude E6430 no funciona.

Esto supone un riesgo ante interrupciones eléctricas y crea la necesidad futura de mejorar la protección eléctrica del nodo.

### Recursos

El laboratorio comenzará utilizando hardware reutilizado, por lo que será necesario administrar cuidadosamente los recursos disponibles.

### Infraestructura de red

La infraestructura definitiva de switching, segmentación, rack y protección eléctrica todavía no está completamente disponible.

Esto no impide comenzar el laboratorio.

## Criterios de diseño

### Reutilizar antes de comprar

Se utilizará primero el hardware disponible.

Las nuevas adquisiciones deben responder a necesidades reales identificadas durante el desarrollo del laboratorio.

### Crecer progresivamente

La infraestructura no se construirá completa desde el primer día.

Cada nueva tecnología será incorporada dentro de una fase determinada.

### Comprender antes de complicar

No se añadirán servicios o tecnologías únicamente para hacer el laboratorio más grande.

Cada componente debe cumplir un objetivo técnico o educativo.

### Seguridad desde el diseño

El laboratorio será utilizado para prácticas de redes y ciberseguridad, por lo que la segmentación, el control de acceso y la protección de la infraestructura se incorporarán progresivamente.

### Documentar el aprendizaje

Las implementaciones, problemas y soluciones serán registrados como parte del proyecto.

## Ruta definida

La planificación dio como resultado la siguiente ruta de trabajo:

| Fase | Tema                |
| ---- | ------------------- |
| 0    | Planificación       |
| 1    | Preparación física  |
| 2    | Proxmox             |
| 3    | Primera VM Linux    |
| 4    | Backups y snapshots |
| 5    | Docker              |
| 6    | Raspberry Pi        |
| 7    | Networking virtual  |
| 8    | Firewall            |
| 9    | Windows Server      |
| 10   | Cyber Range         |
| 11   | Observabilidad      |
| 12   | Automatización      |
| 13   | Redes en Contexto   |

Esta ruta funciona como estructura oficial del HomeLab y de su documentación.

## Entradas de la bitácora

| Entrada | Tema                                | Estado           |
| ------- | ----------------------------------- | ---------------- |
| 01      | Objetivos y alcance                 | ⬜ Por documentar |
| 02      | Inventario y limitaciones iniciales | ⬜ Por documentar |
| 03      | Arquitectura planificada            | ⬜ Por documentar |
| 04      | Ruta y criterios de crecimiento     | ⬜ Por documentar |

## Resultado esperado

Al completar la planificación se debe disponer de:

* objetivos definidos;
* alcance inicial establecido;
* hardware identificado;
* limitaciones conocidas;
* función prevista para los principales equipos;
* arquitectura inicial conceptual;
* ruta de implementación definida.

## Resultado obtenido

Se definió una ruta progresiva de 14 fases y se determinó que el HomeLab comenzaría utilizando principalmente los recursos ya disponibles.

La implementación física y técnica quedó reservada para las fases siguientes.

## Próxima fase

**Fase 1 — Preparación física**
