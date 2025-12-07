# 🎯 Retrospective Action Items - Sistema de Accountability

## 📋 Resumen Ejecutivo

**Problema Crítico**: Los action items de las retrospectivas no tienen seguimiento consistente, resultando en pérdida de confianza del equipo en el proceso.

**Solución**: Sistema estructurado de accountability con owners claros, Definition of Done, timelines, tracking en Jira, y revisión semanal.

**Meta**: >70% de action items completados antes de la siguiente retro.

---

## 🚨 Por Qué Es Crítico

### Impacto de NO Tener Accountability

❌ **Pérdida de Confianza**

- Equipo deja de participar activamente en retros
- "Total, nunca se hace nada con esto"
- Cultura de retrospectivas se vuelve performativa

❌ **Mejora Continua Estancada**

- Problemas recurrentes nunca se resuelven
- Frustración acumulada del equipo
- Deuda de proceso crece sin control

❌ **Desperdicio de Tiempo**

- 1h de retro cada 2 semanas = 26h/año desperdiciadas
- Si multiplicamos por 5 equipos = 130h/año en ceremonias sin valor

### Beneficios del Sistema de Accountability

✅ **Confianza Restaurada**

- Equipo ve acción concreta post-retro
- Mayor engagement en identificar problemas
- Cultura de ownership colectivo

✅ **Mejora Continua Real**

- Problemas sistémicos se resuelven
- Velocidad y calidad mejoran gradualmente
- Team morale aumenta

✅ **Visibilidad Organizacional**

- Management puede ver investment en mejora de procesos
- Métricas claras de efectividad de retros

---

## 📝 Template: Action Item

```yaml
# Action Item #RETRO-2024-12-06-01

## Contexto
Descripción del problema identificado en la retro que motiva este action item.

## Action Item
[Descripción clara y accionable de lo que hay que hacer]

## Owner
- **Responsable Principal**: [Nombre - Rol]
- **Equipo**: [Desarrollo / DevOps / Producto / Diseño / Arquitectura]
- **Colaboradores**: [Opcional - otros involucrados]

## Definition of Done (DoD)
- [ ] Criterio específico #1 (medible)
- [ ] Criterio específico #2 (medible)
- [ ] Criterio específico #3 (medible)
- [ ] Documentación actualizada (si aplica)
- [ ] Equipo informado del cambio

## Timeline
- **Fecha Inicio**: YYYY-MM-DD
- **Fecha Target**: YYYY-MM-DD (antes de próxima retro)
- **Fecha Review**: YYYY-MM-DD (weekly check-in)

## Tracking
- **Jira Ticket**: [TEAM-XXX](link)
- **Status**: Not Started / In Progress / Blocked / Done
- **% Completado**: 0%

## Weekly Check-in (actualizar cada semana)

### Semana 1 (YYYY-MM-DD)
- Status:
- Progreso:
- Blockers:
- Next Steps:

### Semana 2 (YYYY-MM-DD)
- Status:
- Progreso:
- Blockers:
- Next Steps:

## Resultado Final
[Llenar al completar - qué se logró, qué impacto tuvo]

## Retrospective Review
[Llenar en la siguiente retro - el equipo considera esto resuelto?]
```

---

## 🔄 Proceso End-to-End

### Durante la Retrospective (T+0)

#### 1. Identificar Action Items (15 min finales)

**Facilitador**:

- Al final de retro, revisar temas discutidos
- Preguntar: "¿Qué acción concreta podemos tomar para mejorar X?"
- Limitar a **3-5 action items por retro** (más es inmanejable)

**Criterios de Buen Action Item**:

- ✅ **Specific**: "Documentar proceso de deploy" (no "mejorar docs")
- ✅ **Actionable**: Alguien puede empezar mañana
- ✅ **Impactful**: Resuelve un pain point real del equipo
- ✅ **Time-bound**: Completable en 1-2 semanas

**Antipatterns**:

- ❌ "Comunicarnos mejor" (demasiado vago)
- ❌ "Refactorizar toda la codebase" (demasiado grande)
- ❌ "Management debería darnos más recursos" (fuera de control del equipo)

