# Governance Harness — Reporte de Métricas del Ciclo SU.md

**Documento:** SU.md — Statement of Understanding
**Fecha de aprobación:** 2026-05-14
**Aprobado por:** María González (SPONSOR)
**Score de evaluación automática:** 0.919
**Generado por:** harness_director
**Fecha del reporte:** 2026-05-14

---

## Resumen ejecutivo

| Indicador | Valor |
|-----------|-------|
| Salud general | EXCELENTE |
| Métricas OK | 8/10 |
| Alertas activas | 0 |
| Métricas informativas | 2/10 |
| Iteraciones usadas | 1 de 4 disponibles (25%) |

El ciclo SU.md se completó con resultado óptimo: 0 alertas, aprobación en primera iteración y score de 0.919 en evaluación automática. El stakeholder aprobó en primera presentación sin rechazos.

---

## Métricas detalladas

### M01 — Tiempo de ciclo
- **Valor:** 1 día
- **Umbral de alerta:** > 10 días
- **Estado:** OK
- **Nota:** Ciclo completado en una sola jornada de trabajo (2026-05-14). Todas las fases de entrevista, síntesis, evaluación y aprobación en el mismo día.

### M02 — Iteraciones del ciclo synthesizer→evaluator
- **Valor:** 1 iteración
- **Umbral de alerta:** > 3 iteraciones
- **Estado:** OK
- **Nota:** El draft v1 pasó la evaluación automática directamente. El circuit breaker (4 iteraciones máximas para proyectos de alta complejidad) no fue necesario.

### M03 — Score final del evaluador
- **Valor:** 0.919
- **Umbral de alerta:** < 0.75
- **Estado:** OK
- **Nota:** Score por encima del umbral de aprobación (0.8). Todas las dimensiones de la rúbrica > 0.6. Sin criterios de rechazo automático (CRA).

### M04 — Gaps críticos en needs_analysis
- **Valor:** 0 gaps CRITICOS
- **Umbral de alerta:** >= 1 gap CRITICO
- **Estado:** OK
- **Nota:** 0 CRITICOS, 3 MENORES (G1: regla maestro CRM multilinea, G2: compatibilidad IE11/Chrome), 0 AUSENTES. Confidence 0.91 — nivel LISTO, umbral HIGH superado.

### M05 — Fases de entrevista completadas
- **Valor:** 5 fases (Fase 0, Fase 1, Fase 2, Fase 2.T, Fase 2.U)
- **Umbral de alerta:** < 3 fases
- **Estado:** OK
- **Nota:** Cobertura completa para complexity=high. Los 3 stakeholders entrevistados. Fases 2.T (TECNICO) y 2.U (USUARIO) ejecutadas por cumplir condición complexity=high con ambos disponibles.

### M06 — Confidence score del needs_analyzer
- **Valor:** 0.91
- **Umbral de alerta:** < 0.80
- **Estado:** OK
- **Nota:** Nivel LISTO. Umbral adaptativo para HIGH (0.85) superado. Síntesis directa sin rondas adicionales de entrevista.

### M07 — Stakeholders entrevistados
- **Valor:** 3 (SPONSOR, TECNICO, USUARIO)
- **Umbral de alerta:** <= 1 stakeholder
- **Estado:** OK
- **Nota:** María González (SPONSOR), Carlos Méndez (TECNICO), Laura Ríos (USUARIO). Cobertura de perspectivas: negocio, técnica y operativa.

### M08 — cb_threshold utilizado
- **Valor:** 4 iteraciones máximas
- **Estado:** INFORMATIVO
- **Nota:** cb_threshold=4 derivado de complexity=high (4 señales P6-1: multiples_decision_makers, alcance_multi_area, restricciones_legales, industria_regulada). Solo se utilizó 1 de 4 iteraciones disponibles — eficiencia del 25% del presupuesto de iteraciones.

### M09 — Rechazos humanos en Fase 5
- **Valor:** 0 rechazos
- **Umbral de alerta:** >= 1 rechazo
- **Estado:** OK
- **Nota:** El stakeholder aprobó en primera presentación. No fue necesario invocar post_mortem_agent ni prompt_optimizer por Disparador B.

### M10 — Nivel de complejidad
- **Valor:** high
- **Estado:** INFORMATIVO
- **Nota:** 4 señales P6-1 detectadas en Fase 1.5. Proyecto en industria con restricciones legales (protección de datos), múltiples decisores (Andrés Mora, Roberto Vargas, Patricia Solano), alcance multi-área (Retención, TI, Operaciones) y múltiples tomadores de decisión.

---

## Alertas activas

Ninguna. Todas las métricas evaluables están dentro de los umbrales esperados.

---

## Próximo documento: BRD

El harness continúa con el **Business Requirements Document (BRD)**. Estado inicial en gov_state.json: `brd.status=pending`.

El BRD debe construirse sobre la base del SU.md aprobado. Los gaps MENORES G1 y G2 documentados en el SU.md son candidatos a resolverse durante la fase de entrevista del BRD.

**Pendientes a resolver en el BRD:**
- G1: Confirmar regla de deduplicación CRM (línea más antigua como maestro) con María González
- G2: Confirmar política de navegador (Chrome primario, IE11 como secundario o descartado) con María González

---

*Fin del reporte de métricas — Ciclo SU.md*
*Generado: 2026-05-14 | harness_director*
