# Matriz RACI - Responsabilidades del Equipo DevOps

La matriz RACI define claramente quién es **R**esponsable, **A**probador (Accountable), **C**onsultado e **I**nformado para cada actividad del equipo DevOps.

## 🎯 Definiciones

- **R (Responsible)**: Ejecuta la tarea. Puede haber múltiples Rs.
- **A (Accountable)**: Aprueba y es responsable final. Solo uno por actividad.
- **C (Consulted)**: Proporciona input/expertise. Comunicación bidireccional.
- **I (Informed)**: Se le mantiene informado. Comunicación unidireccional.

## 📊 Roles Abreviados

- **DL**: DevOps Lead
- **SRE**: Site Reliability Engineer
- **PE**: Platform Engineer
- **CI**: CI/CD Engineer
- **SE**: Security Engineer (DevSecOps)
- **CE**: Cloud Engineer
- **DEV**: Development Teams
- **PM**: Product Manager

---

## 🔧 Infraestructura y Plataforma

| Actividad                             | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Diseño de arquitectura cloud**      | A   | C   | C   | I   | C   | R   | C   | I   |
| **Provisionar infraestructura nueva** | A   | I   | C   | I   | C   | R   | I   | I   |
| **Gestión de Kubernetes clusters**    | A   | C   | R   | C   | I   | C   | I   | I   |
| **Desarrollo de módulos IaC**         | A   | I   | R   | I   | C   | R   | I   | I   |
| **Optimización de costos cloud**      | A   | C   | C   | I   | I   | R   | I   | I   |
| **Implementar self-service platform** | A   | C   | R   | C   | C   | C   | C   | I   |
| **Network configuration**             | A   | C   | C   | I   | C   | R   | I   | I   |
| **Storage management**                | A   | C   | C   | I   | I   | R   | I   | I   |

---

## 🚀 CI/CD y Deployments

| Actividad                                     | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| --------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Diseño de pipelines CI/CD**                 | A   | C   | C   | R   | C   | I   | C   | I   |
| **Implementar pipeline para nuevo proyecto**  | A   | I   | C   | R   | C   | I   | C   | I   |
| **Configurar deployment strategies**          | A   | C   | C   | R   | I   | C   | I   | I   |
| **Gestionar artifact repositories**           | A   | I   | C   | R   | I   | I   | I   | I   |
| **Optimizar tiempos de build**                | A   | I   | C   | R   | I   | I   | C   | I   |
| **Deployment a producción (automated)**       | I   | I   | I   | R   | I   | I   | R   | I   |
| **Deployment a producción (manual approval)** | A   | C   | I   | R   | C   | I   | C   | C   |
| **Rollback en producción**                    | A   | R   | C   | C   | I   | I   | I   | I   |

---

## 🔒 Seguridad y Compliance

| Actividad                          | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ---------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Security scanning en pipelines** | A   | I   | I   | C   | R   | I   | I   | I   |
| **Gestión de secretos**            | A   | C   | C   | C   | R   | C   | C   | I   |
| **Vulnerability remediation**      | A   | C   | C   | C   | R   | I   | R   | I   |
| **Security incident response**     | A   | C   | C   | I   | R   | C   | I   | I   |
| **Compliance auditing**            | A   | C   | C   | I   | R   | I   | I   | I   |
| **IAM y RBAC configuration**       | A   | C   | C   | I   | R   | C   | I   | I   |
| **Security policies enforcement**  | A   | C   | C   | C   | R   | C   | C   | I   |
| **Penetration testing**            | A   | C   | I   | I   | R   | C   | I   | I   |

---

## 📊 Monitoring y Observabilidad

| Actividad                                 | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ----------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Configurar monitoring de aplicaciones** | A   | R   | C   | I   | I   | I   | C   | I   |
| **Definir SLIs/SLOs/SLAs**                | A   | R   | C   | I   | I   | I   | C   | C   |
| **Implementar alerting**                  | A   | R   | C   | I   | I   | C   | I   | I   |
| **Dashboard creation**                    | C   | R   | C   | I   | I   | C   | C   | C   |
| **Log aggregation setup**                 | A   | R   | C   | I   | I   | C   | I   | I   |
| **Distributed tracing**                   | A   | R   | C   | I   | I   | I   | C   | I   |
| **Performance tuning**                    | A   | R   | C   | I   | I   | C   | R   | I   |
| **Capacity planning**                     | A   | R   | C   | I   | I   | R   | I   | I   |

