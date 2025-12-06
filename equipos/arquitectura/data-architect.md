# Data Architect

## 📋 Visión General

El Data Architect es responsable de diseñar, implementar, y gobernar la **estrategia de datos** de la organización, asegurando que los datos sean accesibles, confiables, seguros, y que generen valor de negocio. Actúa como puente entre necesidades de negocio, analytics, y sistemas transaccionales.

## 🎯 Responsabilidades

### Diseño de Arquitectura de Datos

**Principales tareas**:
- Diseñar data models (conceptual, logical, physical)
- Definir estrategia de data warehouse / data lake
- Arquitectura de data pipelines (ETL/ELT)
- Real-time streaming architecture
- Master Data Management (MDM) strategy

**Entregables**:
- Entity-Relationship Diagrams (ERD)
- Data flow diagrams
- Data architecture blueprints
- Schema design documentation
- Integration patterns

---

### Data Governance

**Principales tareas**:
- Definir políticas de data governance
- Data quality standards y monitoring
- Data lineage tracking
- PII (Personally Identifiable Information) protection
- Compliance (GDPR, CCPA, HIPAA según industria)
- Data retention policies

**Framework de governance**:
```yaml
Data Ownership:
  - Data Stewards: Business owners de cada dominio
  - Data Custodians: Technical owners (Data Engineers)
  - Data Governance Committee: Cross-functional oversight

Data Quality Dimensions:
  - Accuracy: ¿Datos correctos?
  - Completeness: ¿Sin nulls críticos?
  - Consistency: ¿Coherente cross-systems?
  - Timeliness: ¿Actualizado cuando necesario?
  - Uniqueness: ¿Sin duplicados?
  - Validity: ¿Dentro de rangos esperados?

Privacy & Security:
  - Data classification (Public, Internal, Confidential, Restricted)
  - Encryption at rest & in transit
  - Access controls (RBAC, ABAC)
  - Anonymization / Pseudonymization
  - Audit logging
```

---

### Data Platform Architecture

**Principales tareas**:
- Selección de tecnologías de datos (SQL, NoSQL, streaming)
- Data warehouse design (dimensional modeling, star/snowflake schema)
- Data lake architecture (zones: raw, curated, enriched)
- Lakehouse strategy (Delta Lake, Iceberg)
- Analytics platform (BI, ML, self-service)

**Arquitectura típica**:
```
Data Sources (Transactional DBs, APIs, Files, Streaming)
    ↓
Ingestion Layer (Azure Data Factory, Fivetran, Airbyte, Kafka)
    ↓
Raw Data Zone (Data Lake: Parquet, Avro)
    ↓
Transform Layer (Databricks, Spark, dbt)
    ↓
Curated Data Zone (Data Warehouse: Dimensional models)
    ↓
Serving Layer (BI: Power BI, Tableau; ML: Feature Store; API: GraphQL)
    ↓
Consumption (Dashboards, Reports, ML Models, Applications)
```

---

### Data Integration

**Principales tareas**:
- Diseñar estrategia de integración de datos
- API design para data access
- Event-driven data architecture
- Change Data Capture (CDC) patterns
- Data federation vs consolidation

**Patrones de integración**:
- **Batch ETL**: Scheduled jobs (diario, semanal)
- **Real-time streaming**: Kafka, Event Hubs, Kinesis
- **Micro-batch**: Spark Structured Streaming
- **CDC (Change Data Capture)**: Debezium, Azure SQL CDC
- **Reverse ETL**: Warehouse → Operational systems

---

### Analytics & ML Platform

**Principales tareas**:
- Feature store design para ML
- Data catalog implementation
- Self-service analytics enablement
- Semantic layer design
- Metrics store architecture

**Componentes**:
```yaml
Data Catalog:
  - Tool: Azure Purview, Alation, Collibra
  - Purpose: Data discovery, metadata management, lineage

Feature Store:
  - Tool: Feast, Tecton, Azure ML Feature Store
  - Purpose: ML feature reusability, consistency

Semantic Layer:
  - Tool: dbt Metrics, Cube.js, Metabase
  - Purpose: Business logic centralization

Metrics Store:
  - Tool: Transform (dbt metrics), GoodData
  - Purpose: Definición única de métricas de negocio
```

