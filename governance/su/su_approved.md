# SU.md — APROBADO
**Fecha de aprobación:** 2026-05-14
**Versión aprobada:** su_draft_v1.md
**Score de evaluación automática:** 0.919
**Aprobado por:** María González (SPONSOR)

---

# SU.md — Statement of Understanding
## Modelo predictivo de churn para clientes residenciales y SMB

**Versión:** Draft v1
**Fecha de generación:** 2026-05-14
**Generado por:** su_synthesizer
**Fuente:** governance/su/su_interview.md (Fases 0, 1, 2-SPONSOR, 2.T, 2.U completas)
**Knowledge gaps referenciados:** governance/su/su_knowledge_gaps.md (0 CRÍTICOS, 3 MENORES)

---

## 1. Problema de negocio

### 1.1 Enunciado del problema

La empresa enfrenta una tasa de churn mensual del 7% sobre una base de 50,000 clientes activos (segmentos residencial y SMB con menos de 10 líneas). Esto representa una pérdida de aproximadamente $157,500 de ingresos mensuales (50,000 clientes × $45 ticket promedio × 7%). El problema se agudizó hace 6 meses con la entrada de un competidor que ofrece planes un 20% más baratos, sumado a tres incidentes de servicio importantes que generaron quejas masivas. La base de clientes tuvo pérdida neta de 800 clientes en ese período.

El modelo de respuesta actual es estrictamente reactivo: el equipo de retención solo contacta a clientes que ya llamaron para cancelar o presentaron queja formal. No existe mecanismo de identificación temprana de clientes en riesgo antes de que tomen la decisión de cancelar. Los agentes dedican entre 4 y 5 de sus 8 horas de trabajo diarias a procesar la cola de cancelaciones del día anterior, con capacidad proactiva real de solo 300 a 400 contactos semanales sobre una capacidad total de 800 a 1,000 llamadas.

**El supuesto central del proyecto:** el comportamiento previo a la cancelación deja señales detectables en los datos (caídas en el consumo, aumento de llamadas al soporte, retrasos en pagos) que son consistentes y predecibles con al menos 30 días de anticipación.

### 1.2 Oportunidad de negocio

Retener un cliente cuesta 5 veces menos que adquirir uno nuevo. Con un modelo que identifique clientes en riesgo 30 días antes de la cancelación, el equipo puede actuar de forma proactiva mediante llamadas personalizadas y ofertas diferenciadas. Incluso en escenarios conservadores:

- 150 clientes adicionales retenidos/mes = punto de equilibrio en menos de 3 meses sobre $15,000 de inversión
- 200 clientes adicionales retenidos/mes = $9,000/mes de ingreso preservado, recuperación en menos de 2 meses
- 500 clientes adicionales retenidos/mes = $22,500/mes, recuperación en menos de 1 mes

La meta ambiciosa es reducir la tasa de churn del 7% al 5% en los primeros 6 meses de operación, equivalente a retener aproximadamente 1,000 clientes adicionales por mes.

---

## 2. Alcance del proyecto

### 2.1 Casos de uso incluidos

**Caso de uso único (v1):** Generación semanal (cada lunes) de una lista priorizada de clientes en riesgo de cancelar en los próximos 30 días, con razones explicables por cliente en lenguaje operativo, para uso del equipo de retención.

La lista debe permitir:
- Ordenamiento por nivel de riesgo (mayor a menor) como vista por defecto
- Filtrado por monto mensual (para priorizar clientes de mayor valor económico)
- Registro de resultado de llamada o nota por cliente
- Exportación a Excel para asignación de segmentos por agente

### 2.2 Fuera del alcance (v1)

- Clientes corporativos y empresas con cuenta dedicada
- Análisis de causas de churn (por qué se van) — esto es una segunda etapa separada
- Automatización de llamadas o contacto sin intervención humana
- Acceso móvil o trabajo remoto
- Fuentes de datos externas (redes sociales, datos de mercado)
- Integración post-migración a Salesforce (es una fase siguiente)

