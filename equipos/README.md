# Equipos

Esta sección define la estructura organizacional completa, roles, responsabilidades y dinámicas de colaboración entre todos los equipos.

## 📋 Estructura de Equipos

### 🖥️ [Desarrollo](./desarrollo/README.md)
Equipo encargado de la construcción de software, desde frontend hasta backend.
- Frontend Developer
- Backend Developer
- Full-Stack Developer
- Mobile Developer
- Tech Lead
- Engineering Manager
- QA Engineer

### ⚙️ [DevOps](./devops/README.md)
Equipo enfocado en la automatización, infraestructura y operaciones.
- DevOps Lead
- Platform Engineer
- Site Reliability Engineer (SRE)
- Cloud Engineer
- CI/CD Engineer
- Security Engineer

### 📊 [Producto](./producto/README.md)
Equipo responsable de la visión del producto y requisitos de negocio.
- Product Manager
- Product Owner
- Business Analyst
- Data Analyst

### 🎨 [Diseño](./diseno/README.md)
Equipo dedicado a la experiencia de usuario y diseño de interfaces.
- UX Designer
- UI Designer
- UX Researcher

### 🏗️ [Arquitectura](./arquitectura/README.md)
Equipo que define estándares técnicos y decisiones arquitectónicas.
- Solution Architect
- Enterprise Architect
- Data Architect

## 🔄 Modelo de Colaboración

### Team Topologies

Implementamos el modelo de **Team Topologies** para optimizar la entrega de valor:

```
┌─────────────────────────────────────────────────────┐
│           Stream-Aligned Teams                      │
│  (Equipos de Desarrollo por Feature/Producto)      │
│                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐        │
│  │ Team A   │  │ Team B   │  │ Team C   │        │
│  │ Frontend │  │ Backend  │  │ Mobile   │        │
│  └──────────┘  └──────────┘  └──────────┘        │
└──────────┬──────────┬──────────┬──────────────────┘
           │          │          │
           ▼          ▼          ▼
    ┌──────────────────────────────────┐
    │      Platform Team               │
    │  (DevOps + Platform Engineers)   │
    │  - CI/CD                         │
    │  - Infrastructure                │
    │  - Observability                 │
    └──────────────────────────────────┘
           │
           ▼
    ┌──────────────────────────────────┐
    │      Enabling Team               │
    │  (Arquitectura + QA)             │
    │  - Best practices                │
    │  - Training                      │
    │  - Tooling guidance              │
    └──────────────────────────────────┘
```

### Tipos de Equipos

#### 1. Stream-Aligned Teams (Equipos de Desarrollo)
- **Propósito**: Entregar valor continuo a usuarios finales
- **Enfoque**: Features y productos específicos
- **Autonomía**: Alta - end-to-end ownership
- **Tamaño**: 5-9 personas

#### 2. Platform Team (Equipo DevOps)
- **Propósito**: Proveer plataforma self-service a equipos de desarrollo
- **Enfoque**: Reducir carga cognitiva de desarrollo
- **Servicios**: CI/CD, infraestructura, monitoreo, seguridad
- **Interacción**: X-as-a-Service

#### 3. Enabling Team (Equipo de Arquitectura/QA)
- **Propósito**: Ayudar a equipos a superar obstáculos técnicos
- **Enfoque**: Capacitación y mentoría
- **Duración**: Temporal - hasta lograr autonomía
- **Especialidad**: Arquitectura, testing, performance

#### 4. Complicated-Subsystem Team
- **Propósito**: Manejar subsistemas técnicamente complejos
- **Ejemplos**: ML/AI, procesamiento de datos, motores especializados
- **Expertise**: Altamente especializado

## 🤝 Modos de Interacción

### Collaboration (Colaboración)
- **Cuándo**: Descubrimiento de nuevos patrones o tecnologías
- **Duración**: Temporal (semanas/meses)
- **Ejemplo**: Dev + DevOps diseñando nueva arquitectura de deployment

### X-as-a-Service
- **Cuándo**: Consumo de servicios estandarizados
- **Duración**: Permanente
- **Ejemplo**: Desarrollo usando plataforma CI/CD del equipo DevOps

### Facilitating (Facilitación)
- **Cuándo**: Transferencia de conocimiento
- **Duración**: Temporal hasta autonomía
- **Ejemplo**: Arquitecto ayudando a equipo con migración a microservicios

## 📊 Matriz de Responsabilidades (RACI)

| Actividad | Dev | DevOps | Producto | Diseño | Arquitectura |
|-----------|-----|--------|----------|--------|--------------|
| Definir features | C | I | R/A | C | C |
| Diseño UX/UI | C | I | C | R/A | I |
| Arquitectura técnica | C | C | I | I | R/A |
| Desarrollo código | R/A | C | I | I | C |
| Code review | R/A | C | I | I | C |
| Testing | R/A | C | A | I | C |
| CI/CD setup | C | R/A | I | I | C |
| Deployment producción | C | R/A | I | I | C |
| Monitoreo | C | R/A | I | I | I |
| Incident response | C | R/A | I | I | C |
| Performance optimization | R | R/A | I | I | C |
| Security scanning | C | R/A | I | I | C |

**Leyenda:**
- **R** (Responsible): Ejecuta la tarea
- **A** (Accountable): Responsable final, aprueba
- **C** (Consulted): Se consulta su opinión
- **I** (Informed): Se mantiene informado

## 🎯 Tamaño y Composición de Equipos

### Equipo de Desarrollo (Stream-Aligned)
```yaml
Tamaño ideal: 7 personas
Composición:
  - 1 Tech Lead (30% código, 70% coordinación)
  - 2 Senior Developers
  - 3 Mid-level Developers
  - 1 QA Engineer

Ratio Frontend/Backend:
  - Full-stack team: 7 full-stack developers
  - Especializado: 3 frontend, 3 backend, 1 QA
```

### Equipo DevOps (Platform)
```yaml
Tamaño ideal: 5-8 personas (según escala)
Composición:
  - 1 DevOps Lead
  - 2 Platform Engineers
  - 1 SRE
  - 1 Security Engineer
  - 1-2 Cloud Engineers
```

### Equipo Producto
```yaml
Tamaño ideal: 3-5 personas
Composición:
  - 1 Product Manager
  - 1-2 Product Owners
  - 1 Business Analyst
  - 1 Data Analyst
```

## 📈 Escalado de Equipos

### Startup (10-20 personas)
```
1 equipo full-stack + 1 DevOps lead
```

### Scale-up (20-50 personas)
```
2-3 equipos desarrollo
1 equipo DevOps (3-4 personas)
1 Product Manager
1 Architect
```

### Medium (50-100 personas)
```
4-6 equipos desarrollo
1 equipo DevOps (5-6 personas)
1 equipo producto (3 personas)
2 Architects
1 equipo diseño (2 personas)
```

### Enterprise (100+ personas)
```
8+ equipos desarrollo
1 equipo DevOps (8+ personas)
1 equipo producto (5+ personas)
1 equipo arquitectura (3+ personas)
1 equipo diseño (4+ personas)
1 equipo seguridad dedicado
```

## 🔗 Navegación

- [Desarrollo](./desarrollo/README.md)
- [DevOps](./devops/README.md)
- [Producto](./producto/README.md)
- [Diseño](./diseno/README.md)
- [Arquitectura](./arquitectura/README.md)
- [Workflows Inter-equipos](../workflows/README.md)
- [Ceremonias](../ceremonias/README.md)
- [Comunicación](../comunicacion/README.md)

---

**Última actualización**: Diciembre 2025
