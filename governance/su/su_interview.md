# SU Interview Transcript

## FASE 0 — Mapa de stakeholders [COMPLETADO 2026-05-14 00:20]

| Nombre | Cargo | Tipo | Disponible (S/N) |
|--------|-------|------|-----------------|
| María González | Gerente de Retención de Clientes | SPONSOR | S |
| Carlos Méndez | Científico de Datos Senior | TECNICO | S |
| Laura Ríos | Analista de Retención | USUARIO | S |

**Informante:** María González (SPONSOR)

---

## FASE 1 — Exploración del problema [COMPLETADO 2026-05-14 14:32]

### 1.1 El problema central [COMPLETADO 2026-05-14 09:45]

**Pregunta 1:** ¿Cuál es el problema principal que quieres resolver con este proyecto?
**Respuesta:** Estamos perdiendo clientes sin anticiparlo. Cuando nos damos cuenta de que un cliente está en riesgo, ya canceló el servicio. Queremos identificar esos clientes con tiempo para actuar.
**Informante:** María González (SPONSOR)

---

**Pregunta 2:** ¿Qué está pasando hoy en tu negocio que no debería estar pasando?
**Respuesta:** Nuestro equipo de retención trabaja de forma reactiva: solo contacta a clientes que ya se quejaron o que llamaron para cancelar. No tenemos forma de saber quién está en riesgo antes de que tome esa decisión.
**Informante:** María González (SPONSOR)

---

**Pregunta 3:** ¿Qué oportunidad de negocio quieres aprovechar?
**Respuesta:** Si podemos identificar clientes en riesgo 30 días antes de que cancelen, podemos ofrecerles promociones o atención personalizada. Estimamos que retener un cliente cuesta 5 veces menos que adquirir uno nuevo.
**Informante:** María González (SPONSOR)

---

**Pregunta 4:** ¿Cuándo empezó este problema o cuándo se volvió relevante resolverlo?
**Respuesta:** El problema siempre existió, pero se volvió urgente hace 6 meses cuando la tasa de churn subió de 4% a 7% mensual, coincidiendo con la entrada de un competidor nuevo al mercado.
**Informante:** María González (SPONSOR)

### 1.2 El impacto en el negocio [COMPLETADO 2026-05-14 10:15]

**Pregunta:** (Cómo afecta a la empresa hoy)
**Respuesta:** Directamente en ingresos: con una base de 50,000 clientes y un ticket promedio de $45 mensuales, un churn del 7% significa perder aproximadamente $157,500 al mes. Además, el equipo de retención está desbordado atendiendo cancelaciones en lugar de prevenirlas.
**Informante:** María González (SPONSOR)

---

**Pregunta:** (Quiénes se ven perjudicados internamente)
**Respuesta:** El área de Retención, que no tiene herramientas para priorizar. El área Comercial, porque el costo de adquisición sube cuando el churn no se controla. Y la Dirección General, que ve caer el LTV promedio del cliente trimestre a trimestre.
**Informante:** María González (SPONSOR)

---

**Pregunta:** (Consecuencias para los clientes)
**Respuesta:** Los clientes que realmente necesitan ayuda o tienen un problema con el servicio no son contactados a tiempo. Muchos terminan cancelando cuando una llamada oportuna o una oferta diferenciada los hubiera retenido. Es un fallo de servicio que afecta la experiencia.
**Informante:** María González (SPONSOR)

### 1.3 Alcance inicial [COMPLETADO 2026-05-14 11:30]

**Pregunta 1:** ¿Cuáles son los casos de uso principales que quieres cubrir en una primera versión?
**Respuesta:** El objetivo principal es identificar clientes en riesgo de cancelación en los próximos 30 días. Con esa lista priorizada, el equipo de retención decide a quién llamar primero. En una segunda etapa nos interesaría entender por qué se van, pero eso no es parte de este proyecto.
**Informante:** María González (SPONSOR)

---