### 2.3 Segmento objetivo

Clientes residenciales y pequeñas empresas (SMB) con menos de 10 líneas. Los 50,000 clientes activos únicos son el universo de aplicación del modelo. [ALERTA: 68,000 registros en tbl_clientes incluyen bajas y duplicados — el modelo debe trabajar sobre los 50,000 activos únicos, requiere deduplicación previa.]

---

## 3. Solución propuesta

### 3.1 Naturaleza de la solución

Modelo de clasificación supervisado (clasificador binario: cancelará / no cancelará en 30 días) entrenado con datos históricos de 4 fuentes: facturación, uso del servicio, llamadas al call center y datos demográficos del CRM.

El modelo produce, como artefacto operativo, una lista semanal con:
- Nombre del cliente y teléfono de contacto
- Plan contratado y monto mensual
- Nivel de riesgo (ordenamiento, no score numérico expuesto al agente)
- Razones del riesgo en lenguaje claro (2-3 frases accionables, ej. "bajó su consumo 40%", "tres llamadas al soporte este mes", "pago con 10 días de retraso")
- Columna para registrar resultado de llamada o nota

### 3.2 Algoritmo recomendado

Gradient boosting (ej. XGBoost o LightGBM) con técnicas estándar de balanceo de clases (SMOTE o class_weight). Esta familia de algoritmos cumple con el requisito de explicabilidad mediante valores SHAP por instancia, que permiten traducir las contribuciones de features a frases en lenguaje de cliente.

### 3.3 Interfaz de usuario

La lista se entrega como archivo exportable a Excel o como vista web accesible desde navegador en red interna corporativa. Chrome es el navegador primario requerido. [PENDIENTE: confirmar con María González si IE11 es requisito duro o puede limitarse a Chrome dado el feedback de Laura Ríos sobre problemas constantes con IE11 en el CRM actual.]

La interfaz no requiere instalación de software adicional en las estaciones de trabajo de los agentes.

---

## 4. Datos y arquitectura técnica

### 4.1 Fuentes de datos

| Fuente | Tabla / Sistema | Volumen | Rango recomendado | Acceso actual de Carlos |
|--------|----------------|---------|-------------------|------------------------|
| Facturación | tbl_facturas, tbl_pagos (SQL Server principal) | ~1.8M registros, ~12 GB | Ene-2024 en adelante | Completo |
| CRM (demográfico) | tbl_clientes, tbl_lineas (SQL Server principal) | 68K registros (50K activos únicos) | Ene-2024 en adelante | Parcial — sin acceso a tbl_lineas ni historial de cambios de plan |
| Uso del servicio | Base de datos separada (SQL Server secundario) | ~1.2M registros mensuales, ~8 GB | Ene-2024 en adelante | Completo (linked server ad-hoc) |
| Call center | tbl_interacciones (SQL Server principal) | 420K interacciones (2 años), ~3 GB | Ene-2024 en adelante | Sin acceso — bajo esquema de Operaciones |

**Rango de datos para el modelo:** Enero 2024 en adelante, garantizando consistencia entre todas las fuentes. [Nota: María González indicó que la facturación y el uso tienen 3 años disponibles; Carlos Méndez recomienda ene-2024 como punto de partida para asegurar calidad homogénea entre todas las fuentes, dado que el call center solo es confiable desde ese año y la laguna de 6 semanas del servidor de uso ocurrió en 2024. Se adopta la recomendación técnica.]

### 4.2 Features principales esperados

- Tendencia de consumo mensual (últimos 3, 6, 12 meses) — señal más crítica según Laura Ríos
- Frecuencia y motivo de llamadas al call center
- Retrasos en pagos (días de retraso, frecuencia)
- Antigüedad del cliente
- Tipo de plan y monto mensual
- Número de líneas contratadas (posible feature de costo de salida — clientes multilinea tienen mayor costo de salida)
- Cambios de plan en el histórico

