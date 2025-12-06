# Equipo de Desarrollo

El equipo de desarrollo es responsable de construir, probar y mantener el software que entrega valor a los usuarios finales.

## 👥 Roles en el Equipo

### 🎨 [Frontend Developer](./frontend-developer.md)
Especialista en interfaces de usuario y experiencia del cliente.
- **Nivel**: Junior, Mid, Senior, Staff
- **Tecnologías**: React, Vue, Angular, TypeScript
- **Responsabilidad**: UI/UX implementation

### ⚙️ [Backend Developer](./backend-developer.md)
Especialista en lógica de negocio, APIs y bases de datos.
- **Nivel**: Junior, Mid, Senior, Staff
- **Tecnologías**: .NET, Node.js, Python, Java, Go
- **Responsabilidad**: Business logic, APIs, databases

### 🌐 [Full-Stack Developer](./fullstack-developer.md)
Desarrollador versátil con competencias en frontend y backend.
- **Nivel**: Mid, Senior, Staff
- **Tecnologías**: Stack completo (frontend + backend)
- **Responsabilidad**: End-to-end features

### 📱 [Mobile Developer](./mobile-developer.md)
Especialista en aplicaciones móviles nativas o híbridas.
- **Nivel**: Junior, Mid, Senior, Staff
- **Tecnologías**: React Native, Flutter, Swift, Kotlin
- **Responsabilidad**: Mobile apps

### 🎯 [Tech Lead](./tech-lead.md)
Líder técnico del equipo, balance entre código y coordinación.
- **Nivel**: Senior/Staff
- **Enfoque**: 30% código, 70% liderazgo técnico
- **Responsabilidad**: Decisiones técnicas, mentoría, arquitectura

### 👔 [Engineering Manager](./engineering-manager.md)
Manager de personas, enfocado en crecimiento del equipo.
- **Nivel**: Management track
- **Enfoque**: 0-10% código, 90% gestión de personas
- **Responsabilidad**: Hiring, performance, career growth

### 🧪 [QA Engineer](./qa-engineer.md)
Especialista en calidad, testing y automation.
- **Nivel**: Junior, Mid, Senior
- **Tecnologías**: Selenium, Cypress, Playwright, JMeter
- **Responsabilidad**: Test automation, quality assurance

## 📊 Estructura del Equipo

### Modelo Típico (Squad de 7 personas)

```
                    Tech Lead
                       │
        ┌──────────────┼──────────────┐
        │              │              │
    Frontend       Backend          QA
    (2 devs)       (3 devs)      (1 QA)
        │              │              │
        └──────────────┴──────────────┘
                       │
              Engineering Manager
              (gestión de personas)
```

### Variantes de Estructura

#### 1. Full-Stack Team
```yaml
Composición:
  - 1 Tech Lead
  - 5 Full-Stack Developers
  - 1 QA Engineer

Ventajas:
  - Máxima flexibilidad
  - Context switching reducido
  - Ownership completo

Ideal para:
  - Startups
  - Equipos pequeños
  - Productos web simples
```

#### 2. Especializado Frontend/Backend
```yaml
Composición:
  - 1 Tech Lead
  - 3 Frontend Developers
  - 3 Backend Developers
  - 1 QA Engineer

Ventajas:
  - Especialización profunda
  - Paralelización de trabajo
  - Expertise concentrado

Ideal para:
  - Aplicaciones complejas
  - Equipos medianos/grandes
  - Productos enterprise
```

#### 3. Feature Teams (Multi-squad)
```yaml
Estructura:
  Engineering Manager
  ├── Squad A (Product X)
  │   ├── Tech Lead
  │   ├── 5 Developers
  │   └── 1 QA
  ├── Squad B (Product Y)
  │   ├── Tech Lead
  │   ├── 5 Developers
  │   └── 1 QA
  └── Squad C (Platform)
      ├── Tech Lead
      ├── 5 Developers
      └── 1 QA

Ideal para:
  - Múltiples productos
  - Equipos 20+ personas
  - Autonomía por feature
```

## 🎯 Responsabilidades del Equipo

### Ownership Completo (You Build It, You Run It)

```yaml
Planificación:
  - Estimación de features
  - Refinement de historias
  - Sprint planning
  - Definición de done

Desarrollo:
  - Diseño técnico
  - Implementación
  - Code review
  - Pair programming
  - Testing (unit, integration)

Calidad:
  - Automated testing
  - Code quality (SonarQube)
  - Performance testing
  - Security scanning

Deployment:
  - Feature flags
  - Deployment a staging
  - Smoke testing
  - Deployment a producción

Operaciones:
  - Monitoreo de métricas
  - Respuesta a alertas
  - On-call rotation
  - Bug fixing
  - Performance optimization
```

## 📈 Career Path

### Individual Contributor (IC) Track

```
Junior Developer (IC1)
    ↓ (1-2 años)
Mid-level Developer (IC2)
    ↓ (2-3 años)
Senior Developer (IC3)
    ↓ (3-5 años)
Staff Engineer (IC4)
    ↓ (5+ años)
Principal Engineer (IC5)
    ↓ (8+ años)
Distinguished Engineer (IC6)
```