---

## 🚨 Incident Management

| Actividad                          | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ---------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Incident detection**             | I   | R   | C   | C   | C   | C   | C   | I   |
| **Incident triage (SEV-1/2)**      | A   | R   | C   | C   | C   | C   | I   | I   |
| **Incident response coordination** | A   | R   | C   | C   | C   | C   | C   | I   |
| **Root cause analysis**            | A   | R   | C   | C   | C   | C   | C   | I   |
| **Post-mortem facilitation**       | A   | R   | C   | C   | C   | C   | C   | I   |
| **Implement corrective actions**   | A   | R   | R   | R   | R   | R   | C   | I   |
| **Communication to stakeholders**  | A   | C   | I   | I   | I   | I   | I   | I   |

---

## 🔄 Change Management

| Actividad                      | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
| **Change request submission**  | I   | C   | C   | C   | C   | C   | R   | C   |
| **Risk assessment**            | A   | R   | C   | C   | C   | C   | C   | I   |
| **Change approval (standard)** | A   | C   | C   | C   | C   | C   | I   | I   |
| **Change approval (major)**    | A   | C   | C   | C   | C   | C   | I   | C   |
| **Implementation**             | C   | R   | R   | R   | R   | R   | R   | I   |
| **Verification post-change**   | A   | R   | C   | C   | C   | C   | C   | I   |
| **Documentation**              | C   | R   | R   | R   | R   | R   | C   | I   |

---

## 💾 Backup y Disaster Recovery

| Actividad                        | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| -------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Definir backup strategy**      | A   | R   | C   | I   | C   | C   | I   | I   |
| **Configurar automated backups** | A   | R   | C   | I   | I   | C   | I   | I   |
| **Backup verification**          | A   | R   | I   | I   | I   | C   | I   | I   |
| **Disaster recovery planning**   | A   | R   | C   | I   | C   | C   | I   | C   |
| **DR drill execution**           | A   | R   | C   | I   | C   | C   | I   | I   |
| **Recovery execution (actual)**  | A   | R   | C   | C   | C   | C   | I   | I   |
| **RTO/RPO monitoring**           | A   | R   | I   | I   | I   | C   | I   | I   |

---

## 👥 Team Management

| Actividad                       | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Hiring decisions**            | A/R | C   | C   | C   | C   | C   | I   | I   |
| **Onboarding new members**      | A   | C   | C   | C   | C   | C   | I   | I   |
| **Performance reviews**         | A/R | I   | I   | I   | I   | I   | I   | I   |
| **Career development**          | A/R | C   | C   | C   | C   | C   | I   | I   |
| **Training planning**           | A/R | C   | C   | C   | C   | C   | I   | I   |
| **On-call rotation management** | A   | R   | C   | I   | I   | I   | I   | I   |
| **Conflict resolution**         | A/R | C   | C   | C   | C   | C   | I   | I   |

---

## 📋 Documentation y Knowledge

| Actividad                      | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- |
| **Runbook creation**           | A   | R   | R   | R   | R   | R   | C   | I   |
| **Architecture documentation** | A   | C   | R   | C   | C   | R   | C   | I   |
| **Process documentation**      | A   | R   | R   | R   | R   | R   | I   | I   |
| **Knowledge sharing sessions** | A   | R   | R   | R   | R   | R   | C   | I   |
| **Documentation review**       | A   | C   | C   | C   | C   | C   | I   | I   |

---

## 📈 Metrics y Reporting