**Pregunta 2:** ¿Qué queda explícitamente fuera del alcance?
**Respuesta:** Clientes corporativos y empresas — esos tienen un proceso de cuenta dedicada completamente diferente. Este proyecto aplica solo a clientes residenciales y pequeñas empresas (segmento SMB con menos de 10 líneas).
**Informante:** María González (SPONSOR)

---

**Pregunta 3:** ¿Cuál es el horizonte temporal que necesitas para actuar?
**Respuesta:** 30 días es el horizonte ideal. Necesitamos ese margen para que el equipo de retención pueda contactar al cliente, hacer la oferta, y darle tiempo de responder antes de que llegue su fecha de renovación. Con 7 días ya es demasiado tarde en la mayoría de los casos.
**Informante:** María González (SPONSOR)

### 1.4 Limitaciones y supuestos [COMPLETADO 2026-05-14 12:50]

**Pregunta 1:** ¿Cuáles son las limitaciones técnicas, operativas o de negocio que el proyecto debe respetar?
**Respuesta:** Tres principales: primero, no podemos interrumpir los sistemas de facturación y CRM durante el horario de operación — cualquier extracción de datos debe ser en ventanas nocturnas. Segundo, el modelo debe ser explicable; si un analista llama a un cliente, debe poder decirle brevemente por qué lo contactamos, no solo 'el sistema lo dijo'. Tercero, presupuesto acotado: no podemos contratar infraestructura cloud costosa, debe correr en nuestros servidores on-premise actuales.
**Informante:** María González (SPONSOR)

---

**Pregunta 2:** ¿Qué datos, sistemas o recursos están disponibles hoy para construir el modelo de predicción?
**Respuesta:** Tenemos historial de facturación de los últimos 3 años, registros de llamadas al call center, datos de uso del servicio (consumo mensual), y el CRM con información demográfica básica. Todo está en bases de datos SQL Server. No tenemos datos de redes sociales ni fuentes externas.
**Informante:** María González (SPONSOR)

---

**Pregunta 3:** ¿Hay dependencias externas o cambios organizacionales que podrían afectar el éxito del proyecto?
**Respuesta:** Hay una migración de CRM planificada para el cuarto trimestre de este año. Si el proyecto no está listo antes de eso, tendremos que renegociar el acceso a los datos. También dependemos de que el equipo de Retención adopte la herramienta — sin su buy-in, el modelo no sirve de nada.
**Informante:** María González (SPONSOR)

---

**Pregunta 4:** ¿Cuál es tu supuesto más importante sobre cómo se comportan los clientes en riesgo?
**Respuesta:** Que el comportamiento previo a la cancelación deja señales claras en los datos: caídas en el uso, más llamadas al soporte, retrasos en pagos. Asumimos que esos patrones son consistentes y detectables con al menos 30 días de anticipación.
**Informante:** María González (SPONSOR)

### 1.5 Criterios de éxito [COMPLETADO 2026-05-14 14:32]

**Pregunta:** ¿Cuáles son los criterios específicos para medir si el proyecto tiene éxito?
**Respuesta:** Tenemos criterios en cuatro niveles:

**Técnico:** Recall ≥ 70% (identificar correctamente al menos 70% de los clientes que cancelarán en los próximos 30 días), Precisión ≥ 50%. Preferimos no perder clientes en riesgo antes que hacer llamadas innecesarias — es más costoso un falso negativo que un falso positivo.

**Operativo:** Al menos el 80% de los contactos de retención deben originarse desde la lista del modelo en los primeros 3 meses post-lanzamiento. Esto demuestra que el equipo realmente está usando la herramienta.

**Negocio:** Reducir la tasa de churn mensual de 7% a 5% en los primeros 6 meses de operación. Eso equivale a retener aproximadamente 1,000 clientes adicionales por mes.

**Presupuesto y Timeline:** Máximo $15,000 USD para desarrollo e implementación (excluyendo salarios internos). El modelo debe estar en producción antes del 1 de octubre de 2026, antes de la migración de CRM.

**Informante:** María González (SPONSOR)

---

---