### Management Track

```
Senior Developer
    ↓
Tech Lead (híbrido)
    ↓
Engineering Manager
    ↓
Senior Engineering Manager
    ↓
Director of Engineering
    ↓
VP Engineering
    ↓
CTO
```

### Switching Tracks

Los desarrolladores pueden cambiar entre IC y Management track:
- **IC → Management**: Normalmente vía Tech Lead
- **Management → IC**: Vía Staff Engineer role
- **Reversible**: No hay penalización por cambiar

## 🛠️ Stack Tecnológico Típico

### Frontend
```yaml
Frameworks:
  - React 18+ (TypeScript)
  - Next.js 14+ (App Router)
  - Vue 3 + Vite
  - Angular 17+

State Management:
  - React Query / TanStack Query
  - Zustand / Jotai
  - Redux Toolkit (legacy)

Styling:
  - Tailwind CSS
  - CSS Modules
  - Styled Components

Testing:
  - Vitest / Jest
  - React Testing Library
  - Playwright / Cypress
```

### Backend
```yaml
Languages:
  - .NET 8 (C#)
  - Node.js 20 (TypeScript)
  - Python 3.11
  - Java 21
  - Go 1.22

Frameworks:
  - ASP.NET Core
  - NestJS / Express
  - FastAPI
  - Spring Boot
  - Gin

Databases:
  - PostgreSQL
  - Azure SQL
  - MongoDB
  - Redis

Testing:
  - xUnit / NUnit (.NET)
  - Jest / Vitest (Node)
  - pytest (Python)
  - JUnit (Java)
```

### Mobile
```yaml
Cross-platform:
  - React Native
  - Flutter
  
Native:
  - Swift (iOS)
  - Kotlin (Android)
  
Backend-as-a-Service:
  - Firebase
  - Supabase
  - AWS Amplify
```

## 📊 Métricas del Equipo

### DORA Metrics

```yaml
Deployment Frequency:
  Elite: Multiple deployments per day
  High: Once per day - once per week
  Medium: Once per week - once per month
  Low: Less than once per month

Lead Time for Changes:
  Elite: Less than 1 hour
  High: 1 day - 1 week
  Medium: 1 week - 1 month
  Low: 1 month - 6 months

Time to Restore Service:
  Elite: Less than 1 hour
  High: Less than 1 day
  Medium: 1 day - 1 week
  Low: 1 week - 1 month

Change Failure Rate:
  Elite: 0-15%
  High: 16-30%
  Medium: 31-45%
  Low: 46-60%
```

### Team Health Metrics

```yaml
Velocity:
  - Story points completados por sprint
  - Tendencia últimos 6 sprints
  - Predictibilidad (variance < 20%)

Code Quality:
  - Code coverage > 80%
  - Sonar quality gate: Pass
  - Technical debt ratio < 5%
  - Code duplication < 3%

Team Happiness:
  - NPS score mensual
  - Retrospective action items
  - Turnover rate < 10%/año
```

## 🔄 Ceremonias del Equipo

### Diarias
- **Daily Standup**: 15 min, 9:00 AM
- **Code Reviews**: Ongoing, < 4 hours turnaround
- **Pair Programming**: Ad-hoc, 20% del tiempo

### Semanales
- **Tech Talk**: Viernes, 1 hora
- **Planning Poker**: Según necesidad
- **Demo interno**: Jueves

### Por Sprint (2 semanas)
- **Sprint Planning**: Lunes, 2-4 horas
- **Sprint Review**: Viernes, 1 hora
- **Retrospective**: Viernes, 1 hora
- **Refinement**: Miércoles, 1-2 horas

## 🤝 Interacción con Otros Equipos

### Con DevOps
```yaml
Frecuencia: Diaria
Modo: X-as-a-Service + Collaboration ocasional
Puntos de contacto:
  - CI/CD setup
  - Infrastructure requests
  - Incident response
  - Performance tuning
```

### Con Producto
```yaml
Frecuencia: Diaria
Modo: Collaboration
Puntos de contacto:
  - Requirements clarification
  - Sprint planning
  - Demo reviews
  - Roadmap discussion
```

### Con Diseño
```yaml
Frecuencia: Semanal
Modo: Collaboration
Puntos de contacto:
  - Design handoff
  - Component review
  - Accessibility
  - Responsive behavior
```

### Con Arquitectura
```yaml
Frecuencia: Ad-hoc
Modo: Facilitating
Puntos de contacto:
  - Technical design review
  - Architecture decisions
  - Technology adoption
  - Best practices
```

## 📚 Recursos

- [Frontend Developer](./frontend-developer.md)
- [Backend Developer](./backend-developer.md)
- [Full-Stack Developer](./fullstack-developer.md)
- [Mobile Developer](./mobile-developer.md)
- [Tech Lead](./tech-lead.md)
- [Engineering Manager](./engineering-manager.md)
- [QA Engineer](./qa-engineer.md)

---

**Owner**: Engineering Manager / Tech Lead  
**Última actualización**: Diciembre 2025
