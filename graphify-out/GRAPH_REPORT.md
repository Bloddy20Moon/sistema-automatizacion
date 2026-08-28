# Graph Report - sistema_automatizacion  (2026-08-28)

## Corpus Check
- 4 files · ~1,379 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 25 nodes · 21 edges · 7 communities (5 shown, 2 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- dependencies
- Documento de Definición Técnica y Operativa (V4)
- 2. Fases de Implementación
- 3. Estructura de Datos (Diccionario de Datos)
- rules/graphify.md
- workflows/graphify.md
- 1. Caso de Negocio: La Crisis del Crecimiento Operativo

## God Nodes (most connected - your core abstractions)
1. `Documento de Definición Técnica y Operativa (V4)` - 6 edges
2. `2. Fases de Implementación` - 5 edges
3. `3. Estructura de Datos (Diccionario de Datos)` - 5 edges
4. `1. Caso de Negocio: La Crisis del Crecimiento Operativo` - 3 edges
5. `graphify` - 2 edges
6. `graphify` - 1 edges
7. `graphify` - 1 edges
8. `Workflow: graphify` - 1 edges
9. `A. Planteamiento del Problema` - 1 edges
10. `B. Solución Propuesta` - 1 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Communities (7 total, 2 thin omitted)

### Community 0 - "dependencies"
Cohesion: 0.50
Nodes (3): graphify, dependencies, graphify

### Community 1 - "Documento de Definición Técnica y Operativa (V4)"
Cohesion: 0.50
Nodes (3): 4. Flujo de Resiliencia y Gestión de Excepciones, 5. Optimización de Rendimiento y Consumo de APIs, Documento de Definición Técnica y Operativa (V4)

### Community 2 - "2. Fases de Implementación"
Cohesion: 0.40
Nodes (5): 2. Fases de Implementación, Fase 1: Estructuración y Fundación de Datos, Fase 2: Automatización de Ingesta y Limpieza de Datos, Fase 3: Interfaces de Visualización (Dashboards), Fase 4: Transición al Ingreso Nativo y Desconexión

### Community 3 - "3. Estructura de Datos (Diccionario de Datos)"
Cohesion: 0.40
Nodes (5): 3. Estructura de Datos (Diccionario de Datos), A. Matriz Principal de Ventas, B. Matriz de Auditoría y Trazabilidad (Historial), C. Matriz de Usuarios y Accesos, D. Matriz de Metas (Cuotas)

### Community 6 - "1. Caso de Negocio: La Crisis del Crecimiento Operativo"
Cohesion: 0.67
Nodes (3): 1. Caso de Negocio: La Crisis del Crecimiento Operativo, A. Planteamiento del Problema, B. Solución Propuesta

## Knowledge Gaps
- **15 isolated node(s):** `graphify`, `graphify`, `Workflow: graphify`, `A. Planteamiento del Problema`, `B. Solución Propuesta` (+10 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **2 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `Documento de Definición Técnica y Operativa (V4)` connect `Documento de Definición Técnica y Operativa (V4)` to `2. Fases de Implementación`, `3. Estructura de Datos (Diccionario de Datos)`, `1. Caso de Negocio: La Crisis del Crecimiento Operativo`?**
  _High betweenness centrality (0.351) - this node is a cross-community bridge._
- **Why does `2. Fases de Implementación` connect `2. Fases de Implementación` to `Documento de Definición Técnica y Operativa (V4)`?**
  _High betweenness centrality (0.196) - this node is a cross-community bridge._
- **Why does `3. Estructura de Datos (Diccionario de Datos)` connect `3. Estructura de Datos (Diccionario de Datos)` to `Documento de Definición Técnica y Operativa (V4)`?**
  _High betweenness centrality (0.196) - this node is a cross-community bridge._
- **What connects `graphify`, `graphify`, `Workflow: graphify` to the rest of the system?**
  _15 weakly-connected nodes found - possible documentation gaps or missing edges._