## FASE 2 — Confirmación y cierre [EN CURSO]

### 2.1 Contexto del negocio [COMPLETADO 2026-05-14 15:30]

**Pregunta 2.1.1:** ¿Ha habido cambios recientes en el comportamiento de churn que podamos usar como referencia?
**Respuesta:** Sí, hubo varios factores simultáneos. El competidor nuevo lanzó una campaña agresiva de precios — sus planes son un 20% más baratos. Además, tuvimos tres incidentes de servicio importantes en ese período que generaron muchas quejas. La base de clientes no creció; de hecho, tuvimos pérdida neta de unos 800 clientes en esos 6 meses. No hubo cambios en facturación ni en operación interna que expliquen el aumento por sí solos.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.1.2:** ¿Cuál es la capacidad actual del equipo de retención para ejecutar la estrategia?
**Respuesta:** El equipo tiene 8 personas. Cada agente puede hacer entre 20 y 25 llamadas efectivas por día, capacidad total de 160 a 200 contactos diarios, unos 800 a 1,000 por semana. Hoy gastan cerca del 60% de ese tiempo atendiendo cancelaciones entrantes, así que la capacidad real disponible para contacto proactivo es de unas 300 a 400 llamadas por semana.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.1.3:** ¿Cómo concretamente usarán el equipo de retención la lista de riesgo que generemos?
**Respuesta:** Lo ideal es que cada lunes el sistema genere una lista fresca con los clientes en mayor riesgo para esa semana. Los agentes la revisan al inicio del día, se les asigna un segmento, y van trabajando en orden de prioridad. No necesitamos automatización de llamadas — el contacto humano es parte de nuestra propuesta de valor. Solo necesitamos que la lista esté disponible en una interfaz simple, idealmente exportable a Excel para que puedan tomar notas.
**Informante:** María González (SPONSOR)

---

### 2.2 Métricas de éxito y ROI [COMPLETADO 2026-05-14 16:45]

**Pregunta 2.2.1:** ¿Cuál es el threshold mínimo de mejora que consideras un resultado exitoso para el proyecto?
**Respuesta:** Si llegamos a 6% ya es un resultado positivo que justifica el proyecto. Bajar a 5% es la meta ambiciosa. El umbral de 'fracaso' lo pondría en no superar el 6.5% después de 6 meses de operación.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.2.2:** ¿Cuál es el ROI esperado o el tiempo de recuperación que necesitas ver para justificar la inversión?
**Respuesta:** Si retenemos 500 clientes adicionales por mes, son $22,500 mensuales de ingreso preservado. Con inversión de $15,000, el retorno se produce en menos de un mes. Siendo conservadores, 200 clientes adicionales = $9,000 mensuales, recuperación en menos de dos meses. Cualquier escenario por encima de 150 clientes retenidos mensualmente hace el proyecto rentable antes del tercer mes.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.2.3:** ¿Qué pasará con el tiempo liberado en operaciones si el modelo reduce el trabajo reactivo?
**Respuesta:** Redirigir ese 60% de tiempo reactivo hacia contacto proactivo de clientes en riesgo medio — no solo los de alto riesgo que el modelo priorizará, sino también los que están en zona amarilla. A más largo plazo, llamadas de fidelización a clientes con alto valor que aún no están en riesgo (iniciativa separada).
**Informante:** María González (SPONSOR)

---

### 2.3 Restricciones técnicas y operacionales [COMPLETADO 2026-05-14 17:20]

