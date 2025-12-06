# Security Engineer (DevSecOps)

## 👤 Descripción del Rol

El Security Engineer integra prácticas de seguridad en todo el ciclo de vida del desarrollo y operaciones. Automatiza security testing, implementa controles de seguridad, y asegura compliance sin sacrificar velocidad de entrega.

## 🎯 Responsabilidades Principales

### Security Automation
- Integrar security scanning en pipelines CI/CD
  - SAST (Static Application Security Testing)
  - DAST (Dynamic Application Security Testing)
  - SCA (Software Composition Analysis)
  - Container image scanning
- Automatizar remediation de vulnerabilidades comunes
- Implementar security gates en deployment pipelines
- Gestionar false positives y tuning de scanners

### Infrastructure Security
- Implementar security controls en IaC (Infrastructure as Code)
- Configurar security policies (OPA, Kyverno)
- Gestionar secrets management (Key Vaults, sealed secrets)
- Network security (firewalls, NSGs, service mesh policies)
- Identity and Access Management (IAM, RBAC)

### Compliance y Governance
- Asegurar compliance con estándares (SOC2, ISO27001, GDPR)
- Implementar auditing y logging de seguridad
- Gestionar políticas de data encryption (at rest, in transit)
- Realizar security assessments de nuevos servicios
- Mantener documentación de security controls

### Threat Detection y Response
- Configurar security monitoring y alerting
- Análisis de security logs (SIEM)
- Respuesta a security incidents
- Vulnerability management y patching
- Security awareness training

## 📊 Responsabilidades Secundarias

- Revisión de arquitecturas desde perspectiva de seguridad
- Participación en threat modeling sessions
- Mentoría a desarrolladores en secure coding
- Evaluación de herramientas de seguridad

## 🚫 Límites de Actuación

### NO debe hacer:
- Bloquear deploys sin justificación documentada y alternativas
- Implementar controles de seguridad sin considerar usabilidad
- Tomar decisiones de arquitectura de aplicación
- Gestionar aplicaciones individuales

### Debe EVITAR:
- Security por obscuridad
- Procesos de seguridad que añaden semanas a releases
- Rechazar riesgos sin análisis de impacto
- Ignorar feedback de equipos de desarrollo sobre fricciones

## 🔄 Escalamiento

### Escala A:
- **CISO/Security Lead**: Incidentes de seguridad críticos
- **Compliance Officer**: Violaciones de compliance
- **DevOps Lead**: Decisiones de riesgo vs velocidad
- **Legal**: Brechas de datos o incidentes de privacidad

### Recibe Escalamiento De:
- Automated security alerts
- Development teams para security guidance
- SRE para security incidents
- Compliance audits findings

## 📈 Métricas de Éxito

### Vulnerability Management
- **Mean Time to Remediate (MTTR)**: Tiempo promedio para remediar vulnerabilidades
  - Critical: <24h
  - High: <7 días
  - Medium: <30 días
- **Vulnerability Debt**: Número de vulnerabilidades abiertas por severidad
- **Remediation Rate**: % de vulnerabilidades remediadas en SLA

### Security Coverage
- **Scanning Coverage**: % de repositorios con security scanning
- **Secrets Detection**: % de secretos detectados antes de commit
- **Security Gate Pass Rate**: % de builds que pasan security gates
- **Penetration Test Findings**: Número de findings por severity

### Compliance
- **Compliance Score**: % de controles implementados
- **Audit Findings**: Número de findings en auditorías
- **Policy Violations**: Número de violaciones de políticas
- **Training Completion**: % de equipo con security training actualizado

## 🛠 Herramientas Principales

### Code Security
- **SAST**: SonarQube, Checkmarx, Fortify, Semgrep
- **DAST**: OWASP ZAP, Burp Suite
- **SCA**: Snyk, WhiteSource, Dependabot
- **Secrets Scanning**: GitGuardian, TruffleHog, detect-secrets

### Infrastructure Security
- **IaC Scanning**: Checkov, tfsec, Terrascan
- **Container Security**: Trivy, Clair, Aqua Security
- **Kubernetes Security**: Falco, Kube-bench, Kube-hunter
- **Policy as Code**: OPA (Open Policy Agent), Kyverno

### Secrets Management
- **Azure Key Vault**: Secretos, keys, certificados en Azure
- **AWS Secrets Manager**: Secretos en AWS
- **HashiCorp Vault**: Multi-cloud secret management
- **Sealed Secrets**: Encrypted secrets en Kubernetes