| Actividad                 | DL  | SRE | PE  | CI  | SE  | CE  | DEV | PM  |
| ------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Define team KPIs**      | A/R | C   | C   | C   | C   | C   | I   | C   |
| **Collect metrics**       | A   | R   | R   | R   | R   | R   | C   | I   |
| **Analyze trends**        | A   | R   | C   | C   | C   | C   | I   | C   |
| **Report to leadership**  | A/R | C   | C   | C   | C   | C   | I   | I   |
| **DORA metrics tracking** | A   | R   | C   | R   | C   | C   | I   | I   |

---

## 🎓 Ejemplos de Aplicación

### Ejemplo 1: Nueva Feature Requiere Infraestructura

**Escenario**: Development team necesita una nueva base de datos para un microservicio.

| Paso | Actividad      | Ejecución                                                     |
| ---- | -------------- | ------------------------------------------------------------- |
| 1    | Solicitud      | **DEV** (R) crea ticket, **DL** (A) recibe                    |
| 2    | Análisis       | **CE** (R) evalúa opciones, **SE** (C) valida seguridad       |
| 3    | Diseño         | **CE** (R) diseña solución IaC, **PE** (C) revisa integración |
| 4    | Aprobación     | **DL** (A) aprueba, **PM** (I) informado                      |
| 5    | Implementación | **CE** (R) crea infraestructura                               |
| 6    | Configuración  | **PE** (R) configura acceso en plataforma                     |
| 7    | Verificación   | **SRE** (C) valida monitoring, **SE** (C) valida seguridad    |

### Ejemplo 2: Incidente de Producción (SEV-1)

**Escenario**: API principal caída, usuarios afectados.

| Fase        | Actividad          | Ejecución                                       |
| ----------- | ------------------ | ----------------------------------------------- |
| Detection   | Alert triggered    | **SRE** (R) recibe alerta                       |
| Triage      | Assess severity    | **SRE** (R) determina SEV-1                     |
| Mobilize    | Assemble team      | **DL** (A) coordina, **SRE/PE/DEV** (R) se unen |
| Investigate | Root cause         | **SRE** (R) lidera, **PE/CE** (C) asisten       |
| Mitigate    | Apply fix          | **SRE/DEV** (R) implementan fix                 |
| Verify      | Confirm resolution | **SRE** (R) valida, **PM** (I) informado        |
| Post-Mortem | Document & improve | **DL** (A) facilita, **All** (C) participan     |

### Ejemplo 3: Deployment a Producción

**Escenario**: Release de nueva versión de aplicación.

| Etapa          | Actividad         | Ejecución                                         |
| -------------- | ----------------- | ------------------------------------------------- |
| Build          | CI pipeline       | **CI** (R) mantiene pipeline, **DEV** (R) trigger |
| Security Scan  | Automated scan    | **SE** (R) configuró scan, **CI** (C) integró     |
| Staging Deploy | Auto-deployment   | **CI** (R) pipeline auto-deploy                   |
| Smoke Tests    | Automated tests   | **DEV** (R) mantiene tests, **CI** (R) ejecuta    |
| Approval       | Go/No-go          | **DL** (A) aprueba si major, **PM** (C) consulta  |
| Prod Deploy    | Deployment        | **CI** (R) ejecuta, **SRE** (C) monitorea         |
| Monitoring     | Post-deploy watch | **SRE** (R) monitorea 2h, **DL** (I) informado    |

---

## 📝 Notas Importantes

### Principios RACI

1. **Una sola A por actividad**: Evita confusión sobre ownership
2. **Múltiples R permitidos**: Trabajo colaborativo cuando necesario
3. **C vs I**: Consulted requiere feedback, Informed solo recibe updates
4. **Evitar demasiadas C**: Ralentiza decisiones

### Escalamiento

- Si R no puede completar → Escala a A
- Si A necesita decisión mayor → Escala a DL o CTO
- Emergencias (SEV-1) → Puede saltarse C temporalmente, documentar después

### Excepciones

- **Emergencias**: En SEV-1, quien puede resolver lo hace (R), se documenta después
- **Vacaciones/PTO**: Backup assume R o A role temporalmente
- **Gaps de skill**: A puede redistribuir R si hay falta de expertise

---

**Última actualización**: Diciembre 2025