**Pregunta 2.3.1:** ¿Cuándo y durante cuánto tiempo podemos ejecutar procesos que consuman recursos sin afectar la operación?
**Respuesta:** Ventana definida: de 01:00 a 05:00 todos los días. Procesos de facturación corren entre 22:00 y 00:30. A las 05:00 empiezan respaldos automáticos. Ventana de 4 horas estable y disponible todos los días.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.3.2:** ¿Hay cambios planificados en los sistemas de datos o infraestructura que puedan afectar el acceso a los datos del modelo?
**Respuesta:** Sí, la estructura cambia bastante — pasamos de un CRM on-premise desarrollado internamente a Salesforce. Los nombres de campos, tablas y forma de consultar serán completamente diferentes. El dueño es Roberto Vargas, Director de TI. Él sabe que este proyecto depende de los datos del CRM actual y está dispuesto a coordinar para un mapeo de campos antes del corte.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.3.3:** ¿Qué nivel de explicabilidad requieren los stakeholders internos para confiar en las recomendaciones del modelo?
**Respuesta:** Necesitamos explicaciones concretas en lenguaje de cliente, no jerga técnica. Por ejemplo: 'tu consumo bajó un 40% en los últimos dos meses', 'tuviste tres llamadas al soporte este trimestre', 'tu último pago llegó con 10 días de retraso'. Una lista de dos o tres razones principales por cliente es suficiente — frases accionables, no un score numérico explicado.
**Informante:** María González (SPONSOR)

---

### 2.4 Roles, usuarios y aprobación [COMPLETADO 2026-05-14 18:15]

**Pregunta 2.4.1:** ¿Quién tiene la autoridad final para aprobar este proyecto y qué necesita ver antes de comprometer presupuesto?
**Respuesta:** La decisión final la toma el Director General, Andrés Mora. María presenta la propuesta y él firma el presupuesto. Ya tiene conocimiento del proyecto y hay voluntad política, pero necesita ver un caso de negocio formal antes de aprobar los $15,000.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.4.2:** ¿Quiénes son los usuarios reales del sistema que se va a construir?
**Respuesta:** Los Analistas de Retención, como Laura Ríos. Ellos ven la lista, priorizan sus llamadas y registran el resultado en el CRM.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.4.3:** ¿Cuántos usuarios finales usarán el sistema y en qué contextos?
**Respuesta:** 8 agentes de retención usarán la lista diariamente. María como Gerente la revisará semanalmente. Carlos Méndez la monitoreará mensualmente para detectar degradación del modelo. Total: 10 usuarios, con roles distintos.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.4.4:** ¿Hay personas o grupos que podrían resistir la implementación del sistema?
**Respuesta:** TI podría poner obstáculos si percibe trabajo extra sin recursos adicionales — especialmente con la migración de CRM encima. También hay riesgo con los propios agentes: si sienten que el modelo los va a evaluar o controlar, pueden no adoptarlo. Hay que comunicar bien que la lista es una herramienta de apoyo, no un sistema de supervisión.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.4.5:** ¿Quién específicamente tiene acceso a los datos que necesitamos para construir el modelo?
**Respuesta:** Carlos Méndez tiene acceso a bases de datos de uso y facturación. Para el CRM se necesita autorización formal de Roberto Vargas, Director de TI. Los datos de call center los administra el área de Operaciones — acceso a través de Patricia Solano.
**Informante:** María González (SPONSOR)

---

### 2.5 Timeline y milestones [COMPLETADO 2026-05-14 19:00]

**Pregunta 2.5.1:** ¿Cuál es la fecha exacta en la que el modelo debe estar en producción operativa?
**Respuesta:** El modelo debe estar en producción operativa a más tardar el 1 de septiembre de 2026. Eso da un mes de buffer antes del inicio de la migración de CRM.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.5.2:** ¿Cuáles son los hitos intermedios críticos que deben alcanzarse antes de la fecha final?
**Respuesta:** Tenemos tres hitos: Primero, Aprobación presupuestaria antes del 15 de junio de 2026. Segundo, Disponibilidad y validación de datos antes del 15 de julio de 2026 — Carlos Méndez necesita tiempo para explorar, limpiar y confirmar que los datos son suficientes. Tercero, Validación piloto con equipo de Retención en agosto, antes del go-live — Laura y los agentes confirman que la lista tiene sentido.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.5.3:** ¿Qué ocurre el 1 de octubre con la migración de CRM y cómo afecta al proyecto?
**Respuesta:** El modelo debe estar 100% operativo y estable antes del 1 de octubre. Durante la migración de CRM no pueden garantizar acceso a los datos históricos. La adaptación post-migración es aceptable como fase siguiente, pero el núcleo del sistema debe sobrevivir el corte sin intervención manual.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.5.4:** ¿Hay ventanas cerradas o períodos donde no se pueden hacer cambios en el sistema en producción?
**Respuesta:** Sí, hay tres períodos bloqueados. Primero, los últimos 5 días de cada mes — son intocables por cierre de facturación. Segundo, la primera semana de julio 2026 — tenemos una campaña comercial grande y no se pueden hacer cambios en producción. Tercero, del 24 de diciembre al 2 de enero — bloqueado completamente.
**Informante:** María González (SPONSOR)

