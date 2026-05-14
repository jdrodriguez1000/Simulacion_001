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
| Modo de ejecución | local (sin git, sin remoto) |

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

- Modo local: commits git y push no disponibles. Trazabilidad via gov_history.log.
- github_remote_configured: false
- git_available: false

---
*Generado automáticamente por doc_orchestrator — template /su-sprint-contract-template*
