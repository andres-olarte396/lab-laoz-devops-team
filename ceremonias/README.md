# Ceremonias Ágiles

Este directorio documenta las ceremonias ágiles estándar utilizadas por los equipos de desarrollo, siguiendo el marco Scrum con adaptaciones para el modelo Team Topologies.

## 📋 Tabla de Contenidos

- [Visión General de Ceremonias](#visión-general-de-ceremonias)
- [Daily Standup](#daily-standup)
- [Sprint Planning](#sprint-planning)
- [Backlog Refinement](#backlog-refinement)
- [Sprint Review](#sprint-review)
- [Sprint Retrospective](#sprint-retrospective)
- [Ceremonias Adicionales por Equipo](#ceremonias-adicionales-por-equipo)

---

## 🎯 Visión General de Ceremonias

### Calendario de Ceremonias (Sprints de 2 semanas)

| Día | Semana 1 | Semana 2 |
|-----|----------|----------|
| **Lunes** | Daily Standup (15min) | Daily Standup (15min) |
| | | **Sprint Planning** (2-4h) 🔴 |
| **Martes** | Daily Standup (15min) | Daily Standup (15min) |
| | **Backlog Refinement** (1h) | |
| **Miércoles** | Daily Standup (15min) | Daily Standup (15min) |
| **Jueves** | Daily Standup (15min) | Daily Standup (15min) |
| | | **Sprint Review** (1h) 🔴 |
| **Viernes** | Daily Standup (15min) | Daily Standup (15min) |
| | **Backlog Refinement** (1h) | **Sprint Retrospective** (1h) 🔴 |

🔴 = Ceremonias principales de inicio/cierre de sprint

---

### Roles en Ceremonias

| Rol | Daily Standup | Sprint Planning | Refinement | Sprint Review | Retrospective |
|-----|---------------|-----------------|------------|---------------|---------------|
| **Product Owner** | Opcional | Obligatorio | Obligatorio | Obligatorio | Obligatorio |
| **Scrum Master / Tech Lead** | Obligatorio | Obligatorio | Obligatorio | Obligatorio | Obligatorio |
| **Development Team** | Obligatorio | Obligatorio | Obligatorio | Obligatorio | Obligatorio |
| **QA Engineer** | Obligatorio | Obligatorio | Recomendado | Obligatorio | Obligatorio |
| **UX/UI Designer** | Recomendado | Recomendado | Recomendado | Obligatorio | Opcional |
| **DevOps / SRE** | Opcional | Opcional | Opcional | Opcional | Opcional |
| **Stakeholders** | No | No | No | Opcional | No |

---

## 🌅 Daily Standup

**Objetivo**: Sincronización diaria del equipo, identificación de blockers, coordinación del trabajo del día.

### Formato

- **Frecuencia**: Diaria (Lunes a Viernes)
- **Duración**: 15 minutos (estricto)
- **Horario**: 9:30 AM o 10:00 AM (consistente)
- **Ubicación**: Presencial (de pie) o Virtual (Zoom/Teams)
- **Facilitador**: Tech Lead o Scrum Master

### Participantes

- **Obligatorio**: Development Team (Frontend, Backend, Full-Stack, Mobile, QA)
- **Recomendado**: Product Owner, Tech Lead
- **Opcional**: UX/UI Designer (si trabajan en feature activa), DevOps (si hay issues de infra)

### Estructura

Cada miembro del equipo responde **3 preguntas** (máx 1-2 minutos por persona):

1. **¿Qué hice ayer?** - Progreso en tasks, PRs mergeados, trabajo completado
2. **¿Qué haré hoy?** - Plan para el día, tasks a trabajar, PRs a revisar
3. **¿Tengo algún blocker?** - Impedimentos que previenen progreso

### Reglas

✅ **Hacer**:
- Llegar a tiempo (puntualidad es clave)
- Ser conciso (1-2 minutos máximo)
- Enfocarse en el trabajo del sprint
- Identificar blockers claramente
- Tomar notas de seguimientos necesarios

❌ **No hacer**:
- Llegar tarde o saltarse el standup
- Entrar en discusiones técnicas profundas (tomar offline)
- Reportar a un "jefe" (esto es sincronización entre pares)
- Leer del tablero (el equipo ya puede verlo)
- Exceder 15 minutos totales

### Ejemplos

**Buen standup**:
> "Ayer completé el endpoint de autenticación (PR #234), hoy voy a empezar con la integración del frontend y revisar el PR de Sarah. Estoy bloqueado esperando acceso a la base de datos de staging."

**Standup mejorable**:
> "Ayer trabajé en varias cosas... estuve viendo el código... hice algunos cambios... hoy no sé bien, voy a ver qué hay... no tengo blockers creo."

### Manejo de Blockers

Si se identifica un blocker:
1. **Anotar el blocker** en Jira/Linear
2. **Definir owner** para resolverlo (puede no ser quien lo reporta)
3. **Time-box la discusión** (máx 2 minutos)
4. **Mover a "parking lot"** si requiere >2 minutos
5. **Follow-up inmediato** post-standup con las personas relevantes

### Formato Alternativo: Async Standup

Para equipos remotos en zonas horarias muy diferentes:

**Tool**: Slack bot (Geekbot, Standuply) o thread en Slack

**Proceso**:
- Bot pregunta las 3 preguntas cada mañana
- Cada persona responde en texto (antes de 10 AM)
- Equipo lee las actualizaciones asincrónicamente
- Blockers se discuten en threads o calls 1:1

**Cuándo usar**:
- Equipo distribuido en >4 zonas horarias
- Equipo completamente remoto con preferencia async
- **No recomendado** para equipos co-ubicados o en zonas horarias cercanas

---

## 📅 Sprint Planning

**Objetivo**: Planificar el trabajo del próximo sprint, definir el Sprint Goal, comprometerse con un conjunto de User Stories.

### Formato

- **Frecuencia**: Cada 2 semanas (inicio de sprint)
- **Duración**: 2-4 horas (dependiendo del tamaño del equipo)
- **Horario**: Lunes 9:00 AM - 1:00 PM
- **Ubicación**: Presencial (recomendado) o Virtual
- **Facilitador**: Tech Lead o Scrum Master

### Participantes

- **Obligatorio**: Product Owner, Development Team, Tech Lead
- **Recomendado**: QA Engineer, UX/UI Designer (para features con diseño)
- **Opcional**: DevOps Lead (si hay dependencias de infraestructura)

---

### Parte 1: Sprint Goal & Prioridades (45-60 min)

**Responsable**: Product Owner

#### Actividades:

1. **Review del sprint anterior** (15min)
   - ¿Qué se completó? ¿Qué no se completó y por qué?
   - Velocity del último sprint (story points completados)

2. **Presentación de prioridades** (30min)
   - Product Owner presenta las top priorities del backlog
   - Contexto de negocio: ¿Por qué estas features ahora?
   - Dependencias con otros equipos o features

3. **Definición del Sprint Goal** (15min)
   - Equipo + PO acuerdan un objetivo claro del sprint en 1-2 frases
   - Ejemplo: *"Completar el flujo de checkout para usuarios móviles"*

#### Entregable:
- **Sprint Goal** documentado en Jira/Linear

---

### Parte 2: Capacity Planning (30 min)

**Responsable**: Tech Lead + Engineering Manager

#### Actividades:

1. **Disponibilidad del equipo**
   - ¿Quién estará de vacaciones, en training, o en on-call?
   - Días laborables efectivos por persona

2. **Cálculo de capacidad**
   - Velocity promedio de últimos 3 sprints
   - Ajuste por disponibilidad (si alguien está out 50% tiempo, restar 50% de su capacidad)
   - **Ejemplo**: Team de 5 devs, 40 story points/sprint promedio, 1 dev de vacaciones = ~32 points

3. **Buffer para imprevistos**
   - Dejar 10-20% de capacidad para bug fixes, tech debt, interrupciones
   - **Ejemplo**: 32 points de capacidad → commit a ~26-28 points

#### Entregable:
- **Capacity plan**: X story points disponibles para este sprint

---

### Parte 3: Story Selection & Breakdown (60-120 min)

**Responsable**: Todo el equipo

#### Actividades:

1. **Selección de User Stories** (30min)
   - Empezar con las top priorities del backlog
   - Añadir stories hasta llegar a la capacidad
   - Validar que cada story tiene:
     - Acceptance criteria claros
     - Diseños (si aplica)
     - Estimación (story points)

2. **Task Breakdown** (30-60min)
   - Cada User Story se descompone en **tasks técnicas**
   - Ejemplo: User Story "Login con Google"
     - Task 1: Configurar OAuth en Google Cloud (2h)
     - Task 2: Backend endpoint `/auth/google` (4h)
     - Task 3: Frontend botón y redirect (3h)
     - Task 4: Tests E2E (3h)
   - Asignar owner inicial (puede cambiar durante el sprint)

3. **Identificación de Dependencias** (15min)
   - ¿Alguna story depende de otro equipo? (DevOps, Diseño, Backend)
   - ¿Algún blocker conocido?
   - Crear tasks para resolver dependencias

4. **Commitments** (15min)
   - Equipo hace commit final al Sprint Backlog
   - **Pregunta clave**: *"¿Estamos confiados que podemos completar este trabajo?"*
   - Si hay dudas, remover stories de menor prioridad

#### Entregable:
- **Sprint Backlog** con User Stories y Tasks en Jira/Linear
- **Estimación total** dentro de la capacidad del equipo

---

### Parte 4: Kickoff & Dependencies (15-30 min)

**Responsable**: Tech Lead

#### Actividades:

1. **Revisión de dependencias externas**
   - Confirmar con DevOps: "¿Necesitamos algún recurso de infra?"
   - Confirmar con Diseño: "¿Todos los diseños están listos?"
   - Confirmar con Producto: "¿Hay alguna validación de negocio pendiente?"

2. **Distribución inicial de trabajo**
   - Developers toman sus primeras tasks
   - Tech Lead asegura que no hay overlaps o gaps

3. **Confirmation de Sprint Goal**
   - Re-leer el Sprint Goal
   - **Pregunta**: *"¿Si completamos todo esto, cumplimos el goal?"*

#### Entregable:
- **Sprint Plan** documentado y compartido en Slack/Confluence

---

### Post-Planning: Actualización de Herramientas

- [ ] Jira/Linear: Sprint creado con todas las stories y tasks
- [ ] Confluence/Notion: Sprint Goal documentado
- [ ] Slack: Mensaje en #engineering con Sprint Goal y highlights
- [ ] Calendario: Invites para Sprint Review y Retrospective (final de sprint)

---

### Métricas de Sprint Planning

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **Duración de Planning** | <4 horas | Time tracking |
| **Sprint Goal Achievement** | >80% | Goals met / total sprints |
| **Commitment vs Completed** | >85% | Story points completed / committed |
| **Planning Satisfaction** | >4/5 | Team survey post-planning |

---

## 🔍 Backlog Refinement

**Objetivo**: Preparar User Stories para futuros sprints, asegurar que están bien definidas, estimadas, y priorizadas.

### Formato

- **Frecuencia**: 2x por semana (Martes y Viernes)
- **Duración**: 1 hora por sesión
- **Horario**: Flexible (evitar lunes AM y viernes PM)
- **Ubicación**: Virtual OK
- **Facilitador**: Product Owner + Tech Lead

### Participantes

- **Obligatorio**: Product Owner, Tech Lead, 2-3 Senior Developers
- **Recomendado**: QA Engineer, UX Designer (para stories con diseño)
- **Opcional**: Full team (puede rotar)

---

### Estructura de Sesión de Refinement

#### 1. Review de Stories Candidatas (15 min)

**Actividad**: Product Owner presenta 3-5 User Stories para los próximos 2-3 sprints

**Información necesaria por story**:
- **Title**: ¿Qué queremos lograr?
- **User Story**: "Como [rol], quiero [acción], para [beneficio]"
- **Context**: ¿Por qué es importante? (business case)
- **Acceptance Criteria**: ¿Cómo sabemos que está hecho?

**Ejemplo**:
```
Title: Login con Google OAuth

User Story:
Como usuario registrado,
quiero poder hacer login con mi cuenta de Google,
para no tener que recordar otra contraseña.

Context:
60% de nuestros usuarios usan Gmail. Competidores ofrecen social login.
Puede aumentar conversión de signup en 15-20% según benchmarks.

Acceptance Criteria:
- [ ] Botón "Continuar con Google" visible en página de login
- [ ] OAuth flow completo (redirect, consent, callback)
- [ ] Crear usuario automáticamente si no existe
- [ ] Linking con cuenta existente si email ya registrado
- [ ] Error handling si Google rechaza
- [ ] Analytics event "login_google_success" y "login_google_failed"
```

---

#### 2. Discusión Técnica (30 min)

**Actividad**: Equipo técnico hace preguntas, identifica edge cases, propone soluciones

**Preguntas típicas**:
- ¿Qué pasa si el email de Google ya existe en nuestra DB con password?
- ¿Soportamos Google Workspace (enterprise accounts)?
- ¿Qué permisos pedimos a Google (solo email, o también profile picture)?
- ¿Qué pasa si el usuario revoca acceso en Google después?
- ¿Necesitamos refresh tokens?

**Resultado**:
- Acceptance Criteria actualizados con edge cases
- Identificación de dependencias técnicas
- Boceto de solución técnica (no detallada, solo high-level)

---

#### 3. Estimación (10 min)

**Método**: Planning Poker (Fibonacci: 1, 2, 3, 5, 8, 13, 21)

**Proceso**:
1. Equipo discute brevemente (2min)
2. Cada developer vota simultáneamente (muestra su carta)
3. Si hay consenso (+/- 1 point) → esa es la estimación
4. Si hay divergencia (ej: algunos votan 3, otros votan 8):
   - Los extremos explican su razonamiento
   - Re-votar
   - Máx 2 rondas, luego tomar la mediana

**Qué mide Story Points**:
- **Complejidad** técnica
- **Effort** (tiempo de desarrollo)
- **Incertidumbre** (unknowns, riesgos)

**Escala de referencia**:
- **1 point**: Cambio trivial, <2h (ej: cambiar un texto, fix typo)
- **2 points**: Small task, 2-4h (ej: añadir un campo a un form)
- **3 points**: Small story, 4-8h (ej: nuevo endpoint simple)
- **5 points**: Medium story, 1-2 días (ej: CRUD completo)
- **8 points**: Large story, 2-3 días (ej: OAuth integration)
- **13 points**: Very large, 3-5 días (ej: dashboard completo)
- **21+ points**: Epic, necesita descomponerse

**Si una story es >13 points → Romperla en stories más pequeñas**

---

#### 4. Priorización (5 min)

**Responsable**: Product Owner (decisión final)

**Frameworks**:

- **MoSCoW**:
  - **Must have**: Crítico para el negocio, no negociable
  - **Should have**: Importante pero puede esperar 1 sprint
  - **Could have**: Nice to have
  - **Won't have**: Fuera de scope

- **RICE** (usado por PM para priorizar antes de Refinement):
  - **Reach**: ¿Cuántos usuarios impacta?
  - **Impact**: ¿Qué tan grande es el beneficio? (1-5)
  - **Confidence**: ¿Qué tan seguros estamos? (%)
  - **Effort**: ¿Cuánto cuesta implementar? (story points)
  - **Score**: (Reach × Impact × Confidence) / Effort

**Resultado**: Stories ordenadas en el backlog por prioridad

---

### Definition of Ready (DoR)

Una User Story está **ready** para Sprint Planning cuando cumple:

- [ ] **Título claro** que describe el valor
- [ ] **User Story** en formato "Como X quiero Y para Z"
- [ ] **Acceptance Criteria** específicos y testables
- [ ] **Diseños** disponibles (si aplica)
- [ ] **Estimación** (story points) asignada
- [ ] **Dependencias** identificadas y resueltas
- [ ] **Prioridad** asignada por Product Owner
- [ ] **Sin blockers** conocidos

**Regla**: Solo stories que cumplen DoR pueden entrar en Sprint Planning.

---

### Métricas de Backlog Refinement

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **Stories Ready** | 2-3 sprints adelante | Count de stories con DoR |
| **Refinement Time** | <10% del tiempo del equipo | Hours en refinement / total hours |
| **Re-work Rate** | <10% | Stories que vuelven a refinar / total |
| **Team Participation** | >70% del team | Attendees / team size |

---

## 🎉 Sprint Review

**Objetivo**: Demostrar el trabajo completado en el sprint, obtener feedback de stakeholders, validar que cumple expectativas.

### Formato

- **Frecuencia**: Cada 2 semanas (fin de sprint)
- **Duración**: 1 hora
- **Horario**: Jueves 3:00 PM - 4:00 PM (penúltimo día del sprint)
- **Ubicación**: Presencial (recomendado) o Virtual
- **Facilitador**: Product Owner

### Participantes

- **Obligatorio**: Product Owner, Development Team, Tech Lead
- **Recomendado**: Stakeholders (PM, Diseño, Marketing, Sales, Customer Support), Engineering Manager
- **Opcional**: Executives (CEO, CTO) para demos importantes

---

### Estructura de Sprint Review

#### 1. Intro & Sprint Goal Recap (5 min)

**Responsable**: Product Owner

**Contenido**:
- Bienvenida y gracias por asistir
- Re-leer el Sprint Goal
- Context: ¿Qué intentamos lograr en este sprint?

**Ejemplo**:
> "El Sprint Goal era completar el flujo de checkout para usuarios móviles. Hoy vamos a demostrar cómo los usuarios pueden ahora comprar productos desde su teléfono en <30 segundos."

---

#### 2. Demos de Features Completadas (40 min)

**Responsable**: Developers (cada uno demo su feature)

**Formato**:
- **Live demo** (no slides) en ambiente de staging o producción
- **Mostrar el flujo completo** desde la perspectiva del usuario
- **Highlight business value**: ¿Qué problema resuelve?
- **5-7 minutos** por feature

**Ejemplo de buena demo**:
```
Developer: "Voy a demostrar el login con Google que implementamos."

1. [Abre app móvil] "El usuario abre la app y va a login."
2. [Click en botón] "Ahora ve el botón 'Continuar con Google'."
3. [OAuth flow] "Google le pide permiso para compartir su email."
4. [Redirect back] "Y automáticamente está logged in, sin crear password."
5. [Muestra perfil] "Su foto de perfil de Google se importó también."

Esta feature nos ahorra 3 pasos en el signup, lo que según research puede aumentar conversión en 15%.

¿Preguntas?"
```

**Reglas para demos**:
- ✅ Mostrar features **completadas** (100% done, en staging/prod)
- ✅ Demo desde **perspectiva del usuario final**
- ✅ Celebrar el logro del equipo
- ❌ No mostrar work in progress
- ❌ No entrar en detalles técnicos (eso es para otra reunión)
- ❌ No hacer excusas si algo no salió ("hubiera sido mejor si...")

---

#### 3. Features NO Completadas (5 min)

**Responsable**: Product Owner + Tech Lead

**Contenido**:
- ¿Qué stories no se completaron? (sin drama, solo facts)
- ¿Por qué? (blocker, subestimación, scope creep, etc.)
- ¿Se moverán al próximo sprint o se re-priorizarán?

**Ejemplo**:
> "Teníamos 3 stories planeadas: Login con Google, Login con Facebook, y Password Recovery. Completamos Login con Google. Login con Facebook se movió al próximo sprint porque descubrimos que Facebook cambió su API la semana pasada. Password Recovery se va a re-priorizar más abajo porque no es tan urgente."

---

#### 4. Feedback & Q&A (10 min)

**Responsable**: Product Owner (facilita)

**Actividad**:
- Stakeholders dan feedback sobre las demos
- Preguntas de clarificación
- Sugerencias de mejoras

**Capturar feedback**:
- Product Owner toma notas
- Feedback → Backlog (como nuevas stories o bugs)
- No commitments en vivo (evaluar después)

**Preguntas típicas de stakeholders**:
- "¿Esto ya está en producción?" → Sí/No, cuándo se va a deployar
- "¿Podemos cambiar el color del botón?" → Se anota, se evalúa prioridad después
- "¿Soporta modo oscuro?" → Se aclara el scope, se anota si es nuevo requerimiento

---

### Formato Alternativo: Sprint Review + Showcase

Para equipos con múltiples stakeholders externos:

**Sprint Review Interno** (45min):
- Solo equipo de Producto, Desarrollo, Diseño, DevOps
- Demos más técnicas, Q&A profundo

**Product Showcase** (30min):
- Stakeholders externos (Marketing, Sales, Executives)
- Demos más orientadas a negocio, menos técnicas
- Frecuencia: Mensual (cada 2 sprints) en vez de cada sprint

---

### Métricas de Sprint Review

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **Sprint Goal Achievement** | >80% | Goals met / total sprints |
| **Stakeholder Attendance** | >60% | Attendees / invited |
| **Feedback Items Captured** | >5 per review | Items added to backlog |
| **Review Satisfaction** | >4/5 | Stakeholder survey |

---

## 🔄 Sprint Retrospective

**Objetivo**: Reflexionar sobre el sprint pasado, identificar qué funcionó bien y qué se puede mejorar, crear action items para mejora continua.

### Formato

- **Frecuencia**: Cada 2 semanas (fin de sprint)
- **Duración**: 1 hora
- **Horario**: Viernes 2:00 PM - 3:00 PM (último día del sprint, **después** de Sprint Review)
- **Ubicación**: Presencial (muy recomendado) o Virtual
- **Facilitador**: Scrum Master / Tech Lead / Engineering Manager

### Participantes

- **Obligatorio**: Development Team (todos), Tech Lead, QA
- **Recomendado**: Product Owner, UX/UI Designer
- **Opcional**: DevOps (si hay issues de infra)
- **No invitar**: Stakeholders externos, Executives (debe ser espacio seguro)

---

### Principios de la Retrospective

1. **Espacio seguro**: Lo que se dice en retro, se queda en retro
2. **Sin culpa**: Enfocarse en procesos, no en personas
3. **Todos participan**: Cada voz importa
4. **Accionable**: No solo quejarse, sino proponer soluciones
5. **Time-boxed**: Respetar el tiempo (1 hora estricto)

---

### Estructura de Retrospective

#### 1. Set the Stage (5 min)

**Responsable**: Facilitador

**Actividad**: Crear ambiente seguro y positivo

**Opciones**:
- **Check-in personal**: Cada persona comparte cómo se siente (1 palabra o emoji)
- **Prime Directive**: Leer en voz alta:
  > "Asumimos que todos hicieron el mejor trabajo posible, dado lo que sabían en ese momento, sus habilidades, los recursos disponibles, y la situación."

**Objetivo**: Establecer que esto no es "buscar culpables", sino mejorar juntos

---

#### 2. Gather Data (15 min)

**Responsable**: Todo el equipo

**Método**: Retrospective board (Miro, Mural, post-its físicos, o Retrium)

**Columnas**:
1. **😊 What Went Well** - Cosas positivas que queremos mantener
2. **😟 What Didn't Go Well** - Problemas, frustraciones, cosas que no funcionaron
3. **💡 Ideas / Experiments** - Sugerencias para mejorar

**Proceso**:
1. **Silent brainstorming** (5-7min): Cada persona escribe sus notas en post-its
   - Ser específico (no "comunicación mala", sino "no supe que el endpoint cambió hasta que mi PR falló")
   - Una idea por post-it
2. **Sharing** (5-8min): Cada persona comparte brevemente sus notas (1 min cada uno)
3. **Grouping** (2-3min): Agrupar temas similares

**Ejemplo de notas**:

**What Went Well**:
- "El nuevo CI/CD pipeline redujo tiempo de deploy de 30min a 10min ✅"
- "Pair programming con Sarah para OAuth fue muy productivo 👍"
- "Completamos el Sprint Goal por 2do sprint consecutivo 🎉"

**What Didn't Go Well**:
- "Perdimos 4 horas por staging DB down el miércoles 😞"
- "Descubrimos bug crítico 1 día antes de release 🐛"
- "Refinement se extendió a 1.5h (target era 1h) ⏰"

**Ideas**:
- "Propongo hacer smoke tests automáticos en staging cada mañana"
- "Podemos hacer code freeze 2 días antes de release para full QA"

---

#### 3. Generate Insights (20 min)

**Responsable**: Facilitador + Equipo

**Actividad**: Discutir los temas más importantes

**Proceso**:
1. **Dot voting** (3min): Cada persona tiene 3 votos para poner en los temas más importantes
2. **Discusión** (15min): Discutir los top 3-5 temas con más votos

**Técnica de facilitación: 5 Whys**

Si un problema es recurrente, usar "5 Whys" para llegar a la raíz:

**Ejemplo**:
- **Problema**: "Bug crítico 1 día antes de release"
- **Why 1**: ¿Por qué descubrimos el bug tan tarde? → No testeamos antes
- **Why 2**: ¿Por qué no testeamos antes? → QA empezó testing 2 días antes de release
- **Why 3**: ¿Por qué QA empezó tan tarde? → Devs no hicieron code freeze a tiempo
- **Why 4**: ¿Por qué no hubo code freeze? → No está en el calendario como regla
- **Why 5**: ¿Por qué no es una regla? → Nunca lo formalizamos
- **Root cause**: Falta de proceso de code freeze definido

**Solución potencial**: Agregar code freeze 3 días antes de release al proceso

---

#### 4. Decide What to Do (15 min)

**Responsable**: Equipo (consenso)

**Actividad**: Crear 2-3 **action items** concretos para el próximo sprint

**Criterios para buenos action items**:
- ✅ **Específico**: No "mejorar comunicación", sino "crear Slack channel #api-changes para notificar breaking changes"
- ✅ **Accionable**: Algo que podemos empezar la próxima semana
- ✅ **Medible**: Cómo sabemos si funcionó
- ✅ **Owned**: Una persona responsable (no "el equipo")
- ✅ **Time-boxed**: Cuándo lo vamos a hacer

**Template de Action Item**:
```
Action Item: [Qué vamos a hacer]
Owner: [Persona responsable]
Due Date: [Cuándo]
Success Metric: [Cómo medimos éxito]
```

**Ejemplos de buenos action items**:

```
Action Item: Implementar smoke tests automáticos en staging
Owner: @john
Due Date: Próximo sprint (2 semanas)
Success Metric: 0 outages de staging descubiertos manualmente
```

```
Action Item: Agregar code freeze 3 días antes de release al calendario de sprint
Owner: @tech-lead
Due Date: Esta semana
Success Metric: 0 bugs críticos last-minute en próximos 2 releases
```

**⚠️ Limitación importante**: Máximo 2-3 action items por retro
- Si intentamos mejorar 10 cosas, no mejoramos ninguna
- Better done than perfect

---

#### 5. Close Retrospective (5 min)

**Responsable**: Facilitador

**Actividad**:
- Recap de los action items
- Asignar owner a cada uno
- Agregar a Jira/Linear como tasks
- **Feedback sobre la retro** (meta): ¿Fue útil? ¿Cómo mejorarla?

**Check-out**: Cada persona comparte 1 palabra sobre cómo se siente saliendo de la retro

---

### Formatos Alternativos de Retrospective

Cambiar el formato cada 2-3 sprints para mantener frescura:

#### 1. Start, Stop, Continue

**Columnas**:
- **Start**: Cosas que deberíamos empezar a hacer
- **Stop**: Cosas que deberíamos dejar de hacer
- **Continue**: Cosas que funcionan y queremos mantener

#### 2. Sailboat Retrospective

**Metáfora de un velero**:
- **Wind (viento)**: Qué nos impulsa hacia adelante (enablers)
- **Anchor (ancla)**: Qué nos frena (impedimentos)
- **Rocks (rocas)**: Riesgos en el horizonte
- **Island (isla)**: Nuestro objetivo (Sprint Goal)

#### 3. Mad, Sad, Glad

**Emociones**:
- **Mad** 😡: Cosas que me frustran
- **Sad** 😢: Cosas que me decepcionan
- **Glad** 😊: Cosas que me alegran

#### 4. Starfish Retrospective

**5 columnas**:
- **Keep Doing**: Mantener
- **More Of**: Hacer más
- **Start Doing**: Empezar
- **Less Of**: Hacer menos
- **Stop Doing**: Dejar de hacer

---

### Métricas de Retrospective

| Métrica | Target | Cómo Medir |
|---------|--------|------------|
| **Action Items Completion** | >80% | Completed / total action items |
| **Team Participation** | 100% | Everyone spoke in retro |
| **Retro Satisfaction** | >4/5 | Anonymous survey post-retro |
| **Repeat Problems** | Trending down | Same issue appears <2 retros |

---

## 🎭 Ceremonias Adicionales por Equipo

### Equipo de Desarrollo

- **Tech Talks** (mensual, 1h): Developers comparten learnings técnicos
- **Code Review Sessions** (semanal, 30min): Revisar PR complejo juntos
- **Architecture Review** (as needed): Para features complejas, con Solution Architect

### Equipo de DevOps

- **Platform Review** (semanal, 1h): Revisar métricas de plataforma, SLOs
- **Incident Postmortem** (dentro de 48h de incidente): Analizar incidentes P0/P1
- **On-call Handoff** (semanal): Transferir contexto entre on-calls

### Equipo de Producto

- **Discovery Workshop** (bi-semanal, 2h): Explorar nuevas oportunidades
- **Roadmap Review** (mensual, 2h): Revisar y ajustar roadmap con stakeholders
- **User Research Shareout** (bi-semanal, 30min): Compartir insights de research

### Equipo de Diseño

- **Design Critique** (2x/semana, 1h): Feedback estructurado sobre diseños WIP
- **Design System Sync** (semanal, 30min): Evolución del design system
- **Stakeholder Design Review** (semanal, 1h): Presentar diseños a PM/Eng leads

### Equipo de Arquitectura

- **Architecture Forum** (mensual, 2h): Discutir decisiones arquitectónicas mayores
- **ADR Review** (as needed): Revisar Architecture Decision Records
- **Tech Radar Update** (trimestral): Actualizar tecnologías recomendadas

---

## 📊 Métricas Generales de Ceremonias

| Métrica | Target | Acción si bajo target |
|---------|--------|----------------------|
| **On-Time Start Rate** | >90% | Recordatorio 5min antes, cultura de puntualidad |
| **Attendance Rate** | >85% | 1:1 con quienes faltan frecuentemente |
| **Time-box Adherence** | >80% | Facilitador más estricto, parking lot para tangents |
| **Ceremony Satisfaction** | >4/5 | Survey trimestral, ajustar formato |

---

## 🔗 Links Relacionados

- [Workflows](../workflows/README.md) - Procesos inter-equipos
- [Equipos](../equipos/README.md) - Estructura organizacional
- [Comunicación](../comunicacion/README.md) - Estrategia de comunicación
- [Scrum Guide](https://scrumguides.org/) - Guía oficial de Scrum

---

**Última actualización**: Enero 2025  
**Mantenido por**: Engineering Manager + Scrum Masters / Tech Leads