---

### 2.6 Datos disponibles [COMPLETADO 2026-05-14 19:45]

**Pregunta 2.6.1:** ¿Tienes datos históricos sobre el problema? ¿De cuántos años aproximadamente?
**Respuesta:** Facturación y uso: 3 años atrás sin problemas. CRM: 5 años atrás, aunque los primeros 2 años son menos completos (implementación del sistema actual). Call center: 2 años de forma confiable; antes de eso los registros eran en papel y no están digitalizados.
**Informante:** María González (SPONSOR) [Respuesta de negocio — pendiente validación técnica]

---

**Pregunta 2.6.2:** ¿Dónde están guardados esos datos hoy? (ej: Excel, sistema interno, base de datos, papel)
**Respuesta:** Estructura de datos por sistema: Facturación: monto mensual, fecha de pago, días de retraso, método de pago, plan contratado. CRM: nombre, edad, dirección, fecha de alta, segmento (residencial/SMB), número de líneas. Call center: fecha de llamada, motivo (queja, consulta, cancelación, soporte técnico), duración, resolución. Uso del servicio: consumo mensual en GB o minutos según el plan, comparativo con meses anteriores. Todo está en bases de datos SQL Server.
**Informante:** María González (SPONSOR) [Respuesta de negocio — pendiente validación técnica]

---

**Pregunta 2.6.3:** ¿Esos datos son de acceso libre o hay restricciones para usarlos?
**Respuesta:** [Respuesta cubierta en sección 2.4.5 — acceso a través de Carlos Méndez (facturación/uso), Roberto Vargas (CRM) y Patricia Solano (call center)]
**Informante:** María González (SPONSOR)

---

**Pregunta 2.6.4:** ¿Hay datos que sabes que necesitaríamos pero que hoy no existen o no están disponibles?
**Respuesta:** No hay datos de redes sociales ni fuentes externas. Los datos disponibles son: historial de facturación (3 años), registros de llamadas al call center (2 años confiables), datos de uso del servicio (3 años) e información demográfica del CRM (5 años, con las primeras 2 años menos completas).
**Informante:** María González (SPONSOR) [Respuesta de negocio — pendiente validación técnica]

---

**Pregunta 2.6.5:** ¿Hay períodos donde los datos podrían estar incompletos o tener menor calidad? Por ejemplo, ¿algún mes o año donde los registros no estén completos?
**Respuesta:** Problemas conocidos: Clientes con múltiples líneas aparecen duplicados en el CRM (uno por línea en lugar de uno por cliente). Motivos de llamada al call center no estandarizados: texto libre, inconsistencias grandes. Período de 6 semanas en 2024 con lagunas en datos de uso del servicio (migración de plataforma).
**Informante:** María González (SPONSOR) [Respuesta de negocio — pendiente validación técnica con Carlos Méndez]

---

**Pregunta 2.6.6:** ¿Ha habido cambios de sistema o migraciones de datos en los últimos años que puedan haber afectado el histórico?
**Respuesta:** [Cubierto parcialmente en sección 2.3.2 — migración de CRM de on-premise a Salesforce planificada para Q4 2026. Pendiente detalle técnico de Carlos Méndez sobre impacto en datos históricos.]
**Informante:** María González (SPONSOR)

---

### 2.7 Restricciones del proyecto [COMPLETADO 2026-05-14 20:15]

