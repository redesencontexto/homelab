# 04 — Ruta y criterios de crecimiento

**Fase:** Fase 0 — Planificación
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Definir la ruta oficial de crecimiento del HomeLab y establecer los criterios que guiarán la incorporación de nuevas tecnologías, equipos y servicios.

## 2. Ruta oficial del HomeLab

La evolución del proyecto se organizará en las siguientes fases:

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

Esta ruta funcionará como referencia principal tanto para la implementación como para la documentación.

## 3. Criterio de avance

No se avanzará de fase únicamente por completar una instalación.

Antes de considerar una fase terminada se buscará comprobar que:

* el objetivo fue alcanzado;
* la configuración funciona;
* los conceptos principales fueron comprendidos;
* los problemas relevantes fueron documentados;
* la infraestructura quedó suficientemente estable para continuar;
* la siguiente fase tiene sentido sobre la base construida.

## 4. Crecimiento progresivo

El HomeLab crecerá de forma incremental.

```text
Base sencilla
    ↓
Validación
    ↓
Nueva necesidad
    ↓
Nueva tecnología
    ↓
Prueba
    ↓
Documentación
    ↓
Expansión
```

Esto permite reducir cambios innecesarios y comprender mejor el efecto de cada nuevo componente.

## 5. Reutilización antes de adquisición

Se establece como criterio general aprovechar primero los recursos disponibles.

Una nueva compra deberá responder a al menos una de estas razones:

* existe una limitación real del hardware actual;
* mejora la seguridad;
* mejora la disponibilidad;
* permite desarrollar una fase que no puede realizarse con los recursos existentes;
* aporta una capacidad práctica importante para el aprendizaje.

## 6. Separación por fases

Cada tema deberá documentarse dentro de la fase que le corresponde.

Ejemplos:

| Actividad                                   | Fase   |
| ------------------------------------------- | ------ |
| Evaluar la Dell E6430                       | Fase 0 |
| Respaldar información antes de reutilizarla | Fase 1 |
| Preparar físicamente el equipo              | Fase 1 |
| Instalar Proxmox                            | Fase 2 |
| Crear la primera VM Linux                   | Fase 3 |
| Configurar snapshots                        | Fase 4 |
| Implementar Docker                          | Fase 5 |
| Integrar la Raspberry Pi                    | Fase 6 |
| Trabajar VLAN y redes virtuales             | Fase 7 |
| Implementar firewall                        | Fase 8 |

Esta separación busca evitar mezclar planificación, preparación e implementación.

## 7. Criterios técnicos

### Comprender antes de automatizar

La automatización se incorporará después de comprender manualmente los procesos que se desean automatizar.

### Validar antes de ampliar

Una nueva capa de complejidad no debe añadirse sobre una base que todavía presenta problemas importantes.

### Documentar cambios relevantes

Las decisiones, configuraciones y problemas que aporten valor al aprendizaje deberán quedar registrados.

### Mantener capacidad de recuperación

A medida que el laboratorio crezca se incorporarán mecanismos para reducir el impacto de errores o fallos, incluyendo:

* snapshots;
* backups;
* recuperación;
* documentación de configuraciones.

### Seguridad progresiva

La seguridad no será una actividad única ubicada exclusivamente en una fase.

Aunque existan fases específicas para firewall y Cyber Range, se aplicarán criterios de seguridad durante todo el proyecto.

## 8. Criterios de documentación

La bitácora deberá diferenciar claramente entre:

### Planificado

Algo decidido pero todavía no implementado.

### Implementado

Algo que realmente fue configurado o instalado.

### Verificado

Algo cuya operación fue comprobada.

### Pendiente

Algo que todavía no se ha realizado.

Esta distinción evitará presentar planes futuros como si ya formaran parte de la infraestructura real.

## 9. Control de información sensible

Antes de publicar cualquier entrada se realizará una revisión para comprobar que no aparezcan:

* contraseñas;
* tokens;
* claves privadas;
* IP públicas;
* credenciales;
* datos personales;
* identificadores sensibles;
* información innecesaria sobre la infraestructura.

Cuando sea necesario se utilizarán valores de ejemplo.

## 10. Criterio para cerrar una fase

Una fase podrá marcarse como completada cuando:

* [x] Se haya realizado la actividad principal.
* [x] El resultado haya sido validado.
* [x] Las limitaciones relevantes estén identificadas.
* [x] Los problemas importantes estén documentados.
* [x] La documentación correspondiente esté actualizada.
* [x] Exista una base clara para comenzar la fase siguiente.

## 11. Resultado de la Fase 0

La Fase 0 permitió definir:

* el propósito del HomeLab;
* su alcance inicial;
* los recursos disponibles;
* las limitaciones conocidas;
* la arquitectura conceptual;
* la ruta oficial de implementación;
* los criterios de crecimiento;
* los principios de documentación.

Con esto queda completada la etapa de planificación.

## 12. Próxima fase

**Fase 1 — Preparación física**

Esta fase documentará las acciones realizadas sobre el hardware antes de instalar Proxmox, incluyendo la preparación de la Dell Latitude E6430 y el respaldo de la información necesaria.

---

**Estado final:** 🟢 Fase 0 completada