---

### Performance & Optimization

**Principales tareas**:
- Database performance tuning
- Query optimization
- Indexing strategies
- Partitioning & sharding
- Caching layers (Redis, Memcached)
- Cost optimization (storage tiering, compression)

**Métricas de performance**:
- Query latency: p50, p95, p99
- Data freshness: SLAs por dataset
- Pipeline execution time
- Storage costs per TB
- Compute costs (queries, transformations)

---

## 💼 Perfil del Rol

### Seniority

**Nivel**: Senior a Staff (8-15 años de experiencia)

**Progresión típica**:
```
Data Engineer (3-5 años)
    ↓
Senior Data Engineer (5-8 años)
    ↓
Data Architect (8-12 años)
    ↓
Senior Data Architect (12-15 años)
    ↓
Principal Data Architect / Chief Data Officer (15+ años)
```

---

### Skills Requeridas

#### Technical Skills (Deep)

**Must have**:
- ✅ **SQL**: Advanced (window functions, CTEs, query optimization)
- ✅ **Database design**: Normalization, dimensional modeling, indexing
- ✅ **Data warehousing**: Star/snowflake schema, SCD (Slowly Changing Dimensions)
- ✅ **ETL/ELT**: Azure Data Factory, Airflow, dbt, Spark
- ✅ **Big Data**: Spark, Databricks, distributed computing concepts
- ✅ **Cloud data platforms**: Azure (Synapse, Data Lake, Fabric) o AWS (Redshift, S3, Glue)
- ✅ **Streaming**: Kafka, Event Hubs, Flink, Spark Streaming
- ✅ **NoSQL**: MongoDB, Cosmos DB, Cassandra, Redis

**Nice to have**:
- 🔶 **Data science fundamentals**: Para colaborar con Data Scientists
- 🔶 **ML Ops**: Model deployment, feature engineering
- 🔶 **Graph databases**: Neo4j, CosmosDB Gremlin
- 🔶 **Time-series databases**: InfluxDB, TimescaleDB

---

#### Data Modeling (Critical)

**Must have**:
- ✅ **Conceptual modeling**: Entity-Relationship diagrams
- ✅ **Logical modeling**: Normalized models (3NF, BCNF)
- ✅ **Physical modeling**: Indexes, partitions, storage optimization
- ✅ **Dimensional modeling**: Kimball methodology, star schema
- ✅ **Data Vault**: Para enterprise data warehouses
- ✅ **Graph modeling**: Si hay use cases de grafo

---

#### Data Governance & Security

**Must have**:
- ✅ **Data governance frameworks**: DAMA-DMBOK, DGI Framework
- ✅ **Data quality**: Great Expectations, dbt tests, Soda
- ✅ **Privacy regulations**: GDPR, CCPA compliance
- ✅ **Security**: Encryption, masking, tokenization, RBAC
- ✅ **Data lineage**: Tools como Azure Purview, Alation

---

#### Business Skills (Medium)

**Must have**:
- ✅ **Domain knowledge**: Entender el negocio profundamente
- ✅ **Analytics thinking**: Traducir preguntas de negocio a datos
- ✅ **Stakeholder management**: Comunicar con business users
- ✅ **ROI analysis**: Justificar inversiones en data infrastructure

---

### Stack Tecnológico

El Data Architect debe dominar el stack de datos moderno:

#### Databases

**Relational (OLTP)**:
```yaml
Azure SQL Database / SQL Server
PostgreSQL
MySQL
Oracle (legacy enterprises)
```

**Data Warehouses (OLAP)**:
```yaml
Azure Synapse Analytics
Snowflake
Amazon Redshift
Google BigQuery
Databricks SQL
```

**NoSQL**:
```yaml
Document: MongoDB, Cosmos DB
Key-Value: Redis, DynamoDB
Column-family: Cassandra, HBase
Graph: Neo4j, Cosmos DB Gremlin
Time-series: InfluxDB, TimescaleDB
```

---

#### Data Processing

**Batch Processing**:
```yaml
Azure Data Factory (orchestration)
Apache Spark (Databricks, Synapse Spark)
dbt (analytics engineering)
Python (pandas, polars)
```

