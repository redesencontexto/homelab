# 02 — Inventario y limitaciones iniciales

**Fase:** Fase 0 — Planificación
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Identificar el hardware disponible al inicio del proyecto, conocer sus capacidades y registrar las principales limitaciones que deben considerarse antes de comenzar la implementación del HomeLab.

## 2. Contexto

Antes de comprar nuevos equipos o instalar plataformas, se decidió revisar qué recursos ya estaban disponibles.

El objetivo fue determinar cuánto del laboratorio podía comenzar a construirse reutilizando hardware existente.

Durante esta etapa todavía no se realizaron instalaciones ni modificaciones importantes sobre los equipos.

## 3. Hardware disponible

### Dell Latitude E6430

| Característica | Especificación                |
| -------------- | ----------------------------- |
| Modelo         | Dell Latitude E6430           |
| Procesador     | Intel Core i7-3720QM          |
| Memoria RAM    | 16 GB                         |
| Almacenamiento | SSD de 480 GB                 |
| Batería        | No funcional                  |
| Estado general | Disponible para reutilización |

Por sus características, la Dell Latitude E6430 fue identificada como el equipo con mayor potencial para convertirse en el primer nodo de virtualización del HomeLab.

Durante esta fase únicamente se tomó la decisión de reutilizarla.

La preparación del equipo se documenta posteriormente en la **Fase 1 — Preparación física**.

### Raspberry Pi

| Característica | Información  |
| -------------- | ------------ |
| Equipo         | Raspberry Pi |
| Almacenamiento | 64 GB        |
| Estado         | Disponible   |
| Función        | Por definir  |

La Raspberry Pi se identificó como un recurso adicional que podría utilizarse para servicios independientes o tareas específicas.

Se decidió no incorporarla inmediatamente.

Su implementación se reservó para la **Fase 6 — Raspberry Pi**.

### Computadora de administración

También se dispone de una computadora principal desde la cual se administrará progresivamente el HomeLab.

Su función prevista incluye:

* acceso a interfaces de administración;
* conexiones SSH;
* documentación;
* gestión de archivos;
* administración de servidores y servicios;
* acceso remoto a los componentes del laboratorio.

No se contempla inicialmente utilizarla como servidor permanente del HomeLab.

## 4. Recursos de red

El proyecto comienza utilizando la infraestructura de red existente.

En esta etapa todavía no se dispone de todos los componentes considerados para la arquitectura futura, como:

* switch administrable;
* segmentación mediante VLAN;
* firewall dedicado;
* rack;
* patch panel;
* protección eléctrica centralizada.

La ausencia de estos componentes no impide iniciar las primeras fases.

## 5. Limitaciones identificadas

### 5.1 Batería de la Dell Latitude E6430

La batería del equipo no funciona.

La laptop depende completamente del cargador para permanecer encendida.

Esto significa que una pérdida de energía podría provocar un apagado inmediato.

#### Riesgos futuros

Si el equipo se utiliza como servidor, un apagado abrupto podría afectar:

* máquinas virtuales;
* servicios;
* procesos en ejecución;
* datos no guardados;
* disponibilidad del laboratorio.

#### Mejora prevista

Se considera posteriormente:

* reemplazar la batería;
* incorporar un UPS;
* mejorar la protección eléctrica del HomeLab.

### 5.2 Memoria RAM disponible

La Dell dispone de 16 GB de RAM.

Es suficiente para comenzar, pero será necesario distribuir los recursos cuidadosamente cuando se creen múltiples máquinas virtuales o servicios.

### 5.3 Hardware reutilizado

El laboratorio comienza principalmente con equipos que no fueron adquiridos específicamente para funcionar como servidores.

Esto implica aceptar ciertas limitaciones de:

* capacidad;
* consumo;
* disponibilidad;
* expansión;
* redundancia.

Estas limitaciones también forman parte del aprendizaje.

### 5.4 Infraestructura de red incompleta

Todavía no se dispone de la arquitectura de red definitiva.

Esto significa que inicialmente se trabajará con una topología sencilla y posteriormente se incorporarán componentes especializados.

## 6. Equipamiento considerado para el futuro

Durante la planificación se identificaron posibles adquisiciones:

* batería compatible para la Dell Latitude E6430;
* UPS;
* switch administrable;
* rack de 10 pulgadas;
* patch panel;
* PDU;
* bandejas para equipos;
* cableado y accesorios;
* almacenamiento adicional si fuera necesario.

Estos elementos se consideran **planificados**, no adquiridos.

La compra se realizará únicamente cuando exista una necesidad concreta dentro del proyecto.

## 7. Criterio de reutilización

Se adoptó el siguiente principio:

```text
Inventariar
    ↓
Evaluar capacidades
    ↓
Reutilizar
    ↓
Implementar
    ↓
Detectar limitaciones reales
    ↓
Comprar solo cuando sea necesario
```

Esto permite construir el laboratorio progresivamente sin depender de tener toda la infraestructura desde el inicio.

## 8. Resumen del inventario inicial

| Recurso              | Función prevista          | Estado inicial |
| -------------------- | ------------------------- | -------------- |
| Dell Latitude E6430  | Nodo de virtualización    | Disponible     |
| Raspberry Pi         | Nodo/servicios auxiliares | Disponible     |
| PC principal         | Administración            | Disponible     |
| Red existente        | Conectividad inicial      | Disponible     |
| Switch administrable | Networking futuro         | Pendiente      |
| UPS                  | Protección eléctrica      | Pendiente      |
| Rack 10"             | Organización física       | Pendiente      |

## 9. Resultado

* [x] Hardware disponible identificado.
* [x] Capacidades principales registradas.
* [x] Limitaciones iniciales documentadas.
* [x] Riesgo eléctrico identificado.
* [x] Recursos disponibles separados de futuras adquisiciones.
* [x] Dell identificada como candidata principal para virtualización.

## 10. Próximo paso

Definir la arquitectura conceptual inicial del HomeLab y asignar una función prevista a cada uno de los equipos disponibles.

---

**Estado final:** 🟢 Completado