### 4.3 Problemas de calidad de datos conocidos y estrategia

| Problema | Estrategia técnica | Esfuerzo estimado |
|----------|-------------------|-------------------|
| Duplicados en CRM (clientes multilinea) | Consolidar por id_cliente con línea más antigua como maestro; agregar número de líneas como atributo. [PENDIENTE: confirmar con María González si tomar la línea más antigua como registro maestro es correcto desde negocio.] | 1 día (una vez confirmada la regla) |
| Campo motivo_texto en texto libre (call center) | Heurística por palabras clave + clustering TF-IDF. El 80% cae en 8 categorías naturales según exploración previa de Carlos. | 3 días |
| Laguna de 6 semanas en datos de uso (2024) | Imputación con mediana del cliente en los 3 meses anteriores y 3 posteriores a la laguna. | 1 día |
| Join facturación–uso sin id_cliente directo | Tabla puente vía número de línea. Se complica con clientes multilinea. | 2-3 días |

### 4.4 Arquitectura ETL

**Ejecución:** Proceso automatizado nocturno, ventana 01:00-05:00 (4 horas disponibles). ETL maduro estimado en 90-120 minutos. Estrategia de extracción incremental si las queries entre servidores resultan lentas.

**Servidor de uso del servicio:** Acceso vía linked server existente (configurado para queries ad-hoc, no para ETL desatendido). TI debe revisar y garantizar estabilidad para ejecución automatizada — autorización formal de Roberto Vargas (TI). Gestión estimada: 1-2 semanas si se inicia de inmediato.

**Limitaciones de entorno:** No existe entorno de desarrollo separado. Carlos trabaja directamente sobre producción con permisos de solo lectura. Esto limita las opciones de prueba del ETL.

### 4.5 Gestiones de acceso pendientes (bloqueantes de timeline)

Estas dos gestiones deben iniciarse de inmediato para no comprometer el hito del 15 de julio:

1. **Acceso a tbl_lineas y tablas de historial de cambios de plan en CRM** — Autorización de Roberto Vargas (Director de TI)
2. **Acceso a tbl_interacciones (call center)** — Autorización de Patricia Solano (área de Operaciones)

---

## 5. Criterios de éxito

### 5.1 Criterios técnicos

| Métrica | Umbral mínimo | Meta |
|---------|---------------|------|
| Recall (sensibilidad) | ≥ 70% | > 75% |
| Precisión | ≥ 50% | > 60% |

**Justificación del trade-off:** Un falso negativo (cliente en riesgo no identificado) cuesta más que un falso positivo (llamada innecesaria a un cliente que no iba a cancelar). El recall tiene prioridad sobre la precisión.

Evaluación preliminar de Carlos Méndez: alcanzable. Con 7% churn mensual sobre 50,000 clientes, se estiman 3,000-4,000 cancelaciones/mes en los últimos 12 meses — volumen adecuado. Si el desbalance de clases es no mayor de 10:1, recall ≥ 70% es alcanzable con gradient boosting estándar. [ALERTA: esta evaluación es preliminar — Carlos no puede garantizarlo sin exploración formal de datos, que ocurre en el hito del 15 de julio.]

### 5.2 Criterios operativos

- Al menos el 80% de los contactos de retención deben originarse desde la lista del modelo en los primeros 3 meses post-lanzamiento
- La lista debe estar disponible todos los lunes antes del inicio del turno
- Tiempo de carga de la interfaz: significativamente menor a 20-30 segundos del CRM actual (requisito de Laura Ríos — "40 llamadas por día no admiten un sistema lento")

### 5.3 Criterios de negocio

| Escenario | Clientes retenidos adicionales/mes | Resultado |
|-----------|-----------------------------------|-----------|
| Fracaso | ≤ 1,000 adicionales (churn > 6.5%) | Proyecto no justificado |
| Mínimo aceptable | ~1,500 adicionales (churn ≈ 6%) | Resultado positivo |
| Meta ambiciosa | ~2,000 adicionales (churn ≈ 5%) | Éxito pleno |