**Streaming**:
```yaml
Apache Kafka
Azure Event Hubs
Apache Flink
Spark Structured Streaming
Kafka Streams
```

---

#### Data Storage

**Data Lake**:
```yaml
Azure Data Lake Storage Gen2 (ADLS)
AWS S3
Google Cloud Storage
File formats: Parquet, Avro, Delta Lake, Iceberg
```

**Data Warehouse**:
```yaml
Azure Synapse dedicated SQL pools
Snowflake
Redshift
```

---

#### Data Governance & Quality

```yaml
Catalog: Azure Purview, Alation, Collibra, DataHub
Quality: Great Expectations, Soda, dbt tests
Lineage: Azure Purview, OpenLineage
Master Data: Informatica MDM, Profisee
```

---

#### Analytics & BI

```yaml
BI Tools: Power BI, Tableau, Looker, Metabase
Semantic Layer: dbt Metrics, Cube.js
ML Platforms: Azure ML, Databricks MLflow
Notebooks: Jupyter, Databricks, Synapse Notebooks
```

---

## 📊 Métricas de Éxito

### Data Platform KPIs

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Data Availability** | >99.9% | Mensual |
| **Data Freshness SLA** | >95% datasets on time | Diaria |
| **Pipeline Success Rate** | >98% | Diaria |
| **Query Performance** | p95 <5s (BI queries) | Semanal |
| **Storage Cost Efficiency** | <$X per TB/month | Mensual |

### Data Quality KPIs

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Data Quality Score** | >95% | Semanal |
| **Critical Data Issues** | 0 | Diaria |
| **Completeness** | >98% (non-null en campos críticos) | Semanal |
| **Accuracy** | >99% (validated against source) | Mensual |
| **Duplicates** | <0.1% | Semanal |

### Governance KPIs

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Data Catalog Coverage** | >90% datasets catalogados | Mensual |
| **PII Compliance** | 100% PII protegido | Continuo |
| **Access Control Audit** | 0 unauthorized access | Trimestral |
| **Data Lineage Coverage** | >80% pipelines documented | Trimestral |
| **Retention Policy Compliance** | 100% | Trimestral |

### Business Impact KPIs

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Self-Service Adoption** | >60% analysts usando platform | Trimestral |
| **Time to Insight** | -25% YoY | Trimestral |
| **Data-Driven Decisions** | >80% product decisions con datos | Trimestral |
| **ML Model Performance** | Dependent on use case | Mensual |

---

## 🔄 Interacciones con Otros Equipos

### Con Data Engineering Team

**Frecuencia**: Daily a Weekly  
**Modo**: **Facilitating** + **Collaboration**

**Actividades**:
- Diseño de data pipelines
- Code reviews de transformaciones complejas
- Performance optimization
- Best practices sharing
- Architecture decisions

