# Documentación Organizacional - Equipos de Tecnología

Este repositorio contiene la documentación completa de la estructura organizacional de tecnología, basada en el modelo **Team Topologies**. Incluye perfiles de roles, responsabilidades, procesos, interacciones entre equipos, y límites claros para cada actividad.

## 🏛️ Modelo Organizacional

Nuestra organización sigue el modelo **Team Topologies**, que define cuatro tipos fundamentales de equipos:

- **Stream-Aligned Teams**: Equipos alineados al flujo de valor que entregan características directamente a usuarios (Desarrollo, Producto)
- **Platform Teams**: Equipos que construyen plataformas internas que otros equipos consumen como servicio (DevOps)
- **Enabling Teams**: Equipos que ayudan a otros equipos a superar obstáculos y adquirir nuevas capacidades (Arquitectura, Diseño)
- **Complicated-Subsystem Teams**: Equipos especializados en subsistemas que requieren conocimiento profundo (según necesidad)

## 📋 Estructura de Equipos

### 🚀 [Equipo de Desarrollo](./equipos/desarrollo/README.md)

**Tipo**: Stream-Aligned Team  
**Misión**: Construir y entregar software de alta calidad que resuelva problemas de usuarios y genere valor de negocio.

**Roles incluidos**:

- Frontend Developer
- Backend Developer
- Full-Stack Developer
- Mobile Developer
- Tech Lead
- Engineering Manager
- QA Engineer

**Tamaño**: 5-8 personas por squad (Startup) a 40-80 personas en múltiples squads (Enterprise)

---

### ⚙️ [Equipo de DevOps / Platform](./equipos/devops/README.md)

**Tipo**: Platform Team  
**Misión**: Construir y mantener plataformas internas que permitan a los equipos de desarrollo desplegar software de forma autónoma, segura y eficiente.

**Roles incluidos**:

- Platform Engineer
- Cloud Engineer
- Site Reliability Engineer (SRE)
- CI/CD Engineer
- Security Engineer
- DevOps Team Lead

**Tamaño**: 1 persona (Startup) a 8-15 personas (Enterprise)  
**Modelo de interacción**: 70% X-as-a-Service, 20% Collaboration, 10% Facilitating

---

### 📊 [Equipo de Producto](./equipos/producto/README.md)

**Tipo**: Stream-Aligned Team  
**Misión**: Descubrir y entregar soluciones que resuelvan problemas reales de usuarios mientras cumplen objetivos de negocio.

**Roles incluidos**:

- Product Manager (Estrategia)
- Product Owner (Ejecución)
- Business Analyst
- Data Analyst

**Tamaño**: 1-2 personas (Startup) a 10-20 personas (Enterprise)  
**Modelo**: Dual-Track Agile (Discovery + Delivery)

---

### 🎨 [Equipo de Diseño](./equipos/diseno/README.md)

**Tipo**: Enabling Team / Collaboration  
**Misión**: Diseñar experiencias de usuario excepcionales que sean usables, accesibles y alineadas con los objetivos de negocio.

**Roles incluidos**:

- UX Designer
- UI Designer
- UX Researcher
- Product Designer (híbrido)

**Tamaño**: 1 persona (Startup) a 8-15 personas (Enterprise)  
**Ratio recomendado**: 1 diseñador por cada 8-10 ingenieros

---

### 🏗️ [Equipo de Arquitectura](./equipos/arquitectura/README.md)

**Tipo**: Enabling Team  
**Misión**: Establecer y mantener una arquitectura técnica coherente, escalable y sostenible que permita entregar valor rápidamente mientras se gestiona la complejidad y el riesgo técnico.

**Roles incluidos**:

- Solution Architect
- Enterprise Architect
- Data Architect
- (Modelo federado con Tech Leads)

**Tamaño**: 0 personas (Startup) a 5-10 personas (Large Enterprise)  
**Cuándo contratar**: Solution Architect a partir de 40-50 ingenieros, Enterprise Architect a partir de 100+ ingenieros

---

## 🛠️ [Stacks Tecnológicos](./stacks/README.md)

Catálogo completo de 13 stacks tecnológicos recomendados para diferentes tipos de proyectos:

**Por Arquitectura**:

- Microservices Stack
- Serverless Stack
- Monolith Stack
- Static Site Stack
- Data Pipeline Stack

**Por Lenguaje**:

- .NET Stack
- Node.js Stack
- Python Stack
- Java Stack
- Go Stack

**Por Etapa de Empresa**:

- Startup MVP Stack
- Scale-Up Stack
- Enterprise Stack

Cada stack incluye frontend, backend, bases de datos, infraestructura, CI/CD, observabilidad, y cuándo usar cada uno.

---

## 🔄 Procesos y Workflows

### [Workflows Inter-Equipos](./workflows/README.md)

Documentación de procesos que cruzan múltiples equipos:

- Feature Development (Discovery → Design → Development → Deployment)
- Sprint Planning Cross-Team
- Incident Response & Postmortem
- Release Management
- Onboarding de Nuevos Empleados

### [Ceremonias Ágiles](./ceremonias/README.md)

Documentación de ceremonias estándar:

- Daily Standup
- Sprint Planning
- Sprint Review
- Retrospective
- Backlog Refinement

### [Comunicación](./comunicacion/README.md)

Estrategia de comunicación organizacional:

- Estructura de Canales (Slack/Teams)
- Matriz de Escalación
- Reporting y Métricas
- Documentación Asíncrona

---

## 🎯 Objetivos de Esta Documentación

