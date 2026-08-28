# Documento de Definición Técnica y Operativa (V4)

**Proyecto:** Plataforma Inteligente de Monitoreo y Efectividad Comercial

Este documento detalla exhaustivamente cada fase operativa, los pasos de ejecución y la estructura de datos para la transición hacia la nueva plataforma.

---

## 1. Caso de Negocio: La Crisis del Crecimiento Operativo

### A. Planteamiento del Problema
Actualmente, la operación comercial se sostiene sobre una arquitectura transitoria basada en múltiples hojas de cálculo (Google Sheets / Excel) creadas mes a mes. El volumen transaccional actual ha puesto en evidencia cuellos de botella críticos:
* **Fragmentación Histórica:** Un archivo nuevo por mes fragmenta el historial de clientes y asesores, haciendo que los análisis trimestrales requieran un trabajo de consolidación manual masivo.
* **Carga Administrativa:** El equipo realiza tareas manuales repetitivas, como el desdoblamiento manual de ventas múltiples ("Ventas Dobles" o "Triples") y la actualización diaria de estados a las 2:00 PM.
* **Riesgo de Datos:** Inconsistencias de formato en los números telefónicos, DNIs mal ingresados o duplicados no controlados ensucian los reportes de efectividad y comisiones.
* **Falta de Visibilidad:** Los asesores operan "a ciegas" sin acceso en tiempo real a su progreso de cuotas, efectividad o alertas de rechazos.

### B. Solución Propuesta
Transicionar a una **Plataforma Web Centralizada con Base de Datos Relacional (PostgreSQL)** basada en Next.js (React) y Node.js.
* **Ingesta y Desdoblamiento Automático (ETL):** El backend leerá los Sheets/formularios y separará de forma automática las ventas multilínea.
* **Lógica de UPSERT:** El sistema actualizará los estados modificados por Backoffice (2:00 PM) sin generar duplicados.
* **Resiliencia (Ventas Huérfanas):** Los DNI erróneos irán a una cola especial para asignación manual en vez de perder la venta.
* **Dashboards por Rol:** Vistas diferenciadas y seguras para Asesores, Supervisores y la Jefatura.

---

## 2. Fases de Implementación

### Fase 1: Estructuración y Fundación de Datos
* **Paso 1 - ERD:** Diseño del Modelo Entidad-Relación (Ventas, Usuarios, Colas, Auditoría).
* **Paso 2 - Clave Compuesta:** Unidad mínima de negocio: la línea (`ID_ORDEN` + `NÚMERO/CORRELATIVO`).
* **Paso 3 - Auditoría:** Estructura que guardará el histórico de modificaciones (valor anterior, nuevo, autor, fecha).
* **Paso 4 - Seguridad:** Segmentación de colas (`WSP APP`, `WSP APP RENO`, `WSP DIGITAL`, `C2C APP`, `C2C DIGITAL`).

### Fase 2: Automatización de Ingesta y Limpieza de Datos
* **Paso 1 - Lector:** Proceso automatizado que lee periódicamente las filas del Google Sheet.
* **Paso 2 - Normalización (Regex):** Eliminación de espacios y caracteres en números de portabilidad.
* **Paso 3 - Desdoblamiento:** Creación de múltiples registros en la base de datos a partir de una celda con múltiples números.
* **Paso 4 - UPSERT:** Lógica inteligente de actualización sin duplicidades.

### Fase 3: Interfaces de Visualización (Dashboards)
* **Paso 1 - Panel Asesor:** Resumen diario, mis ventas, caídas (gráficos de motivos y tendencia), metas y alertas.
* **Paso 2 - Panel Supervisor:** Analítica de equipo, operaciones, caídas (drill-down por asesor), configuraciones, cuotas y alerts.
* **Paso 3 - Panel Jefe:** Vista comparativa inter-colas y panel de administración de cuentas (usuarios, roles, colas).
* **Paso 4 - Panel de Excepciones:** Bandeja para resolver ventas huérfanas y errores de carga.

### Fase 4: Transición al Ingreso Nativo y Desconexión
* **Paso 1 - Formulario Web:** Carga nativa para los asesores con validación inmediata.
* **Paso 2 - Panel de Backoffice:** Pantallas dedicadas para validadores y carga masiva de estados.
* **Paso 3 - Marcha Blanca:** Funcionamiento en paralelo.
* **Paso 4 - Desconexión:** Apagado definitivo del motor de sincronización con Google Sheets.

---

