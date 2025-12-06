# Guía de Contribución

Este documento explica cómo contribuir y mantener actualizada la documentación del equipo DevOps.

## 🎯 Propósito

Esta guía asegura que toda la documentación se mantenga:
- **Actualizada**: Refleja la realidad actual del equipo
- **Consistente**: Sigue formatos y estándares uniformes
- **Accesible**: Fácil de encontrar y entender
- **Útil**: Proporciona valor real al equipo

## 📝 Proceso de Contribución

### 1. Identificar Necesidad de Cambio

Los cambios pueden surgir de:
- Procesos que han evolucionado
- Nuevas herramientas adoptadas
- Feedback del equipo
- Onboarding de nuevos miembros
- Post-mortems
- Auditorías de documentación

### 2. Crear Branch

```bash
# Clonar el repositorio
git clone https://github.com/[org]/lab-laoz-devops-team.git
cd lab-laoz-devops-team

# Crear branch descriptivo
git checkout -b update/[descripción-breve]

# Ejemplos:
git checkout -b update/add-sre-runbook
git checkout -b fix/outdated-raci-matrix
git checkout -b docs/new-tool-documentation
```

### 3. Hacer Cambios

#### Tipos de Cambios

**Actualización Menor** (typos, formatting, links)
- No requiere revisión extensa
- Puede mergearse con una aprobación

**Actualización Significativa** (procesos, roles, responsabilidades)
- Requiere revisión del equipo
- Puede requerir discusión en meeting
- Mínimo 2 aprobaciones

**Nueva Documentación**
- Seguir templates existentes
- Asegurar que está en la sección correcta
- Actualizar índices y enlaces

#### Estándares de Formato

**Markdown**
- Usar Markdown para todos los documentos
- Headers: `#` para nivel 1, `##` para nivel 2, etc.
- Listas: `-` para bullets, `1.` para numeradas
- Code blocks: Triple backticks con lenguaje

**Estructura**
```markdown
# Título Principal

## Sección 1

### Subsección

Contenido...

## Sección 2

### Subsección

Contenido...

---

**Última actualización**: [Fecha]
```

**Convenciones de Nombres**
- Archivos: `kebab-case.md` (ej: `incident-management.md`)
- Directorios: `kebab-case` (ej: `post-mortems`)
- No usar espacios en nombres de archivos

### 4. Commit Changes

```bash
# Stage changes
git add .

# Commit con mensaje descriptivo
git commit -m "tipo: descripción breve

Explicación más detallada si es necesario.

Closes #issue-number (si aplica)"
```

**Tipos de Commit**:
- `docs:` - Cambios de documentación
- `update:` - Actualización de contenido existente
- `fix:` - Corrección de errores
- `add:` - Nueva documentación
- `remove:` - Eliminar documentación obsoleta

**Ejemplos**:
```bash
git commit -m "docs: add SRE runbook for API service"

git commit -m "update: refresh RACI matrix with new roles

- Added Security Engineer responsibilities
- Updated Platform Engineer ownership
- Clarified DevOps Lead escalation paths"

git commit -m "fix: correct broken links in tools documentation"
```

### 5. Push y Crear Pull Request

```bash
# Push branch
git push origin update/[descripción-breve]
```

En GitHub:
1. Ir al repositorio
2. Click en "Compare & pull request"
3. Llenar template de PR:

```markdown
## Descripción
[Qué cambios se hicieron y por qué]

## Tipo de Cambio
- [ ] Actualización menor (typo, link, formato)
- [ ] Actualización significativa (proceso, rol, responsabilidad)
- [ ] Nueva documentación
- [ ] Eliminación de contenido obsoleto

## Checklist
- [ ] He seguido los estándares de formato
- [ ] He actualizado los índices relevantes
- [ ] He probado todos los links
- [ ] He actualizado la fecha de "última actualización"
- [ ] He notificado a stakeholders relevantes (si aplica)

## Reviewers Sugeridos
@[username1] @[username2]

## Contexto Adicional
[Información adicional si es necesaria]
```

### 6. Code Review

**Responsabilidades del Reviewer**:
- Verificar exactitud técnica
- Asegurar claridad y comprensibilidad
- Validar formato y estándares
- Sugerir mejoras

**Timeframe**:
- Actualizaciones menores: 1 día laboral
- Actualizaciones significativas: 2-3 días laborales
- Nueva documentación: 1 semana

**Aprobaciones Requeridas**:
- Menor: 1 aprobación
- Significativa: 2 aprobaciones (incluyendo DevOps Lead)
- Nueva: 2 aprobaciones

### 7. Merge

Una vez aprobado:
```bash
# Opción 1: Squash and merge (preferido para cambios pequeños)
# Opción 2: Merge commit (para cambios grandes con historia relevante)

# Después de merge, eliminar branch
git branch -d update/[descripción-breve]
git push origin --delete update/[descripción-breve]
```

## 📂 Estructura de Directorios