**Tools**: Daily standups, Slack (#data-engineering), GitHub, Databricks

---

### Con Data Science / ML Team

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Feature store design
- Data requirements para modelos
- Model serving infrastructure
- ML Ops pipelines
- Exploratory data analysis support

**Tools**: Weekly sync, Jupyter notebooks, ML platform (Azure ML, Databricks)

---

### Con Analytics / BI Team

**Frecuencia**: Weekly  
**Modo**: **X-as-a-Service** + **Facilitating**

**Actividades**:
- Semantic layer design
- BI data mart creation
- Query optimization
- Self-service enablement
- Metrics definitions

**Tools**: Power BI, dbt, Slack (#analytics)

---

### Con Application Developers

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Database schema design
- API design para data access
- Performance troubleshooting
- CDC implementation
- Caching strategies

**Tools**: GitHub, Slack (#development), Architecture reviews

---

### Con Product Team

**Frecuencia**: Bi-weekly  
**Modo**: **Facilitating**

**Actividades**:
- Data requirements gathering
- Feasibility assessments
- Analytics roadmap alignment
- Business metric definitions
- User behavior data design

**Tools**: Product roadmap reviews, Confluence

---

### Con Security / Compliance

**Frecuencia**: Monthly  
**Modo**: **Collaboration**

**Actividades**:
- Data security reviews
- PII protection strategies
- Compliance audits (GDPR, etc.)
- Access control policies
- Encryption standards

**Tools**: Security reviews, Compliance dashboards

---

### Con Enterprise Architect

**Frecuencia**: Monthly  
**Modo**: **Facilitating** (recibiendo guidance)

**Actividades**:
- Data strategy alignment
- Cross-system data integration
- Technology evaluations
- Enterprise data governance
- ADR reviews

**Tools**: Architecture forum, ADRs, Monthly syncs

---

## 🎓 Desarrollo Profesional

### Path de Carrera

#### Opción 1: Technical Depth (IC Track)

```
Data Architect (8-12 años)
    ↓
Senior Data Architect (12-15 años)
    - Scope: Enterprise data platform
    - Impact: Org-wide data strategy
    ↓
Principal Data Architect (15-20 años)
    - Scope: Multi-product data ecosystems
    - Impact: Industry thought leadership
    ↓
Distinguished Engineer - Data (20+ años)
    - Scope: Technology vision
    - Impact: External influence
```

#### Opción 2: Leadership (Management Track)

```
Data Architect (8-12 años)
    ↓
Head of Data Architecture (10-14 años)
    - Manage: 2-5 data architects/engineers
    - Scope: Data platform team
    ↓
Director of Data Engineering (14-18 años)
    - Manage: 10-30 data professionals
    - Scope: Entire data organization
    ↓
Chief Data Officer (CDO) (18+ años)
    - Manage: Data + Analytics + ML org
    - Scope: Enterprise data strategy
```

---

### Skills a Desarrollar

**Próximos 6-12 meses**:
- [ ] Certificación avanzada cloud data (Azure Data Engineer Associate + Expert, AWS Data Analytics)
- [ ] Implementar data quality framework (Great Expectations / Soda)
- [ ] Desplegar data catalog (Azure Purview / Alation)
- [ ] Mentoring de 1-2 Data Engineers
- [ ] Presentar 2-3 tech talks sobre data architecture

**Próximos 1-2 años**:
- [ ] Liderar migración data warehouse a cloud
- [ ] Implementar real-time streaming platform
- [ ] Build feature store para ML
- [ ] Desarrollar data governance program
- [ ] Contribuir a open source data tools

**Próximos 3-5 años** (hacia Principal / CDO):
- [ ] Data strategy enterprise-wide
- [ ] Thought leadership (conferencias, blogs)
- [ ] Cross-industry data expertise
- [ ] Business impact demostrable
- [ ] Team building (contratar data team)

---

### Recursos de Aprendizaje

#### Libros Esenciales

- 📚 **"Designing Data-Intensive Applications"** - Martin Kleppmann (must-read)
- 📚 **"The Data Warehouse Toolkit"** - Ralph Kimball (dimensional modeling bible)
- 📚 **"Fundamentals of Data Engineering"** - Joe Reis & Matt Housley (2022)
- 📚 **"Data Mesh"** - Zhamak Dehghani (modern data architecture)
- 📚 **"Building a Data Lakehouse"** - Bill Inmon et al.
- 📚 **"The Enterprise Big Data Lake"** - Alex Gorelik

#### Cursos y Certificaciones

**Azure**:
- Microsoft Certified: Azure Data Engineer Associate (DP-203)
- Microsoft Certified: Azure Data Scientist Associate (DP-100)
- Microsoft Certified: Azure Database Administrator Associate (DP-300)
- Databricks Data Engineer Professional

**AWS**:
- AWS Certified Data Analytics - Specialty
- AWS Certified Database - Specialty

**Otros**:
- dbt Analytics Engineering Certification
- Snowflake SnowPro Core/Advanced Certifications
- CDMP (Certified Data Management Professional) - DAMA

#### Comunidades

- **Data Engineering Weekly**: Newsletter
- **dbt Community Slack**: Analytics engineering
- **Locally Optimistic**: Data newsletter/slack
- **DataTalks.Club**: Comunidad de data engineering
- **Databricks Community**: Cloud data platform

---

## 📝 Herramientas del Día a Día

### Data Modeling

| Tool | Uso | Nivel |
|------|-----|-------|
| **ERwin** | Enterprise data modeling | Advanced |
| **Lucidchart** | ERD diagrams | Intermediate |
| **dbdiagram.io** | Quick database schema design | Basic |
| **dbt** | Analytics data modeling | Advanced |

### Development & Transformation

| Tool | Uso |
|------|-----|
| **SQL (T-SQL, PostgreSQL)** | Query development, optimization |
| **Python** | Data pipelines, automation |
| **dbt** | Analytics transformations, testing |
| **Databricks / Synapse** | Big data processing |
| **Spark (PySpark)** | Large-scale data processing |

### Governance & Quality

| Tool | Uso |
|------|-----|
| **Azure Purview** | Data catalog, lineage |
| **Great Expectations** | Data quality validation |
| **Soda** | Data quality monitoring |
| **Collibra / Alation** | Data governance platform |

### Orchestration & Monitoring

| Tool | Uso |
|------|-----|
| **Azure Data Factory** | ETL orchestration |
| **Apache Airflow** | Workflow orchestration |
| **dbt Cloud** | Analytics workflow management |
| **Grafana / Azure Monitor** | Pipeline monitoring |

---

## 🚀 Ejemplo de Semana Típica

### Lunes
- **9:00-9:30**: Review de data quality alerts del fin de semana
- **10:00-11:00**: Sync con Data Engineering team (sprint planning)
- **11:00-12:00**: Design session: Nueva data pipeline con Data Engineer
- **14:00-15:00**: 1:1 con Data Scientist (feature store requirements)
- **15:00-17:00**: Deep work: Dimensional model design para BI

### Martes
- **9:00-10:00**: Data governance meeting (PII compliance review)
- **10:00-12:00**: Deep work: Performance tuning de queries lentas
- **14:00-15:00**: Analytics roadmap sync con Product Manager
- **15:00-17:00**: Code review de dbt models + Slack support

### Miércoles
- **9:00-10:00**: 1:1 con Enterprise Architect (data strategy alignment)
- **10:00-12:00**: POC: Evaluar nueva tecnología (e.g., Iceberg table format)
- **14:00-15:30**: Architecture review: Real-time streaming design
- **15:30-17:00**: Deep work: Data catalog metadata enrichment

### Jueves
- **9:00-10:00**: Security review: Data access controls audit
- **10:00-12:00**: Pair programming con Data Engineer (complex CDC pipeline)
- **14:00-15:00**: BI team sync: Semantic layer design
- **15:00-17:00**: Deep work: Data quality framework implementation

### Viernes
- **9:00-10:00**: Review de métricas (pipeline SLAs, data quality scores)
- **10:00-11:00**: Tech talk: Presentar dimensional modeling best practices
- **11:00-12:00**: 1:1 mentoring con junior Data Engineer
- **14:00-16:00**: Deep work: Documentation (ADRs, data dictionary)
- **16:00-17:00**: Week wrap-up, backlog grooming

**Deep work**: ~35% del tiempo  
**Meetings & Collaboration**: ~35% del tiempo  
**Code/Design Reviews**: ~20% del tiempo  
**Documentation & Governance**: ~10% del tiempo

---

## 🎯 Señales de que estás listo para este rol

✅ **Tienes**:
- 8+ años de experiencia con datos (Data Engineer, Database Developer)
- Profundo conocimiento de SQL y data modeling
- Experiencia diseñando data warehouses en producción
- Track record de optimización de performance
- Conocimiento de al menos 2 cloud data platforms

✅ **Puedes**:
- Diseñar un data warehouse dimensional desde cero
- Optimizar queries complejas a escala
- Evaluar trade-offs de tecnologías de datos
- Implementar data governance practices
- Comunicar arquitectura de datos a stakeholders no-técnicos

✅ **Te gusta**:
- Resolver problemas de data modeling complejos
- Trabajar con grandes volúmenes de datos
- Garantizar calidad y governance de datos
- Habilitar analytics y ML con datos
- Aprender nuevas tecnologías de datos constantemente

---

## 🔗 Links Relacionados

- [Solution Architect](solution-architect.md) - Arquitectura de soluciones
- [Enterprise Architect](enterprise-architect.md) - Arquitectura empresarial
- [Equipo de Arquitectura](README.md) - Visión general del equipo

---

**Última actualización**: Diciembre 2025  
**Mantenido por**: Data Architect / Enterprise Architect