Umbral de fracaso: churn > 6.5% después de 6 meses de operación con el modelo activo.

### 5.4 Criterios de adopción del usuario

- Los agentes deben encontrar las razones de riesgo en "lenguaje de cliente" comprensibles y útiles para preparar la llamada
- La lista debe ser exportable a Excel para asignación de segmentos sin conflicto entre agentes
- Laura Ríos y María González aprueban que la lista tiene sentido operativo en la validación piloto de agosto 2026

---

## 6. Restricciones y condicionantes

### 6.1 Infraestructura

- **On-premise obligatorio:** Windows Server 2019 + SQL Server 2019. Sin servicios cloud por política de TI aprobada este año.
- **Lenguaje:** Python (TI tiene experiencia interna; preferido sobre R).
- **Licencias:** Herramientas open source bienvenidas. Licencias comerciales requieren aprobación adicional (puede tomar semanas — debe anticiparse si aplica).
- **Sin entorno de desarrollo separado:** Carlos trabaja sobre producción con permisos de solo lectura.

### 6.2 Datos y privacidad

- Datos de clientes sujetos a ley local de protección de datos personales
- Los datos no pueden salir de los servidores de la empresa ni compartirse con terceros sin anonimización previa
- Cualquier acceso a datos de clientes debe quedar registrado en bitácora de auditoría
- El modelo y sus resultados son información confidencial interna

### 6.3 Operativas

- Extracciones de datos solo en ventana nocturna: 01:00-05:00 (no interrumpir facturación 22:00-00:30 ni respaldos desde 05:00)
- Los agentes trabajan exclusivamente desde escritorio en oficina — sin trabajo remoto ni acceso móvil
- Conectividad: red interna corporativa sin acceso a internet desde estaciones de trabajo de agentes
- El modelo debe ser explicable en 2-3 frases accionables por cliente — no se expone score numérico al agente

### 6.4 Período de cambios bloqueados (freeze)

| Período | Razón |
|---------|-------|
| Últimos 5 días de cada mes | Cierre de facturación — intocable |
| Primera semana de julio 2026 | Campaña comercial grande — sin cambios en producción |
| 24 dic 2026 – 2 ene 2027 | Cierre de año — bloqueado completamente |

---

## 7. Timeline y hitos

| Hito | Fecha | Responsable | Condición de aprobación |
|------|-------|-------------|------------------------|
| Aprobación presupuestaria ($15,000) | ≤ 15-jun-2026 | Andrés Mora (Director General) | Caso de negocio formal presentado por María González |
| Exploración y validación de datos | ≤ 15-jul-2026 | Carlos Méndez (TECNICO) | Carlos confirma que los datos son suficientes para recall ≥ 70% |
| Inicio de desarrollo formal | 16-jul-2026 | María González (SPONSOR) | Visto bueno de María tras confirmación técnica de Carlos |
| Prototipo funcional con datos reales | 1-ago-2026 | Equipo de desarrollo | Lista generada con datos reales, lista para piloto |
| Validación piloto con equipo de retención | Agosto 2026 | Laura Ríos + María González | Aprobación operativa de que la lista tiene sentido |
| Go-live en producción | 1-sep-2026 | María González + Carlos + Roberto Vargas | Visto bueno técnico y de negocio |
| Migración de CRM (bloqueante externo) | 1-oct-2026 | Roberto Vargas (TI) | El modelo debe estar estable antes de este corte |

**Señales de pausa o cancelación del proyecto:**
1. Carlos concluye en el hito del 15-jul que los datos son insuficientes para recall ≥ 70% (bloqueante técnico irrecuperable)
2. Aprobación presupuestaria no llega antes del 30-jun-2026 (se pierde el buffer para cumplir el deadline de septiembre)
3. La migración de CRM se adelanta a antes de agosto 2026 (proyecto se congela hasta que la migración esté estable)

---

## 8. Stakeholders y roles