#### 2. Asignar Ownership (En la retro misma)

**Proceso**:

1. Facilitador pregunta: "¿Quién puede liderar este action item?"
2. **El owner debe aceptar voluntariamente** (no asignar por decreto)
3. Si nadie se ofrece → el item no es lo suficientemente importante → descartarlo

**Owner Responsibilities**:

- ✅ Crear Jira ticket inmediatamente post-retro
- ✅ Definir DoD específico
- ✅ Identificar colaboradores si necesita ayuda
- ✅ Dar update semanal (30 seg en daily standup)
- ✅ Escalar si está bloqueado

**Backup Plan**:

- Si owner sale de vacaciones/deja el equipo → reasignar en daily standup
- Tech Lead es backup default si action item queda huérfano

#### 3. Definir DoD y Timeline (En la retro misma)

**Definition of Done**:

- Debe ser **binario** (hecho o no hecho, no "80% completado")
- Debe ser **verificable** por cualquier miembro del equipo
- Ejemplo bueno: "README.md tiene sección 'Deployment' con 5 pasos documentados + diagrama"
- Ejemplo malo: "Deployment está mejor documentado"

**Timeline**:

- Default: **Completar antes de próxima retro** (2 semanas)
- Si requiere >2 semanas → dividir en sub-items más pequeños
- Review semanal cada viernes en daily standup

---

### Post-Retrospective (T+0 a T+1 día)

#### Owner Actions (Dentro de 24h)

1. **Crear Jira Ticket**
   - Board: Team's board
   - Type: `Task` o `Process Improvement`
   - Label: `retro-action-item`
   - Priority: `High` (action items tienen prioridad sobre feature work)
   - Sprint: Current sprint (si hay capacidad) o siguiente
2. **Crear Markdown File**

   - Usar template arriba
   - Guardar en `ceremonias/retro-action-items/YYYY-MM-DD-{descripcion-corta}.md`
   - Linkear desde README.md de ceremonias

3. **Comunicar en Slack**

   ```
   📋 New Retro Action Item

   **Item**: Documentar proceso de deployment
   **Owner**: @andres.olarte
   **DoD**: README.md actualizado + diagrama en Confluence
   **Target**: Dec 20, 2024 (antes de próxima retro)
   **Jira**: TEAM-456

   Weekly updates every Friday en daily standup 🚀
   ```

---

### Durante el Sprint (T+1 día a T+14 días)

#### Weekly Check-in (Cada Viernes en Daily Standup)

**Formato (30-60 segundos por action item)**:

Owner:

```
Retro Action Item Update:
- Item: [nombre corto]
- Status: In Progress
- Progress: Documenté 3 de 5 pasos del deployment
- Blockers: Ninguno
- Next: Terminar últimos 2 pasos + crear diagrama
- ETA: On track para Dec 20
```

**Si está bloqueado**:

```
- Status: Blocked ⚠️
- Blocker: Necesito acceso a AWS prod para documentar último paso
- Help needed: @devops.lead puede darme read-only access?
- Risk: Puede retrasar 3 días
```

**Escalation Path** (si owner no da update):

1. Día 1: Tech Lead ping en Slack
2. Día 3: Tech Lead reasigna o marca como dropped
3. En próxima retro: Discutir por qué el item murió

#### Sprint Planning Consideration

**Action Items tienen prioridad**:

- Reserve **10-20% de sprint capacity** para action items
- Si hay conflicto entre feature work y action items → action items ganan
- Rationale: Mejorar procesos = mayor velocidad long-term

**Tracking en Jira**:

- Action items aparecen en sprint board
- Daily standup: Revisar progress visualmente
- Burndown chart incluye action items

---

### En la Siguiente Retrospective (T+14 días)

#### Review de Action Items Previos (Primeros 10 min de retro)

**Facilitador presenta**:

```markdown
## Action Items de Retro Anterior (Nov 22)

### ✅ Completados (3/5 = 60%)

1. ✅ **Documentar proceso de deployment**

   - Owner: Andres Olarte
   - Result: README.md actualizado + diagrama en Confluence
   - Impact: 2 nuevos devs pudieron hacer deploy sin ayuda

2. ✅ **Automatizar smoke tests pre-demo**

   - Owner: Maria Garcia
   - Result: Script en CI/CD que corre antes de Sprint Review
   - Impact: 0 demos rotos en últimas 2 semanas (antes: 50% broken)

3. ✅ **Definir Definition of Ready para user stories**
   - Owner: Product Owner
   - Result: Checklist en Jira + doc en Confluence
   - Impact: 0 stories sin AC en último sprint planning

### ❌ No Completados (2/5 = 40%)

4. ❌ **Reducir tiempo de build de 20min a 10min**

   - Owner: DevOps Lead
   - Status: 30% done (build ahora es 16min)
   - Blocker: Docker layer caching requiere upgrade de CI runners ($$$)
   - Decision: Carry over a siguiente sprint, escalar budget a VP Eng

5. ❌ **Crear onboarding guide para nuevos devs**
   - Owner: Tech Lead
   - Status: Dropped
   - Reason: Owner salió de vacaciones, nadie tomó ownership
   - Decision: Re-open este action item? O no es prioritario?
```

**Discusión del Equipo** (5 min):

- ¿Los items completados tuvieron impacto real?
- ¿Por qué fallaron los no completados?
- ¿Deberíamos re-intentarlos o dejarlos ir?

**Meta de Éxito**: >70% completion rate

- Si <50% → equipo está sobre-comprometido, reducir a 2-3 action items
- Si >90% → equipo podría tomar más ambiciosos action items

---

## 📊 Métricas de Accountability

### Métricas Primarias

1. **Completion Rate**

   - Fórmula: `(Items completados / Total items) * 100`
   - Target: >70%
   - Tracking: Por sprint, rolling average de 6 sprints

2. **Time to Complete**

   - Fórmula: Días desde asignación hasta completion
   - Target: <14 días (antes de siguiente retro)
   - Red flag: >20 días

3. **Carry-over Rate**
   - Fórmula: `(Items movidos a siguiente sprint / Total) * 100`
   - Target: <20%
   - Red flag: >40% (equipo está sobre-comprometido)

### Métricas Secundarias

4. **Action Item Velocity**

   - Cuántos action items puede completar el equipo por sprint
   - Usar para capacity planning
   - Typical: 3-5 items/sprint para equipo de 5-7 personas

5. **Impact Score** (Subjetivo, votación del equipo)

   - En siguiente retro: "Del 1-5, ¿cuánto impacto tuvo este action item?"
   - Promedio >3.5 = buenos action items
   - Promedio <2.5 = estamos resolviendo problemas equivocados

6. **Blocker Frequency**
   - % de action items que se bloquean
   - Target: <20%
   - Si >40% → action items dependen demasiado de externos

### Dashboard (Confluence o Jira Dashboard)

```markdown
## Retro Action Items - Q4 2024

| Sprint | Items Created | Completed | Completion % | Avg Days to Complete |
| ------ | ------------- | --------- | ------------ | -------------------- |
| S23    | 5             | 4         | 80%          | 10 days              |
| S24    | 4             | 3         | 75%          | 12 days              |
| S25    | 5             | 2         | 40% ⚠️       | 18 days              |
| S26    | 3             | 3         | 100% 🎉      | 8 days               |

**Trends**:

- ✅ S26 had 100% completion (reduced scope to 3 items)
- ⚠️ S25 was overcommitted (5 items too many)
- 📈 Avg completion rate: 73% (above 70% target)
```

---

## 🎭 Roles y Responsabilidades

### Facilitador de Retrospectiva

**Durante Retro**:

- ✅ Limitar a 3-5 action items (rechazar vagos o inaccionables)
- ✅ Asegurar que cada item tenga owner voluntario
- ✅ Definir DoD específico antes de cerrar retro
- ✅ Timebox: Max 15min para action items (no toda la retro)

**Post-Retro**:

- ✅ Verificar que owners crearon Jira tickets (dentro de 24h)
- ✅ Agregar action items a tracking dashboard
- ✅ Comunicar en Slack #team-channel