### Monitoring & Response
- **SIEM**: Splunk, Azure Sentinel, Elastic Security
- **EDR**: CrowdStrike, Microsoft Defender
- **Cloud Security**: Azure Security Center, AWS Security Hub
- **Vulnerability Management**: Tenable, Qualys

## 🎓 Competencias Requeridas

### Técnicas (Experto)
- Application security (OWASP Top 10)
- Security testing tools (SAST, DAST, SCA)
- Secrets management
- Threat modeling
- Incident response

### Técnicas (Avanzado)
- Cloud security (Azure/AWS/GCP)
- Kubernetes security
- Network security
- Encryption (TLS, encryption at rest)
- Identity and Access Management
- Compliance frameworks (SOC2, ISO27001)

### Blandas
- Comunicación de riesgos a stakeholders
- Balance entre seguridad y usabilidad
- Colaboración con equipos de desarrollo
- Educación y training

## 📅 Actividades Recurrentes

### Diarias
- Revisión de security alerts y vulnerabilities
- Triaging de security scan findings
- Respuesta a consultas de desarrollo teams
- Monitoreo de security dashboards

### Semanales
- Vulnerability management review
- Security incidents retrospective
- Coordination con CI/CD Engineers para mejoras
- Revisión de nuevos security findings

### Mensuales
- Security metrics reporting
- Patching status review
- Security awareness session con equipos
- Evaluación de nuevas herramientas de seguridad
- Compliance checklist review

### Trimestrales
- Penetration testing (interno o externo)
- Security audit preparation
- Disaster recovery drills
- Security roadmap planning
- Threat modeling de nuevos servicios

## 🛡️ Security Controls Framework

### Preventive Controls
```
- Branch protection rules
- Code review requirements
- Security scanning gates
- Secrets prevention (pre-commit hooks)
- Network segmentation
- Least privilege access (RBAC)
```

### Detective Controls
```
- SIEM monitoring
- Anomaly detection
- Vulnerability scanning
- Log analysis
- File integrity monitoring
- Cloud posture management
```

### Corrective Controls
```
- Incident response playbooks
- Automated remediation
- Patch management
- Security updates automation
```

## 🚨 Security Incident Response

### Severity Levels

**Critical (P1)**
- Active data breach
- Ransomware attack
- Compromised credentials with access to production
- Response: Immediate, 24/7

**High (P2)**
- Confirmed vulnerability exploitation attempt
- Unauthorized access to sensitive systems
- Malware detection in production
- Response: Within 2 hours

**Medium (P3)**
- Critical vulnerability disclosed (no exploitation)
- Suspicious activity detected
- Failed authentication spikes
- Response: Within 24 hours

**Low (P4)**
- Security policy violations
- Non-critical vulnerabilities
- Response: Within 1 week

### Response Procedure
1. **Detection**: Alert triggered or reported
2. **Triage**: Assess severity and impact
3. **Containment**: Isolate affected systems
4. **Eradication**: Remove threat
5. **Recovery**: Restore to normal operations
6. **Post-Incident**: Document and improve

## 📚 Security Best Practices

### Shift Left Security
- ✅ Security scanning en IDE (pre-commit)
- ✅ Automated security tests en CI
- ✅ Security training para developers
- ✅ Threat modeling en diseño

### Defense in Depth
- ✅ Múltiples capas de seguridad
- ✅ Network segmentation
- ✅ Principle of least privilege
- ✅ Zero trust architecture

### Secrets Management
- ✅ NUNCA hardcodear secretos
- ✅ Usar secret managers (Key Vault)
- ✅ Rotar secretos regularmente
- ✅ Audit access to secrets

### Compliance
- ✅ Mantener evidencia de controles
- ✅ Regular compliance scanning
- ✅ Documentation up-to-date
- ✅ Audit logs habilitados y protegidos

## 🔍 Common Vulnerabilities

### OWASP Top 10 (2021)
1. Broken Access Control
2. Cryptographic Failures
3. Injection
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery (SSRF)

### Remediation Priorities
- **Critical/High + Exploitable**: Remediar inmediatamente
- **Critical/High + No exploitable**: Remediar en <7 días
- **Medium**: Remediar en sprint planning
- **Low**: Backlog para future sprints

## 📞 Contactos Clave

- **Reporta a**: CISO / DevOps Lead
- **Colabora con**: CI/CD Engineers, Platform Engineers, Development Teams
- **Escala a**: CISO, Legal, Compliance Officer

---

**Última actualización**: Diciembre 2025