```
lab-laoz-devops-team/
├── README.md                    # Punto de entrada principal
├── roles/                       # Definiciones de roles
│   ├── README.md
│   ├── devops-lead.md
│   ├── sre.md
│   └── ...
├── procesos/                    # Procesos y workflows
│   ├── README.md
│   ├── incident-management.md
│   └── ...
├── responsabilidades/           # Matrices RACI
│   └── RACI.md
├── herramientas/               # Catálogo de herramientas
│   └── README.md
├── metricas/                   # KPIs y métricas
│   └── README.md
├── plantillas/                 # Templates reutilizables
│   ├── README.md
│   ├── post-mortem-template.md
│   └── ...
└── CONTRIBUTING.md             # Esta guía
```

## 🔍 Auditoría de Documentación

### Quarterly Review (Trimestral)

**Owner**: DevOps Lead  
**Participantes**: Todo el equipo

**Checklist**:
- [ ] Revisar cada documento para exactitud
- [ ] Verificar que links funcionen
- [ ] Identificar documentación obsoleta
- [ ] Buscar gaps en cobertura
- [ ] Actualizar fechas de "última actualización"
- [ ] Recopilar feedback del equipo

**Proceso**:
1. DevOps Lead crea issue para audit
2. Asignar secciones a miembros del equipo
3. Cada miembro revisa su sección (1 semana)
4. Crear PRs con updates necesarios
5. Review en team meeting
6. Merge cambios aprobados

### Continuous Improvement

**Cuando documentar algo nuevo**:
- ✅ Nuevo proceso implementado
- ✅ Nueva herramienta adoptada
- ✅ Cambio significativo en responsabilidades
- ✅ Lesson learned de post-mortem
- ✅ Pregunta repetida >3 veces (documentar respuesta)

**Señales de documentación obsoleta**:
- ⚠️ Procesos que ya no se siguen
- ⚠️ Herramientas deprecadas
- ⚠️ Roles que han cambiado
- ⚠️ Links rotos
- ⚠️ Información contradictoria

## 📋 Templates Disponibles

Al crear nueva documentación, usar templates en `/plantillas/`:

- **Post-Mortem**: `/plantillas/post-mortem-template.md`
- **Runbook**: `/plantillas/runbook-template.md`
- **Change Request**: `/plantillas/change-request-template.md`
- **ADR**: `/plantillas/adr-template.md`
- **Onboarding**: `/plantillas/onboarding-checklist.md`

## ✅ Checklist para Nueva Documentación

Antes de crear PR:

- [ ] Contenido es exacto y verificado
- [ ] Sigue template apropiado (si aplica)
- [ ] Formato Markdown correcto
- [ ] Headers y estructura lógica
- [ ] Code blocks tienen syntax highlighting
- [ ] Todos los links funcionan
- [ ] Imágenes/diagramas incluidos si es necesario
- [ ] Actualizado índice de sección
- [ ] Actualizado README principal si es necesario
- [ ] Fecha de "última actualización" incluida
- [ ] Reviewed for sensitive information (no secrets!)

## 🚫 Qué NO Documentar Aquí

Este repositorio NO debe contener:

- ❌ Secretos, passwords, API keys
- ❌ Información confidencial de clientes
- ❌ IP addresses o detalles de infraestructura sensibles
- ❌ Vulnerabilidades de seguridad sin remediar
- ❌ Información personal identificable (PII)
- ❌ Código fuente de aplicaciones (usar repos apropiados)

**Para información sensible**: Usar Confluence privado o sistemas de secrets management.

## 💡 Tips para Buena Documentación

### Claridad
- Usar lenguaje simple y directo
- Evitar jargon innecesario
- Definir acrónimos en primera mención
- Incluir ejemplos cuando sea posible

### Estructura
- Comenzar con overview/contexto
- Usar headers para organizar
- Bullets/listas para información scannable
- Secciones lógicas y bien organizadas

### Mantenibilidad
- Evitar duplicación (link a fuente única de verdad)
- Fechar documentos
- Indicar owner/contacto
- Versionar si es apropiado

### Usabilidad
- Incluir links a recursos relacionados
- Proporcionar comandos copy-paste ready
- Diagramas para conceptos complejos
- Screenshots cuando agregan valor

## 🙋 Obtener Ayuda

¿Dudas sobre cómo contribuir?

1. **Slack**: Preguntar en `#devops`
2. **Issue**: Crear issue en GitHub con pregunta
3. **1-on-1**: Hablar con DevOps Lead en próximo 1-on-1

## 📞 Contactos

- **Documentation Owner**: DevOps Lead
- **Preguntas**: Slack `#devops`
- **Reportar problemas**: GitHub Issues

---

## Changelog

| Fecha | Cambio | Autor |
|-------|--------|-------|
| 2025-12-05 | Versión inicial | [Tu nombre] |

---

**Gracias por contribuir a mantener nuestra documentación actualizada y útil!** 🎉
