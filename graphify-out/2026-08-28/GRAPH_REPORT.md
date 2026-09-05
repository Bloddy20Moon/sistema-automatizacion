# Graph Report - sistema_automatizacion  (2026-08-28)

## Corpus Check
- 5 files · ~2,397 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 34 nodes · 29 edges · 8 communities (6 shown, 2 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `ac5110cd`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- dependencies
- Documento de Definición Técnica y Operativa (V4)
- 2. Fases de Implementación
- 3. Estructura de Datos (Diccionario de Datos)
- rules/graphify.md
- workflows/graphify.md
- A. Matriz Principal de Ventas (Columnas del Excel)

## God Nodes (most connected - your core abstractions)
1. `3. Estructura de Datos (Diccionario de Datos)` - 7 edges
2. `A. Matriz Principal de Ventas (Columnas del Excel)` - 7 edges
3. `Documento de Definición Técnica y Operativa (V4)` - 6 edges
4. `2. Fases de Implementación` - 5 edges
5. `1. Caso de Negocio: La Crisis del Crecimiento Operativo` - 3 edges
6. `graphify` - 2 edges
7. `graphify` - 1 edges
8. `graphify` - 1 edges
9. `Workflow: graphify` - 1 edges
10. `A. Planteamiento del Problema` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Communities (8 total, 2 thin omitted)

### Community 0 - "dependencies"
Cohesion: 0.50
Nodes (3): graphify, dependencies, graphify

### Community 1 - "Documento de Definición Técnica y Operativa (V4)"
Cohesion: 0.29
Nodes (6): 1. Caso de Negocio: La Crisis del Crecimiento Operativo, 4. Flujo de Resiliencia y Gestión de Excepciones, 5. Optimización de Rendimiento y Consumo de APIs, A. Planteamiento del Problema, B. Solución Propuesta, Documento de Definición Técnica y Operativa (V4)

### Community 2 - "2. Fases de Implementación"
Cohesion: 0.40
Nodes (5): 2. Fases de Implementación, Fase 1: Estructuración y Fundación de Datos, Fase 2: Automatización de Ingesta y Limpieza de Datos, Fase 3: Interfaces de Visualización (Dashboards), Fase 4: Transición al Ingreso Nativo y Desconexión

### Community 3 - "3. Estructura de Datos (Diccionario de Datos)"
Cohesion: 0.33
Nodes (6): 3. Estructura de Datos (Diccionario de Datos), B. Matriz de Auditoría y Trazabilidad (Historial), C. Lógica de Multiórdenes y Tipos de Venta, C. Matriz de Usuarios y Accesos, D. Matriz de Metas (Cuotas), D. Reglas de Visibilidad y Seguridad de Datos (RLS)

### Community 6 - "A. Matriz Principal de Ventas (Columnas del Excel)"
Cohesion: 0.29
Nodes (7): 1. Datos de Identificación y Control Operativo, 2. Datos del Cliente y la Gestión, 3. Especificaciones del Plan y Equipo, 4. Entrega y Logística, 5. Gestión del Asesor y Venta, 6. Calidad y Validación (Campos actualizados por Backoffice), A. Matriz Principal de Ventas (Columnas del Excel)

## Knowledge Gaps
- **22 isolated node(s):** `graphify`, `graphify`, `Workflow: graphify`, `A. Planteamiento del Problema`, `B. Solución Propuesta` (+17 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **2 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `3. Estructura de Datos (Diccionario de Datos)` connect `3. Estructura de Datos (Diccionario de Datos)` to `Documento de Definición Técnica y Operativa (V4)`, `A. Matriz Principal de Ventas (Columnas del Excel)`?**
  _High betweenness centrality (0.358) - this node is a cross-community bridge._
- **Why does `Documento de Definición Técnica y Operativa (V4)` connect `Documento de Definición Técnica y Operativa (V4)` to `2. Fases de Implementación`, `3. Estructura de Datos (Diccionario de Datos)`?**
  _High betweenness centrality (0.350) - this node is a cross-community bridge._
- **Why does `A. Matriz Principal de Ventas (Columnas del Excel)` connect `A. Matriz Principal de Ventas (Columnas del Excel)` to `3. Estructura de Datos (Diccionario de Datos)`?**
  _High betweenness centrality (0.233) - this node is a cross-community bridge._
- **What connects `graphify`, `graphify`, `Workflow: graphify` to the rest of the system?**
  _22 weakly-connected nodes found - possible documentation gaps or missing edges._