| Nombre | Cargo | Rol en el proyecto | Responsabilidad |
|--------|-------|-------------------|-----------------|
| Andrés Mora | Director General | Patrocinador ejecutivo | Aprobación presupuestaria — necesita caso de negocio formal |
| María González | Gerente de Retención | SPONSOR / Dueña del proyecto | Decisiones de negocio, aprobación de hitos, reporte a Andrés Mora (cada 2 semanas) |
| Carlos Méndez | Científico de Datos Sr. | TECNICO / Responsable técnico | Exploración de datos, desarrollo del modelo, monitoreo mensual en producción |
| Laura Ríos | Analista de Retención | USUARIO principal | Uso diario de la lista, aprobación piloto, representante de los 8 agentes |
| Roberto Vargas | Director de TI | Árbitro de conflictos TI | Autorización de acceso a datos (CRM, linked server), gestión de migración a Salesforce |
| Patricia Solano | Área de Operaciones | Custodio de datos | Autorización de acceso a datos de call center |

**Árbitro de conflictos:** Roberto Vargas para conflictos técnicos/TI; María González para trade-offs de presupuesto, fecha o alcance.

**Usuarios finales del sistema:**
- 8 agentes de retención — usan la lista diariamente
- María González — revisa la lista semanalmente (gestión)
- Carlos Méndez — monitorea el modelo mensualmente (degradación)

**Riesgos de adopción:**
- TI puede poner obstáculos con trabajo extra durante la migración de CRM — comunicar valor y coordinar con Roberto Vargas desde el inicio
- Los agentes pueden resistir si perciben el sistema como herramienta de supervisión — comunicar que es herramienta de apoyo, no de control

---

## 9. Gobernanza y aprobación

### 9.1 Proceso de aprobación por hito

| Hito | Aprobador(es) |
|------|--------------|
| Presupuesto | Andrés Mora |
| Inicio de desarrollo | María González (con confirmación técnica de Carlos) |
| Piloto | Laura Ríos + María González |
| Go-live | María González + Carlos Méndez + Roberto Vargas |

### 9.2 Cadencia de reporte

- María González → Andrés Mora: reporte ejecutivo cada 2 semanas (3 líneas: avance, riesgos, próximo hito)
- Carlos Méndez ↔ María González: reunión semanal de seguimiento técnico
- Sin steering committee ni ceremonias formales adicionales

### 9.3 Presupuesto

- Máximo: $15,000 USD — sin posibilidad de ampliación este año
- Incluye: desarrollo, herramientas y licencias
- Excluye: salarios internos de Carlos Méndez y María González

---

## Pendientes documentados (gaps MENORES — no bloquean síntesis)

| ID | Pendiente | Decisor | Impacto si no se resuelve antes del BRD |
|----|-----------|---------|----------------------------------------|
| G1 | Confirmar si la línea más antigua es el registro maestro correcto para clientes multilinea (regla de negocio de deduplicación CRM) | María González | Bajo — Carlos puede proponer la regla por defecto; si está equivocada se corrige en fase de datos |
| G2 | Confirmar si IE11 es requisito duro o puede limitarse a Chrome como navegador primario, dado el feedback de Laura Ríos sobre problemas constantes con IE11 | María González | Bajo — Chrome funciona en cualquier escenario; IE11 puede agregarse como requisito secundario de bajo esfuerzo |

---

*Fin del SU.md — APROBADO*
*Generado a partir de: Fase 0 (stakeholders), Fase 1 (1.1-1.5 con SPONSOR), Fase 2 (2.1-2.8 con SPONSOR), Fase 2.T (2.T.1-2.T.3 con TECNICO), Fase 2.U (2.U.1-2.U.2 con USUARIO)*
*Knowledge gaps: 0 CRITICOS, 3 MENORES, 0 AUSENTES — confidence 0.91 (LISTO)*
*Aprobado por María González (SPONSOR) el 2026-05-14. Score evaluación automática: 0.919*