**Pregunta 2.7.1:** ¿Cuál es la fecha límite para que los primeros resultados o un prototipo estén listos?
**Respuesta:** Prototipo funcional con datos reales listo para el 1 de agosto de 2026 — inicio del piloto con el equipo de Retención. Ese mes de agosto es para validar con Laura y los agentes antes del go-live del 1 de septiembre. Sin prototipo el 1 de agosto, se pierde la ventana de validación.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.7.2:** ¿Cuál es el presupuesto disponible para este proyecto?
**Respuesta:** Confirmado: $15,000 USD máximo, sin posibilidad de ampliación este año. Cubre desarrollo, herramientas y licencias. Salarios del equipo interno (Carlos, María) no entran en ese cómputo.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.7.3:** ¿Hay tecnologías obligatorias, prohibidas o preferidas que deba usar?
**Respuesta:** Infraestructura on-premise existente — servidores Windows Server 2019 con SQL Server 2019. No se pueden contratar servicios cloud por política de TI aprobada este año. TI prefiere Python sobre R (ya tienen experiencia interna). Herramientas open source bienvenidas; licencias comerciales requieren aprobación adicional (puede tomar semanas).
**Informante:** María González (SPONSOR)

---

**Pregunta 2.7.4:** ¿Hay restricciones de confidencialidad, privacidad o seguridad en los datos y resultados?
**Respuesta:** Datos de clientes sujetos a ley local de protección de datos personales. No pueden salir de servidores de la empresa ni compartirse con terceros sin anonimización previa. El modelo y resultados son información confidencial interna. Cualquier acceso a datos de clientes debe quedar registrado en bitácora de auditoría.
**Informante:** María González (SPONSOR)

---

**Pregunta 2.7.5:** ¿Hay restricciones en cómo y dónde se puede acceder al sistema o los resultados? (ej: ubicación, dispositivo, conectividad)
**Respuesta:** Los agentes trabajan exclusivamente desde escritorio en la oficina — sin trabajo remoto ni acceso móvil. Conectividad: red interna corporativa, sin acceso a internet desde estaciones de trabajo de los agentes. Interfaz debe funcionar en navegador (Chrome e IE11) o como archivo Excel — nada que requiera instalación de software adicional.
**Informante:** María González (SPONSOR)

---

## 2.8 Aprobación y gobernanza [COMPLETADO 2026-05-14 20:45]

### 2.8.1 Proceso formal de aprobación [COMPLETADO 2026-05-14 20:45]

**Pregunta:** ¿Cuál es el proceso formal de aprobación en cada hito del proyecto?

**Respuesta:** Presupuesto: Andrés Mora (Director General) aprueba los $15,000 antes del 15 de junio 2026. Inicio de desarrollo: María González da el visto bueno una vez que Carlos confirma que los datos son suficientes (hito del 15 de julio 2026). Validación piloto: Laura Ríos y María González aprueban que la lista tiene sentido operativo antes del go-live (agosto 2026). Go-live: María González firma autorización de paso a producción, con visto bueno técnico de Carlos Méndez y Roberto Vargas (TI).

**Informante:** María González (SPONSOR)

---

### 2.8.2 Responsable de decisiones durante ejecución [COMPLETADO 2026-05-14 20:45]

**Pregunta:** ¿Quién toma las decisiones clave durante la ejecución del proyecto? ¿Hay un árbitro para conflictos?

**Respuesta:** María González es responsable del proyecto desde el lado de negocio. Para decisiones técnicas (arquitectura, algoritmos, herramientas), Carlos tiene autonomía dentro de las restricciones definidas. Si hay un trade-off que afecte presupuesto, fecha o alcance, la decisión final es de María. Si hay un conflicto con TI o acceso a datos, Roberto Vargas es el árbitro.

**Informante:** María González (SPONSOR)

---

### 2.8.3 Comité de gobernanza y reportes [COMPLETADO 2026-05-14 20:45]

**Pregunta:** ¿Hay un comité de gobernanza formal? ¿Cuáles son las cadencias de reporte?

