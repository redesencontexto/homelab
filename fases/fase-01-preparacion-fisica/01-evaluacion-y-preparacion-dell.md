# 01 — Evaluación y preparación de la Dell Latitude E6430

**Fase:** Fase 1 — Preparación física
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Evaluar la Dell Latitude E6430 antes de reutilizarla como nodo principal del HomeLab y comprobar que sus características permitieran comenzar el proyecto de virtualización.

## 2. Contexto

Durante la planificación se decidió aprovechar el hardware disponible antes de adquirir nuevos equipos.

La Dell Latitude E6430 fue seleccionada como candidata para convertirse en el primer nodo de virtualización debido a sus recursos de hardware.

Antes de realizar cambios sobre el equipo era necesario revisar:

* capacidades;
* almacenamiento;
* memoria;
* estado general;
* limitaciones;
* información existente que debía conservarse.

## 3. Especificaciones del equipo

| Característica   | Especificación                   |
| ---------------- | -------------------------------- |
| Modelo           | Dell Latitude E6430              |
| Procesador       | Intel Core i7-3720QM             |
| Memoria RAM      | 16 GB                            |
| Almacenamiento   | SSD de 480 GB                    |
| Batería          | No funcional                     |
| Función prevista | Nodo principal de virtualización |

Estas características se consideraron suficientes para comenzar un HomeLab de pequeña escala.

## 4. Función asignada

Se decidió dedicar la Dell principalmente al laboratorio.

La función prevista sería:

```text
Dell Latitude E6430
        │
        ▼
Nodo de virtualización
        │
        ▼
Máquinas virtuales y servicios
```

El equipo dejaría de utilizarse como laptop de propósito general y pasaría a formar parte de la infraestructura del HomeLab.

## 5. Evaluación de recursos

### Procesador

El Intel Core i7-3720QM proporciona múltiples núcleos e hilos de ejecución, permitiendo comenzar a trabajar con varias cargas virtualizadas de tamaño moderado.

### Memoria RAM

Los 16 GB de RAM permiten iniciar el laboratorio, aunque será necesario controlar cuidadosamente la memoria asignada a cada máquina virtual.

No todas las máquinas previstas deberán ejecutarse simultáneamente.

### Almacenamiento

El SSD de 480 GB proporciona espacio suficiente para comenzar con:

* el hipervisor;
* imágenes ISO;
* máquinas virtuales;
* contenedores;
* archivos de laboratorio.

El uso del almacenamiento deberá supervisarse conforme crezca la infraestructura.

## 6. Limitación identificada: batería

La principal limitación física detectada fue la batería.

La batería de la Dell no funciona correctamente, por lo que el equipo depende completamente de la alimentación mediante cargador.

```text
Corriente eléctrica
       │
       ▼
    Cargador
       │
       ▼
Dell E6430
```

Sin alimentación externa:

```text
Pérdida de energía
       ↓
Apagado inmediato
```

## 7. Riesgo para el futuro nodo

Aunque durante esta fase todavía no se había instalado el hipervisor, se identificó que esta condición podría representar un problema una vez que la Dell comenzara a ejecutar servidores.

Un apagado inesperado podría afectar:

* máquinas virtuales;
* sistemas de archivos;
* servicios;
* procesos en ejecución;
* disponibilidad del laboratorio.

## 8. Mitigaciones consideradas

Se identificaron dos mejoras futuras principales:

### Reemplazo de batería

Instalar una batería compatible permitiría que la propia laptop actuara temporalmente como respaldo ante una interrupción eléctrica.

### UPS

Un UPS proporcionaría protección adicional para la infraestructura y permitiría manejar mejor cortes o variaciones de energía.

Estas mejoras no eran requisito para comenzar el laboratorio, pero quedaron registradas como necesidades futuras.

## 9. Decisión final

Después de evaluar el equipo se decidió continuar con la reutilización de la Dell Latitude E6430.

La estrategia sería:

```text
Evaluar hardware
      ↓
Confirmar capacidades
      ↓
Identificar limitaciones
      ↓
Respaldar información
      ↓
Preparar el equipo
      ↓
Instalar plataforma de virtualización
```

El respaldo de la información sería obligatorio antes de modificar el sistema existente.

## 10. Qué aprendí

* Un HomeLab puede comenzar reutilizando hardware existente.
* No es necesario disponer inicialmente de servidores empresariales.
* Antes de reutilizar un equipo se deben evaluar tanto sus capacidades como sus limitaciones.
* La disponibilidad eléctrica es importante cuando un equipo comienza a funcionar como servidor.
* La memoria y el almacenamiento deben considerarse al planificar máquinas virtuales.
* Antes de realizar una instalación destructiva debe protegerse la información existente.

## 11. Resultado

* [x] Dell Latitude E6430 evaluada.
* [x] Características principales documentadas.
* [x] Equipo considerado adecuado para comenzar.
* [x] Función dentro del HomeLab definida.
* [x] Limitación de batería identificada.
* [x] Riesgo eléctrico registrado.
* [x] Necesidad de respaldo establecida.

## 12. Próximo paso

Respaldar los archivos necesarios antes de realizar cualquier cambio que pudiera eliminar el sistema operativo y la información existente en el SSD.

---

**Estado final:** 🟢 Completado
