# Sprint Contract — SU.md
**Fecha de creación:** 2026-05-14
**Creado por:** doc_orchestrator (auto-reparación Paso 0)
**Estado:** ACTIVO

---

## Alcance del sprint

| Campo | Valor |
|-------|-------|
| Documento objetivo | SU.md (Statement of Understanding) |
| Harness activo | governance |
| Fase de entrada | interview_phase1 |
| Modo de ejecución | git + GitHub habilitados (actualizado 2026-05-14) |

## Artefactos a producir

| Artefacto | Path | Responsable |
|-----------|------|-------------|
| Entrevista completa | `governance/su/su_interview.md` | su_interviewer |
| Análisis de gaps | `governance/su/su_knowledge_gaps.md` | su_needs_analyzer |
| Draft SU.md | `governance/su/su_draft_v{n}.md` | su_synthesizer |
| Review | `governance/su/su_review.md` | su_evaluator + doc_auditor |
| SU aprobado | `governance/su/su_approved.md` | doc_orchestrator |

## Criterios de terminado

- [ ] su_interview.md con Fase 0, Fase 1 y Fase 2 completas
- [ ] su_knowledge_gaps.md con confidence_score
- [ ] su_draft aprobado por evaluador (score >= umbral según complejidad)
- [ ] su_approved.md aprobado por stakeholder
- [ ] gov_state.json con su.status=approved

## Restricciones

- git_available: true (actualizado 2026-05-14 tras git init por operador)
- github_remote_configured: true — Remote: https://github.com/jdrodriguez1000/Simulacion_001.git
- Commits y push habilitados. Trazabilidad via gov_history.log y GitHub.

---
*Generado automáticamente por doc_orchestrator — template /su-sprint-contract-template*
