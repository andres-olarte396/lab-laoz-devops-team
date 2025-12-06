# Roles y Perfiles del Equipo DevOps

Esta sección define claramente cada rol dentro del equipo DevOps, sus responsabilidades, límites de actuación, y competencias requeridas.

## 📊 Estructura del Equipo

```
DevOps Team
├── DevOps Lead / Manager
├── Site Reliability Engineer (SRE)
├── Platform Engineer
├── CI/CD Engineer
├── Security Engineer (DevSecOps)
└── Cloud Infrastructure Engineer
```

## 🎭 Roles Definidos

### [1. DevOps Lead / Manager](./devops-lead.md)
**Responsabilidad Principal**: Liderazgo estratégico y gestión del equipo DevOps

### [2. Site Reliability Engineer (SRE)](./sre.md)
**Responsabilidad Principal**: Garantizar la confiabilidad, disponibilidad y rendimiento de los sistemas

### [3. Platform Engineer](./platform-engineer.md)
**Responsabilidad Principal**: Diseño y mantenimiento de plataformas internas y herramientas de desarrollo

### [4. CI/CD Engineer](./cicd-engineer.md)
**Responsabilidad Principal**: Automatización de pipelines de integración y despliegue continuo

### [5. Security Engineer (DevSecOps)](./security-engineer.md)
**Responsabilidad Principal**: Integración de seguridad en todo el ciclo de vida del desarrollo

### [6. Cloud Infrastructure Engineer](./cloud-engineer.md)
**Responsabilidad Principal**: Gestión y optimización de infraestructura cloud

## 🔄 Colaboración entre Roles

### Superposiciones Permitidas
- **SRE ↔ Platform Engineer**: Colaboración en observabilidad y herramientas de monitoreo
- **CI/CD Engineer ↔ Security Engineer**: Integración de escaneos de seguridad en pipelines
- **Cloud Engineer ↔ Platform Engineer**: Diseño de arquitecturas escalables

### Límites Claros
- **Desarrolladores** → No gestionan infraestructura de producción directamente
- **DevOps** → No desarrollan features de aplicación (salvo herramientas internas)
- **Security** → Asesora pero no bloquea sin justificación documentada

## 📋 Matriz de Competencias

| Competencia | DevOps Lead | SRE | Platform Eng | CI/CD Eng | Security Eng | Cloud Eng |
|-------------|-------------|-----|--------------|-----------|--------------|-----------|
| Kubernetes | Avanzado | Experto | Experto | Intermedio | Intermedio | Avanzado |
| CI/CD Tools | Avanzado | Intermedio | Intermedio | Experto | Avanzado | Básico |
| Scripting | Avanzado | Experto | Experto | Avanzado | Avanzado | Avanzado |
| Monitoring | Avanzado | Experto | Avanzado | Intermedio | Intermedio | Intermedio |
| Security | Intermedio | Intermedio | Intermedio | Intermedio | Experto | Intermedio |
| Cloud (AWS/Azure) | Avanzado | Avanzado | Avanzado | Intermedio | Intermedio | Experto |
| IaC (Terraform) | Avanzado | Avanzado | Experto | Intermedio | Intermedio | Experto |
| Gestión Proyectos | Experto | Básico | Básico | Básico | Básico | Básico |

**Niveles**: Básico → Intermedio → Avanzado → Experto

## 🎯 Modelo de Responsabilidad

Cada rol sigue el modelo:
- **Responsabilidades Principales**: Tareas core del rol
- **Responsabilidades Secundarias**: Apoyo a otros equipos
- **Límites de Actuación**: Qué NO debe hacer este rol
- **Escalamiento**: Cuándo y a quién escalar problemas

---

Ver documentos individuales de cada rol para detalles completos.