**Próxima Retro**:

- ✅ Preparar review de action items previos (primeros 10min)
- ✅ Presentar métricas: completion rate, avg days to complete
- ✅ Facilitar discusión: ¿Por qué fallaron algunos items?

### Action Item Owner

**Inmediatamente Post-Retro** (<24h):

- ✅ Crear Jira ticket con label `retro-action-item`
- ✅ Crear markdown file en `ceremonias/retro-action-items/`
- ✅ Comunicar en Slack con DoD y timeline

**Durante Sprint**:

- ✅ Weekly update en Friday daily standup (30 seg)
- ✅ Escalar inmediatamente si bloqueado
- ✅ Actualizar Jira ticket status y % completado

**Al Completar**:

- ✅ Mover Jira ticket a Done
- ✅ Actualizar markdown con resultado y impacto
- ✅ Comunicar en Slack con screenshot/link a resultado
- ✅ Preparar mini-demo para siguiente retro (1-2 min)

### Tech Lead (Backup/Accountability Enforcer)

**Weekly Check-in Review**:

- ✅ Si owner no da update en Friday standup → ping en Slack
- ✅ Si bloqueado >3 días sin resolverse → escalar o reasignar
- ✅ Si item morirá → comunicar al equipo proactivamente

**Sprint Planning**:

- ✅ Reserve 10-20% de sprint capacity para action items
- ✅ Action items tienen prioridad sobre new features
- ✅ Bloquear time del owner si es necesario

**Metrics Tracking**:

- ✅ Actualizar dashboard cada fin de sprint
- ✅ Compartir trends con equipo en retro
- ✅ Proponer ajustes (ej: reducir # items si completion <50%)

### Equipo Completo

**En Retro**:

- ✅ Proponer action items accionables y específicos
- ✅ Ofrecerse como owner si genuinamente pueden ejecutar
- ✅ Votar en impacto de action items previos

**Durante Sprint**:

- ✅ Apoyar a owners si piden ayuda
- ✅ Remover blockers cuando sea posible
- ✅ Celebrar cuando action items se completan 🎉

---

## 🚀 Implementation Roadmap

### Sprint 1: Setup (2 semanas)

**Semana 1**:

- [ ] Tech Lead crea directorio `ceremonias/retro-action-items/`
- [ ] Facilitador presenta este documento en team meeting (15 min)
- [ ] Equipo revisa template y proceso
- [ ] Crear Jira label `retro-action-item`
- [ ] Setup dashboard básico en Confluence

**Semana 2**:

- [ ] En próxima retro: Aplicar proceso por primera vez
- [ ] Crear 3-5 action items usando template
- [ ] Owners crean Jira tickets y markdown files
- [ ] First weekly check-in en Friday standup

### Sprint 2-3: Iterate (4 semanas)

- [ ] Continuar weekly check-ins
- [ ] En retro de S2: Review de primeros action items
- [ ] Calcular completion rate y avg days to complete
- [ ] Ajustar proceso basado en feedback (ej: reducir # items si <50%)

### Sprint 4+: Steady State

- [ ] Proceso se vuelve hábito
- [ ] Completion rate >70% consistentemente
- [ ] Equipo confía en que action items se ejecutan
- [ ] Retrospectivas generan mejora continua real

---

## 🎯 Success Criteria

### Mes 1

- ✅ 100% de action items tienen owner asignado en la retro
- ✅ 100% de action items tienen Jira ticket creado <24h post-retro
- ✅ >50% completion rate (primera vez, target bajo)

### Mes 2-3

- ✅ >70% completion rate
- ✅ Weekly check-ins ocurren consistentemente
- ✅ Action items completados tienen impacto visible (avg score >3/5)

### Mes 4+

- ✅ >80% completion rate
- ✅ Team morale aumenta (survey de retros)
- ✅ Problemas recurrentes se resuelven (evidencia en retros)
- ✅ Equipo proactivamente propone action items (ownership culture)

---

## 🔗 Links Relacionados

- [Ceremonias: Retrospective](README.md#retrospective) - Ceremonia principal
- [Formatos de Retrospective](retro-formats.md) - Variedad de formatos para engagement
- [Análisis de Ceremonias](../responsabilidades/analisis-ceremonias.md) - Gap analysis completo
- [RACI: Ceremonias](../responsabilidades/RACI.md#ceremonias) - Responsabilidades por rol

---

## 📚 Antipatterns y Cómo Evitarlos

### ❌ Antipattern #1: Action Items Vagos

**Síntoma**: "Mejorar comunicación", "Ser más ágiles"

**Por Qué Falla**: No es accionable, no tiene DoD claro

**Solución**: Preguntar "¿Qué acción específica tomarías mañana para mejorar comunicación?"

- Ejemplo bueno: "Crear #incidents-updates channel y documentar escalation process"

### ❌ Antipattern #2: Demasiados Action Items

**Síntoma**: 8-10 action items por retro

**Por Qué Falla**: Equipo se sobre-compromete, ninguno se completa, frustración

**Solución**: Limitar a 3-5 items, priorizar por impacto

- Tech Lead debe rechazar items de baja prioridad

### ❌ Antipattern #3: Owners Asignados por Decreto

**Síntoma**: "Juan, tú te encargas de esto" (sin consultar)

**Por Qué Falla**: Juan no tiene ownership real, item muere silenciosamente

**Solución**: Preguntar "¿Quién puede liderar esto?" y esperar voluntario

- Si nadie se ofrece → item no es importante → descartarlo

### ❌ Antipattern #4: No Review en Siguiente Retro

**Síntoma**: Action items se crean pero nunca se revisan

**Por Qué Falla**: Equipo aprende que no hay accountability, deja de tomarlos en serio

**Solución**: Primeros 10min de TODA retro = review de action items previos

- Facilitador debe blocker este tiempo religiosamente

### ❌ Antipattern #5: Action Items = Feature Work

**Síntoma**: "Implementar feature X que quedó del backlog"

**Por Qué Falla**: Action items son para mejorar PROCESOS, no para sneakear features

**Solución**: Action items deben mejorar forma de trabajar, no output del trabajo

- Ejemplo correcto: "Documentar proceso de code review para reducir ciclo de 3 días a 1 día"

---

## 📞 FAQ

**P: ¿Qué pasa si un action item requiere >2 semanas?**

R: Dividirlo en sub-items más pequeños. Ejemplo:

- ❌ "Migrar toda la infra a Kubernetes" (6 meses)
- ✅ "Crear PoC de 1 microservice en K8s" (2 semanas)
- ✅ "Documentar migration path y costs" (1 semana)

**P: ¿Action items se estiman en story points?**

R: No necesariamente. Si ocupan sprint capacity, pueden estimarse, pero:

- Típicamente son tareas pequeñas (2-3 story points)
- Prioridad Alta por default
- Reserve 10-20% de sprint capacity en aggregate

**P: ¿Quién puede ser owner?**

R: Cualquier miembro del equipo, incluyendo PO, QA, Designer

- No solo devs
- Quien tiene el skill/contexto para ejecutar
- Debe aceptar voluntariamente

**P: ¿Qué pasa si owner sale de vacaciones mid-sprint?**

R:

1. Owner debe reasignar proactivamente antes de irse
2. Si no lo hace, Tech Lead reasigna en daily standup
3. Tech Lead es backup default si queda huérfano

**P: ¿Podemos tener action items fuera de retros?**

R: Sí, pero con precaución:

- Úsalos para quick wins obvios
- Pero mantén el rigor: owner, DoD, timeline, Jira ticket
- Review en siguiente retro igual

**P: ¿Cómo medimos impacto de un action item?**

R: En siguiente retro, equipo vota 1-5:

- 5 = Huge impact, problema crítico resuelto
- 3 = Moderate improvement
- 1 = No notamos diferencia

Avg >3.5 = buenos action items

---

**Versión**: 1.0
**Última Actualización**: 2024-12-06
**Owner**: Tech Lead + Retro Facilitator
**Review Cycle**: Trimestral
