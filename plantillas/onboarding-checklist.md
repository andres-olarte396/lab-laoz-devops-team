# Checklist de Onboarding - Nuevo Miembro DevOps

**Nombre**: ________________  
**Rol**: ________________  
**Fecha de Inicio**: ________________  
**Buddy/Mentor**: ________________  
**Manager**: ________________

---

## 🎯 Objetivos de Onboarding

- Configurar accesos y herramientas necesarias
- Entender la estructura y procesos del equipo
- Conocer la infraestructura y sistemas
- Realizar primeras contribuciones guiadas
- Integración social con el equipo

**Meta**: Productive contributor en 2 semanas

---

## Día 1: Bienvenida y Setup Inicial

### Administrativo
- [ ] Firma de documentos (NDAs, políticas)
- [ ] Badge/acceso físico a oficina
- [ ] Laptop y equipo asignados
- [ ] Email y credenciales corporativas activas

### Accesos Básicos
- [ ] Slack workspace joined (#general, #devops, #random)
- [ ] Email grupos añadidos
- [ ] Confluence access
- [ ] Jira access
- [ ] GitHub organization member

### Reuniones
- [ ] Welcome meeting con manager (30 min)
- [ ] Meet & greet con el equipo (30 min)
- [ ] Team lunch o coffee
- [ ] Introduction al buddy/mentor

### Lecturas Día 1
- [ ] Leer README principal del repo `lab-laoz-devops-team`
- [ ] Revisar estructura de roles
- [ ] Leer tu propio rol en `/roles/[tu-rol].md`

---

## Semana 1: Fundamentos y Configuración

### Setup de Desarrollo (Día 1-2)

#### Local Environment
- [ ] Instalar Git y configurar SSH keys para GitHub
- [ ] Instalar Docker Desktop
- [ ] Instalar kubectl
- [ ] Instalar Azure CLI (`az`)
- [ ] Instalar Terraform
- [ ] Instalar VS Code con extensiones recomendadas
- [ ] Configurar terminal (oh-my-zsh / PowerShell)

#### Cloud Access
- [ ] Azure Portal access
- [ ] Azure CLI login configurado
- [ ] Suscripción asignada
- [ ] RBAC roles asignados según rol

#### Herramientas de Equipo
- [ ] GitHub account linked a organización
- [ ] Azure DevOps access
- [ ] PagerDuty account (si SRE)
- [ ] Datadog / Grafana access
- [ ] Terraform Cloud / backend access

### Documentación (Día 2-3)

- [ ] Leer matriz RACI completa
- [ ] Revisar procesos principales en `/procesos/`
- [ ] Estudiar herramientas en `/herramientas/`
- [ ] Leer al menos 2 runbooks relevantes
- [ ] Revisar 2 post-mortems recientes

### Infraestructura (Día 3-4)

- [ ] Walkthrough de arquitectura cloud con Cloud Engineer
- [ ] Entender ambientes (dev, staging, prod)
- [ ] Revisar dashboards de monitoring principales
- [ ] Acceso de solo lectura a Kubernetes clusters
- [ ] Tour por Terraform repositories

### Meetings & Shadowing (Durante la semana)

- [ ] Asistir a Daily Standup (todos los días)
- [ ] Shadowing de on-call engineer (medio día)
- [ ] Asistir a 1-on-1 con manager
- [ ] Participar en retrospectiva de equipo
- [ ] Asistir a code review session

---

## Semana 2: Hands-On y Primeras Contribuciones

### Tareas Guiadas

- [ ] **Tarea 1**: Actualizar documentación (encontrar y fix typo/outdated info)
  - Objetivo: Familiarizarse con proceso de PR
  - Buddy review required
  
- [ ] **Tarea 2**: Deploy a ambiente de desarrollo
  - Objetivo: Entender pipeline CI/CD
  - Usar existing pipeline, solo trigger
  
- [ ] **Tarea 3**: Crear un recurso simple en dev con IaC
  - Objetivo: Práctica con Terraform/Bicep
  - Ejemplo: Storage account o resource group
  - Buddy review required

- [ ] **Tarea 4**: Investigar y resolver ticket de menor complejidad
  - Objetivo: Troubleshooting básico
  - Ticket será pre-seleccionado por buddy

### Shadowing Avanzado

- [ ] Shadowing de deployment a producción
- [ ] Participar en incident response (observador)
- [ ] Asistir a architecture review meeting
- [ ] Join a post-mortem meeting

### Networking

- [ ] 1-on-1 coffee chat con cada miembro del equipo DevOps
- [ ] Meet cross-functional teams (Development, QA, Security)
- [ ] Lunch con Product Manager

---

## Semana 3-4: Incrementar Autonomía

### Proyectos

- [ ] **Proyecto Onboarding**: [Asignado por manager]
  - Tamaño: Completable en 1-2 semanas
  - Objetivo: Contribución real al equipo
  - Ejemplo: Automatizar proceso manual, optimizar pipeline, crear dashboard
  
### On-Call Preparation (si aplica a rol)

- [ ] Leer todos los runbooks de servicios críticos
- [ ] Practicar troubleshooting scenarios con buddy
- [ ] Configurar PagerDuty y test notifications
- [ ] Shadowing on-call completo (1 semana)
- [ ] Backup on-call role (con mentor disponible)

### Knowledge Sharing

- [ ] Presentar proyecto de onboarding al equipo (15 min)
- [ ] Escribir documento de "What I learned" y compartir

---

## Fin de Mes 1: Evaluación

### Self-Assessment

¿Te sientes cómodo/a con...? (1-5 scale)

- [ ] Procesos del equipo: ___/5
- [ ] Herramientas principales: ___/5
- [ ] Arquitectura de sistemas: ___/5
- [ ] Autonomía para contribuir: ___/5
- [ ] Conocimiento de tu rol: ___/5

### 30-Day Review Meeting

- [ ] Meeting con manager (1 hora)
- [ ] Feedback de buddy
- [ ] Discutir: Qué fue bien, qué puede mejorar
- [ ] Establecer goals para próximos 60 días

---

## Recursos de Referencia

### Documentación Esencial
- Repositorio: `lab-laoz-devops-team`
- Confluence: [Link a wiki]
- Architecture docs: [Link]
- Runbooks: `/procesos/runbooks/`

### Contactos Clave
- Manager: [Nombre] - [Email] - [Slack]
- Buddy: [Nombre] - [Email] - [Slack]
- DevOps Lead: [Nombre] - [Email] - [Slack]

### Canales de Slack
- `#devops` - General team channel
- `#devops-support` - Support requests
- `#incidents` - Incident coordination
- `#deployments` - Deployment notifications
- `#alerts` - Automated alerts (read-only)

### Dashboards
- Grafana: [Link]
- Datadog: [Link]
- Azure Portal: [Link]
- PagerDuty: [Link]

---

## Notas y Feedback

### Lo que fue bien
[Espacio para notas]

### Lo que puede mejorar
[Espacio para notas]

### Preguntas Pendientes
[Espacio para notas]

---

**Completado por**: ________________  
**Fecha**: ________________  
**Manager Sign-off**: ________________