## 3. Estructura de Datos (Diccionario de Datos)

### A. Matriz Principal de Ventas
| Dato a Capturar | Tipo | Propósito |
| :--- | :--- | :--- |
| **Identificador de Orden** | Texto Alfanumérico | Código de expediente general agrupador. |
| **Correlativo / Número** | Texto Numérico / Entero | Identificador de línea. Para líneas nuevas, inicia como "POR ASIGNAR". |
| **Documento del Asesor** | Texto Numérico | DNI del asesor para asociar KPIs y comisiones. |
| **Tipo de Transacción** | Lista Opciones | Portabilidad, Línea Nueva, Línea Adicional, Renovación. |
| **Estado de Operación** | Lista Opciones | Pendiente, Activado, Caído. |
| **Motivo de Caída** | Lista Opciones | Causa del rechazo (Riesgo Crediticio, Fraude, Desiste, etc.). |
| **Condición de Equipo y Logística** | Lista Opciones | Tipo de entrega (Delivery, Tienda) y hardware (Solo Chip, Con Equipo). |
| **Fecha de Ingreso** | Fecha y Hora | Cuándo el asesor ingresó la venta. |
| **Fecha de Activación** | Fecha y Hora | Cuándo el Backoffice cerró la venta en Siebel. |
| **Fecha de Última Modificación** | Fecha y Hora | Control de auditoría técnica. |

### B. Matriz de Auditoría y Trazabilidad (Historial)
* **Referencia de Venta:** Expediente y correlativo modificado.
* **Elemento Modificado:** Campo que cambió (ej. "Estado de Operación").
* **Dato Anterior / Dato Nuevo:** Valores antes y después del cambio.
* **Autor & Marca de Tiempo:** Quién editó y cuándo.

### C. Matriz de Usuarios y Accesos
* **Documento / DNI:** Login único del personal.
* **Rol:** Asesor, Supervisor, Jefe de Supervisión.
* **Cola Asignada:** `WSP APP`, `WSP APP RENO`, `WSP DIGITAL`, `C2C APP`, `C2C DIGITAL`.

### D. Matriz de Metas (Cuotas)
* **Asociación:** DNI del asesor o ID de la Cola.
* **Periodo:** Mes y Año (ej. `2026-08`).
* **Meta (Cuota):** Cantidad de líneas activadas a cumplir.

---

## 4. Flujo de Resiliencia y Gestión de Excepciones

* **Inconsistencias (Opción A):** Si el asesor marca "Venta Doble" pero digita un solo número, el sistema registra una venta simple con una alerta amarilla en el panel del supervisor, evitando duplicaciones falsas.
* **Ventas Huérfanas:** Si el DNI no existe en el catálogo de usuarios, el registro no se borra. Pasa a una bandeja de "Ventas Huérfanas" para que el supervisor lo reasigne manualmente.
* **Reingresos:** Si una venta se cae en Siebel (ID 01) y se vuelve a ingresar generando un nuevo ID de Siebel (ID 02), el sistema registra ID 01 como "CAÍDO" e ID 02 como una nueva transacción independiente.

---

## 5. Optimización de Rendimiento y Consumo de APIs

Para evitar la saturación de consultas recurrentes, cuellos de botella en el servidor y latencia en el consumo de la API REST, se implementarán las siguientes reglas de optimización a nivel de base de datos PostgreSQL:

* **Encapsulamiento en Vistas y Funciones Almacenadas (Procedimientos):** Las agregaciones complejas (como el cálculo del porcentaje de efectividad diaria/mensual, el ranking de asesores y la analítica comparativa entre colas) se resolverán del lado del motor PostgreSQL utilizando **Vistas (Views)**, **Vistas Materializadas (Materialized Views)** o **Funciones de Base de Datos (PL/pgSQL)**. Esto permite que el backend de Next.js consuma resultados precalculados o consultas sumamente eficientes.
* **Índices de Alto Rendimiento:** Se crearán índices compuestos y de búsqueda en las columnas de mayor filtrado y agrupación:
  * Índice sobre `agentDni` para el panel individual del asesor.
  * Índice sobre `opState` y `createdAt` para el filtrado de analíticas por estados y fechas.
  * Índice compuesto sobre `[orderId, correlative]` para la validación ultrarrápida del motor de UPSERT.
* **Vistas de Caché para Dashboards:** La Jefatura y los supervisores consumirán vistas pre-agregadas que evitarán el escaneo completo de la tabla principal de ventas en cada petición de API.
