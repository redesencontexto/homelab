# 05 — Prueba de restauración del backup

**Fase:** Fase 4 — Backups y snapshots
**Estado:** 🟢 Completado
**Documentación:** Retrospectiva

---

## 1. Objetivo

Comprobar que el backup de `ubuntu-server-01` pudiera utilizarse realmente para recuperar una máquina virtual funcional.

La prueba se realizó creando una VM independiente para no modificar ni sustituir la máquina original.

## 2. Contexto

En la entrada anterior se generó un backup de:

```text
ubuntu-server-01
```

Sin embargo, disponer de una copia no era suficiente para considerar validada la estrategia de respaldo.

Era necesario comprobar:

```text
Backup creado
      ↓
¿Puede restaurarse?
      ↓
¿La VM arranca?
      ↓
¿El sistema funciona?
```

Por ello se realizó una restauración de prueba.

## 3. Estrategia utilizada

En lugar de restaurar el backup sobre la VM original, se creó una segunda máquina virtual.

Esto permitió mantener intacta:

```text
ubuntu-server-01
```

mientras se comprobaba la recuperación en:

```text
ubuntu-server-01-restore-test
```

La arquitectura temporal quedó:

```text
pve01
│
├── ubuntu-server-01
│      └── VM original
│
└── ubuntu-server-01-restore-test
       └── VM restaurada desde backup
```

## 4. Identificación de la VM restaurada

La máquina creada para la prueba quedó identificada como:

```text
VM ID: 101
```

y recibió el nombre:

```text
ubuntu-server-01-restore-test
```

Utilizar un nombre descriptivo permitió distinguir claramente la VM restaurada de la máquina original.

## 5. Selección del backup

Desde Proxmox se localizó la copia de seguridad creada previamente.

A partir de esa copia se inició el proceso de restauración.

Conceptualmente:

```text
Backup de ubuntu-server-01
          ↓
       Restore
          ↓
Nueva máquina virtual
          ↓
VM 101
ubuntu-server-01-restore-test
```

## 6. Restauración como VM independiente

La restauración creó una nueva máquina virtual utilizando la información almacenada en el backup.

Esto permitió comprobar de forma práctica que el respaldo contenía la información necesaria para reconstruir el sistema.

La VM original permaneció disponible durante toda la prueba.

## 7. Inicio de la VM restaurada

Después de completar la restauración se inició:

```text
ubuntu-server-01-restore-test
```

El objetivo era comprobar que Ubuntu pudiera arrancar desde los discos recuperados.

El flujo de validación fue:

```text
Restore completado
       ↓
Iniciar VM 101
       ↓
Ubuntu comienza a arrancar
       ↓
Sistema operativo disponible
```

La máquina restaurada consiguió iniciar correctamente.

## 8. Verificación mediante consola

Se utilizó la consola de Proxmox para interactuar con la VM restaurada.

Esto permitió comprobar el sistema incluso antes de depender de otros métodos de administración remota.

Se verificó que Ubuntu llegara correctamente a un estado utilizable.

## 9. Inicio de sesión

Se comprobó que fuera posible acceder al sistema restaurado utilizando las credenciales correspondientes al servidor original.

Las credenciales no se incluyen en esta documentación.

El inicio de sesión confirmó que no se había recuperado únicamente una estructura vacía de VM, sino el sistema instalado previamente.

## 10. Qué demuestra esta prueba

La prueba permitió validar una cadena completa de recuperación:

```text
VM funcional
     ↓
Backup
     ↓
Copia almacenada
     ↓
Restore
     ↓
Nueva VM
     ↓
Arranque
     ↓
Inicio de sesión
     ↓
Recuperación validada
```

Esto proporciona una evidencia mucho más útil que comprobar únicamente que el archivo de backup existe.

## 11. VM original vs. VM restaurada

Después de la prueba existían temporalmente dos máquinas relacionadas:

| VM                              | Función                |
| ------------------------------- | ---------------------- |
| `ubuntu-server-01`              | Máquina original       |
| `ubuntu-server-01-restore-test` | Prueba de recuperación |

La segunda no fue creada para convertirse en un nuevo servidor permanente.

Su propósito era comprobar el funcionamiento del mecanismo de recuperación.

## 12. Consideración sobre la red

Una VM restaurada a partir de otra puede conservar configuraciones internas del sistema original.

Por esta razón, si ambas máquinas se ejecutan simultáneamente, debe prestarse atención a posibles conflictos relacionados con:

* dirección IP;
* hostname;
* servicios;
* identificadores;
* recursos de red.

Una restauración de prueba debe realizarse de forma controlada.

## 13. Importancia de probar las copias

Esta práctica permitió comprobar una regla fundamental:

> Un backup no debe considerarse completamente confiable únicamente porque fue creado sin errores.

La verdadera pregunta es:

```text
¿Puedo recuperar mi sistema con él?
```

La restauración de prueba proporciona una respuesta mucho más sólida.

## 14. Recuperación vs. disponibilidad

El backup permite recuperar una VM, pero no evita necesariamente una interrupción del servicio.

Si `pve01` sufriera un fallo físico grave, la capacidad de recuperación también dependería de:

* dónde se encuentran los backups;
* disponibilidad de otro nodo;
* almacenamiento alternativo;
* hardware disponible;
* tiempo necesario para restaurar.

Estos aspectos pertenecen a una estrategia de recuperación más avanzada.

## 15. Qué aprendí

* Un backup debe probarse mediante restauración.
* Es posible restaurar una copia como una VM independiente.
* Mantener la VM original reduce el riesgo durante la prueba.
* Una restauración correcta debe llegar más allá de crear la VM: también debe comprobarse el arranque.
* El inicio de sesión ayuda a confirmar que el sistema fue recuperado correctamente.
* Una VM restaurada puede conservar configuraciones de red de la original.
* Deben evitarse conflictos si ambas máquinas se ejecutan simultáneamente.
* Backup y recuperación forman parte del mismo proceso.

## 16. Resultado

* [x] Backup localizado.
* [x] Restauración iniciada.
* [x] VM de prueba creada.
* [x] VM ID `101` asignado.
* [x] Nombre `ubuntu-server-01-restore-test` utilizado.
* [x] VM restaurada iniciada.
* [x] Ubuntu Server arrancó correctamente.
* [x] Inicio de sesión comprobado.
* [x] VM original conservada.
* [x] Capacidad de recuperación validada.

## 17. Cierre de la Fase 4

La Fase 4 permitió pasar de disponer únicamente de una VM funcional a contar con mecanismos básicos de protección y recuperación.

```text
ubuntu-server-01
       │
       ├── Snapshots
       │     ├── post-instalación
       │     └── antes de cambios
       │
       └── Backup
             ↓
          Restore
             ↓
VM 101 — ubuntu-server-01-restore-test
             ↓
          Arranque
             ↓
      Recuperación validada
```

Con esto se comprobó tanto la creación de puntos de recuperación como la capacidad de restaurar una copia de seguridad.

## 18. Próximo paso

**Fase 5 — Docker**

Con una VM Linux funcional y una estrategia básica de recuperación comprobada, el siguiente paso será comenzar a trabajar con contenedores mediante Docker.

---

**Estado final:** 🟢 Fase 4 completada