- **Claridad de Roles**: Cada miembro conoce exactamente sus responsabilidades y límites
- **Interacciones Definidas**: Cómo los equipos colaboran, cuándo y para qué
- **Procesos Estandarizados**: Garantizar consistencia en las operaciones
- **Escalabilidad Organizacional**: Framework para crecer de 10 a 500+ personas
- **Onboarding Eficiente**: Nueva incorporación entiende la estructura completa en días
- **Autonomía con Alineación**: Equipos autónomos dentro de un marco coherente

---

## 🚀 Inicio Rápido

### Para Nuevos Empleados

1. **Entiende la estructura**: Lee [Estructura de Equipos](./equipos/README.md) para comprender el modelo Team Topologies
2. **Encuentra tu equipo**: Navega al README de tu equipo (Desarrollo, DevOps, Producto, Diseño, o Arquitectura)
3. **Lee tu rol**: Dentro de tu equipo, lee el documento de tu rol específico
4. **Aprende los procesos**: Revisa [Workflows](./workflows/README.md) y [Ceremonias](./ceremonias/README.md)
5. **Comunicación**: Configura tus canales según [Comunicación](./comunicacion/README.md)

### Para Líderes de Equipo

1. **Revisa el modelo**: Lee [equipos/README.md](./equipos/README.md) para entender la topología completa
2. **Tamaño de equipo**: Consulta las recomendaciones de tamaño según tu etapa (Startup/Scale-up/Enterprise)
3. **Interacciones**: Define tus modos de interacción con otros equipos (Collaboration, X-as-a-Service, Facilitating)
4. **Métricas**: Implementa las métricas y KPIs documentadas para tu equipo
5. **Stack tecnológico**: Selecciona el stack apropiado de [Stacks](./stacks/README.md)

### Para Ejecutivos

1. **Visión general**: Lee este README y [equipos/README.md](./equipos/README.md)
2. **Escalamiento**: Revisa las tablas de evolución de tamaño de equipos (Startup → Enterprise)
3. **Métricas**: Consulta las métricas de negocio en cada README de equipo
4. **Stacks**: Entiende las decisiones tecnológicas en [Stacks](./stacks/README.md)

---

## 📐 Modos de Interacción Entre Equipos

Basados en Team Topologies, usamos tres modos principales:

| Modo               | Descripción                                                | Duración Típica | Ejemplo                                              |
| ------------------ | ---------------------------------------------------------- | --------------- | ---------------------------------------------------- |
| **Collaboration**  | Dos equipos trabajan juntos en un problema compartido      | Sprints o meses | Desarrollo + Diseño trabajando en nueva feature      |
| **X-as-a-Service** | Un equipo consume servicios de otro con mínima interacción | Continuo        | Desarrollo usando plataforma CI/CD de DevOps         |
| **Facilitating**   | Un equipo ayuda a otro a adquirir nuevas capacidades       | Semanas         | Arquitectura ayudando a Desarrollo con microservices |

---

## 📊 Tamaños de Equipo Recomendados

| Etapa de Empresa            | Ingeniería Total | Desarrollo           | DevOps | Producto | Diseño | Arquitectura |
| --------------------------- | ---------------- | -------------------- | ------ | -------- | ------ | ------------ |
| **Startup** (10-20)         | 6-12             | 5-8 (1 squad)        | 1      | 1-2      | 1      | 0            |
| **Scale-up** (20-50)        | 15-35            | 12-25 (2-3 squads)   | 2-3    | 2-3      | 2-3    | 0-1          |
| **Medium** (50-100)         | 35-70            | 25-50 (3-6 squads)   | 3-5    | 4-7      | 4-6    | 1-2          |
| **Enterprise** (100-300)    | 70-210           | 50-150 (6-20 squads) | 5-10   | 8-15     | 6-10   | 2-4          |
| **Large Enterprise** (300+) | 210+             | 150+ (20+ squads)    | 8-15   | 10-20    | 8-15   | 5-10         |

---

## 📝 Contribuir a Esta Documentación

Para actualizar o mejorar esta documentación:

1. **Crea una rama** con tus cambios: `git checkout -b docs/nombre-cambio`
2. **Actualiza la documentación** relevante siguiendo el formato existente
3. **Crea un Pull Request** con descripción clara de los cambios
4. **Revisión requerida** del líder del equipo correspondiente
5. **Aprobación y merge** por el equipo de arquitectura o engineering manager

### Estándares de Documentación

- Usar Markdown para todos los documentos
- Incluir tabla de contenidos para documentos >200 líneas
- Mantener consistencia con la estructura existente
- Incluir ejemplos prácticos cuando sea posible
- Actualizar la fecha de última modificación

---

## 🔗 Links Útiles

- [Libro Team Topologies](https://teamtopologies.com/)
- [DORA Metrics](https://dora.dev/)
- [Shape Up by Basecamp](https://basecamp.com/shapeup)
- [Google Design Sprint](https://www.gv.com/sprint/)

---

## 📞 Contacto

Para dudas o consultas sobre esta documentación:

- **Estructura organizacional general**: Engineering Manager o VP of Engineering
- **Equipo de Desarrollo**: Tech Lead o Engineering Manager
- **DevOps / Platform**: DevOps Team Lead
- **Producto**: Head of Product o Product Manager principal
- **Diseño**: Design Lead o Head of Design
- **Arquitectura**: Enterprise Architect o Chief Architect

---

## 📜 Notas de Deprecación

⚠️ **Estructura anterior**: Los directorios `/roles/`, `/procesos/`, `/responsabilidades/`, `/herramientas/`, `/metricas/`, y `/plantillas/` están deprecados. La nueva estructura está en `/equipos/`, `/workflows/`, `/ceremonias/`, y `/comunicacion/`.

---

**Última actualización**: Enero 2025  
**Versión**: 2.0 (Team Topologies Model)  
**Modelo**: Team Topologies con equipos Stream-Aligned, Platform, y Enabling