**Respuesta:** No hay un comité formal. Reporte directo: María actualiza a Andrés Mora cada dos semanas con resumen ejecutivo de tres líneas (avance, riesgos, próximo hito). Carlos y María tienen reunión semanal de seguimiento técnico. Sin steering committee ni ceremonias formales adicionales.

**Informante:** María González (SPONSOR)

---

### 2.8.4 Señales de pausa o cancelación [COMPLETADO 2026-05-14 20:45]

**Pregunta:** ¿Cuáles son las condiciones bajo las que el proyecto se pausaría o cancelaría?

**Respuesta:** Si Carlos concluye que los datos no son suficientes para entrenar un modelo con recall ≥ 70% (bloqueante técnico irrecuperable sin más inversión). Si la aprobación presupuestaria no llega antes del 30 de junio 2026 (sin ese buffer no se puede cumplir el deadline de septiembre). Si la migración de CRM se adelanta a antes de agosto 2026 (proyecto se congela hasta que la migración esté estable y haya acceso a los nuevos datos).

**Informante:** María González (SPONSOR)

---

## FASE 2 CON SPONSOR COMPLETADA [2026-05-14 20:45]

---

---

## FASE 2.T — Entrevista técnica [EN CURSO]

### 2.T.1 Estructura y volumen de datos [COMPLETADO 2026-05-14 21:30]

**Pregunta:** ¿Cómo está estructurada actualmente la información de clientes, facturación, uso de servicio y llamadas? ¿Cuál es el volumen exacto de datos en cada fuente?

**Respuesta:**

**Estructura de datos:**
- **Facturación:** Tablas `tbl_facturas` y `tbl_pagos`, bien normalizadas, las más confiables del sistema
- **CRM:** Tabla maestra `tbl_clientes` en relación uno-a-muchos con tabla `tbl_lineas` (fuente de duplicados: un cliente con varias líneas aparece una vez por línea en lugar de una entrada consolidada)
- **Call center:** Tabla `tbl_interacciones` con campo `motivo_texto varchar(500)` en texto libre — confirmado problema de estandarización
- **Dato crítico nuevo:** Datos de uso del servicio están en **base de datos SEPARADA en otro servidor SQL Server** — el ETL necesitará queries entre servidores (linked server), agregando complejidad arquitectónica no mencionada por María

**Volumen exacto:**
- Facturación: ~1.8M registros desde enero 2023, ~12 GB
- CRM: 68,000 registros en `tbl_clientes`, pero solo 50,000 clientes únicos activos (resto son bajas o duplicados)
- Call center: 420,000 interacciones en los últimos 2 años, ~3 GB
- Uso del servicio: 1.2M registros mensuales agregados por cliente, ~8 GB

**Rango recomendado para análisis:** Enero 2024 en adelante para garantizar consistencia entre todas las fuentes.

**Informante:** Carlos Méndez (TECNICO)

---

### 2.T.2 Calidad y completitud de datos [PENDIENTE]

**Pregunta:** ¿Cuáles son los problemas específicos de calidad de datos? ¿Qué lagunas temporales o incompletetud hay en cada fuente?

**Nota para operador:** Esta es la siguiente pregunta. Carlos ya ha identificado algunos problemas en 2.T.1 (duplicados en CRM, motivos texto libre, laguna de 6 semanas). Ahora necesitamos su evaluación detallada de qué tan solucionable es cada problema y cuál es el impacto en la capacidad de entrenar el modelo.

---

### 2.T.3 Acceso y restricciones técnicas [PENDIENTE]

---

## Metadata
- Fecha Fase 0: 2026-05-14
- Fecha Fase 1: 2026-05-14 (completada)
- Fecha Fase 2 con SPONSOR: 2026-05-14 (completada a las 20:45)
- Complejidad clasificada: HIGH (leer gov_state.json para confirmar)
- Señales de complejidad detectadas: Múltiples sistemas, migración de CRM, datos distribuidos, requiere validación técnica
