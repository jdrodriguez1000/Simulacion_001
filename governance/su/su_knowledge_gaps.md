# SU Knowledge Gaps — Análisis pre-síntesis

**Agente:** su_needs_analyzer
**Documento base:** governance/su/su_interview.md
**Fecha de análisis:** 2026-05-14
**Complejidad del proyecto:** HIGH
**Umbral de confidence para complejidad HIGH:** 0.85

---

## Resultado del análisis

| Campo | Valor |
|-------|-------|
| **confidence_score** | 0.91 |
| **confidence_level** | LISTO |
| **gaps_criticos** | 0 |
| **gaps_menores** | 3 |
| **gaps_ausentes** | 0 |
| **Recomendación** | Proceder directamente a síntesis — confidence supera umbral HIGH (0.85). Los 3 gaps MENORES deben anotarse con [PENDIENTE] en el draft para resolución posterior. |

---

## Evaluación por sección

| Sección | Estado | Fuente | Observación |
|---------|--------|--------|-------------|
| 1.1 Problema central | COMPLETA | SPONSOR | Problema enunciado con claridad, contexto temporal, oportunidad de negocio. |
| 1.2 Impacto en el negocio | COMPLETA | SPONSOR | Cifras cuantitativas ($157,500/mes), áreas afectadas, consecuencias. |
| 1.3 Alcance | COMPLETA | SPONSOR | Casos de uso, exclusiones explícitas (corporativos), horizonte 30 días. |
| 1.4 Limitaciones y supuestos | COMPLETA | SPONSOR + TECNICO | Restricciones operativas, datos disponibles, dependencias. Gap menor G1. |
| 1.5 Criterios de éxito | COMPLETA | SPONSOR | Recall ≥ 70%, precisión ≥ 50%, adopción 80%, churn a 5%, $15K, 1-oct-2026. |
| 2.1 Contexto del negocio | COMPLETA | SPONSOR | Factores churn, capacidad equipo (300-400 llamadas proactivas/semana). |
| 2.2 Métricas y ROI | COMPLETA | SPONSOR | Umbrales éxito/fracaso, escenarios ROI, uso del tiempo liberado. |
| 2.3 Restricciones técnicas | COMPLETA | SPONSOR | Ventana 01:00-05:00, migración CRM a Salesforce, explicabilidad en lenguaje claro. |
| 2.4 Roles y usuarios | COMPLETA | SPONSOR | Tomadores de decisión, usuarios (10), resistencias, custodios de datos. |
| 2.5 Timeline y milestones | COMPLETA | SPONSOR | Producción 1-sep-2026, hitos intermedios, períodos bloqueados. |
| 2.6 Datos disponibles | COMPLETA | SPONSOR + TECNICO | Fuentes con volúmenes exactos. Gap menor G2. |
| 2.7 Restricciones del proyecto | COMPLETA | SPONSOR | Presupuesto, tecnología, privacidad, acceso físico. |
| 2.8 Gobernanza | COMPLETA | SPONSOR | Proceso de aprobación, árbitros, cadencia de reporte, señales de pausa. |
| 2.T.1 Estructura y volumen | COMPLETA | TECNICO | Tablas confirmadas, volúmenes exactos, linked server identificado. |
| 2.T.2 Calidad de datos | COMPLETA | TECNICO | Duplicados CRM, campo texto libre call center, laguna 6 semanas. |
| 2.T.3 Acceso y restricciones | COMPLETA | TECNICO | Linked server, permisos pendientes (tbl_lineas, call center), ETL complejo. |
| 2.U.1 Flujo de usuario final | COMPLETA | USUARIO | Flujo diario detallado, 4-5h/8h en cola reactiva, datos necesarios por cliente. |
| 2.U.2 Requisitos de interfaz | COMPLETA | USUARIO | Campos requeridos, razones en lenguaje claro, filtros, Excel, Chrome. Gap menor G3. |

---

## Gaps detectados por sección

### G1 — Regla de negocio para consolidar clientes multilinea [MENOR]

**Sección afectada:** 1.4 Limitaciones y supuestos / 2.T.2.1 (Duplicados en CRM)
**Descripción:** Carlos Méndez propone consolidar clientes multilinea tomando la línea más antigua como registro maestro y agregar el número de líneas adicionales como atributo. Sin embargo, indica explícitamente que necesita confirmación de María González sobre la regla de negocio antes de implementar.
**Impacto en el SU.md:** Bajo. La estrategia técnica de deduplicación es clara; falta solo la validación de negocio.
**Fuente posible:** preguntar al stakeholder (María González — SPONSOR)
**Resolución recomendada:** El synthesizer anota `[PENDIENTE: confirmar con María González si tomar línea más antigua como maestro para clientes multilinea es correcto desde negocio]` en la sección de datos.

---

### G2 — Rango temporal de datos para el modelo [MENOR]

**Sección afectada:** 2.6 Datos disponibles / 2.T.1
**Descripción:** María González indica que los datos de facturación y uso tienen 3 años de antigüedad. Carlos Méndez recomienda usar datos desde enero 2024 en adelante para garantizar consistencia entre todas las fuentes (el call center solo es confiable desde 2024, y la laguna de 6 semanas ocurrió en 2024). Hay una tensión entre lo que el negocio cree disponible y lo que el técnico recomienda usar.
**Impacto en el SU.md:** Bajo — la fuente técnica (Carlos) es la autoridad en este punto. El SU.md debe reflejar la recomendación técnica como definición de trabajo.
**Fuente posible:** stakeholder + técnico (información existente en entrevista — Carlos es la fuente autorizada)
**Resolución recomendada:** El synthesizer toma la recomendación técnica de Carlos (ene-2024 en adelante) como dato definitivo y lo documenta sin anotación [PENDIENTE], dado que la fuente técnica es explícita. Opcional: notar que el negocio pensaba tener 3 años disponibles.

---

### G3 — Tensión Chrome vs IE11 en requisitos de interfaz [MENOR]

**Sección afectada:** 2.7.5 Acceso al sistema / 2.U.2.2 Fricciones actuales
**Descripción:** La sección 2.7.5 especifica que la interfaz debe funcionar en Chrome e IE11. Laura Ríos indica en 2.U.2.2 que IE11 tiene problemas constantemente con el CRM actual y solicita que el nuevo sistema funcione bien en Chrome. Hay una tensión entre el requisito de negocio (ambos navegadores) y la preferencia operativa del usuario (Chrome primero).
**Impacto en el SU.md:** Bajo — no bloquea la síntesis, pero debe documentarse para que el stakeholder decida si IE11 es un requisito duro o una preferencia que puede relajarse.
**Fuente posible:** preguntar al stakeholder (María González)
**Resolución recomendada:** El synthesizer documenta Chrome como requisito primario e IE11 como requisito secundario a confirmar, con anotación `[PENDIENTE: confirmar con María González si IE11 es requisito duro o puede limitarse a Chrome dado el feedback de Laura]`.

---

## Resumen para el orquestador

```
confidence_score: 0.91
confidence_level: LISTO
gaps_criticos: 0
gaps_menores: 3
gaps_ausentes: 0
recommendation: Proceder directamente a su_synthesizer. Incluir los 3 gaps MENORES como anotaciones [PENDIENTE] en las secciones correspondientes del draft.
aborted: false
```
