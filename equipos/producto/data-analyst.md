# Data Analyst

## 📋 Visión General

El Data Analyst es responsable de **analizar datos para generar insights accionables** que informen decisiones de negocio y producto. Trabaja con grandes volúmenes de datos, crea dashboards, y traduce hallazgos técnicos en recomendaciones comprensibles para stakeholders no-técnicos.

**Diferencia clave**: 
- **Data Analyst**: Descriptive & diagnostic analytics (qué pasó, por qué)
- **Data Scientist**: Predictive & prescriptive analytics (qué pasará, qué hacer) + ML

## 🎯 Responsabilidades

### Data Collection & Cleaning

**Principales tareas**:
- Identificar fuentes de datos relevantes
- Extract data (SQL, APIs, web scraping)
- Clean data (missing values, duplicates, outliers)
- Transform data (ETL processes)
- Validate data quality

**Data quality checks**:
```sql
-- Example: Data quality validation
SELECT 
  COUNT(*) as total_rows,
  COUNT(DISTINCT user_id) as unique_users,
  SUM(CASE WHEN email IS NULL THEN 1 ELSE 0 END) as missing_emails,
  SUM(CASE WHEN created_at > CURRENT_DATE THEN 1 ELSE 0 END) as future_dates,
  MIN(created_at) as earliest_date,
  MAX(created_at) as latest_date
FROM users;
```

**Data cleaning techniques**:
- **Missing values**: Imputation (mean, median, mode) o deletion
- **Duplicates**: Deduplication basado en unique keys
- **Outliers**: Winsorization, z-score filtering
- **Inconsistencies**: Standardize formats (dates, phone numbers)

---

### Exploratory Data Analysis (EDA)

**Principales tareas**:
- Understand data distributions (histograms, box plots)
- Identify correlations (heatmaps)
- Detect anomalies y outliers
- Segment data (cohorts, groups)
- Hypothesis generation (what to investigate deeper)

**EDA techniques**:
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load data
df = pd.read_csv('sales_data.csv')

# Descriptive statistics
print(df.describe())

# Check for missing values
print(df.isnull().sum())

# Correlation matrix
corr = df.corr()
sns.heatmap(corr, annot=True)
plt.show()

# Distribution plot
sns.histplot(df['revenue'], bins=50)
plt.show()

# Outlier detection (box plot)
sns.boxplot(x=df['revenue'])
plt.show()
```

---

### SQL Queries & Data Extraction

**Principales tareas**:
- Write complex SQL queries (joins, subqueries, CTEs)
- Optimize query performance
- Create views para queries recurrentes
- Extract data para análisis (export to CSV, Excel)

**SQL skills requeridas**:
```sql
-- Example: Cohort retention analysis
WITH cohort_users AS (
  SELECT 
    user_id,
    DATE_TRUNC('month', first_purchase_date) AS cohort_month
  FROM users
),
cohort_activity AS (
  SELECT 
    cu.cohort_month,
    DATE_TRUNC('month', o.order_date) AS activity_month,
    COUNT(DISTINCT cu.user_id) AS active_users
  FROM cohort_users cu
  JOIN orders o ON cu.user_id = o.user_id
  GROUP BY cu.cohort_month, DATE_TRUNC('month', o.order_date)
)
SELECT 
  cohort_month,
  activity_month,
  active_users,
  ROUND(100.0 * active_users / FIRST_VALUE(active_users) OVER (
    PARTITION BY cohort_month 
    ORDER BY activity_month
  ), 2) AS retention_rate
FROM cohort_activity
ORDER BY cohort_month, activity_month;
```

---

### Dashboard & Visualization Creation

**Principales tareas**:
- Diseñar dashboards (Power BI, Tableau, Looker)
- Seleccionar visualizaciones apropiadas (bar, line, pie, scatter)
- Create interactive dashboards (filters, drill-downs)
- Automate data refresh (scheduled updates)
- Ensure dashboard performance (optimized queries)

**Visualization best practices**:
- **Bar charts**: Comparisons (sales by region)
- **Line charts**: Trends over time (revenue growth)
- **Pie charts**: Proportions (market share) - use sparingly
- **Scatter plots**: Correlations (price vs demand)
- **Heatmaps**: Patterns (user activity by day/hour)
- **Funnels**: Conversion flows (signup → activation → purchase)

**Dashboard design principles**:
- **Clarity**: Simple, no clutter
- **Hierarchy**: Most important metrics prominent
- **Context**: Comparisons (vs last month, vs target)
- **Interactivity**: Filters, drill-downs
- **Performance**: Fast load times (<5 seconds)

---

### Business Metrics & KPI Tracking

**Principales tareas**:
- Define business metrics (con PM, leadership)
- Create KPI dashboards (automated, real-time)
- Monitor metric anomalies (alerts)
- Explain metric movements (why did X change?)
- Forecasting (trend extrapolation, seasonality)

**Common business metrics**:

**Product Metrics**:
- DAU/MAU (Daily/Monthly Active Users)
- Retention Rate (Day 1, Day 7, Day 30)
- Churn Rate
- Feature Adoption Rate
- Session Duration

**Revenue Metrics**:
- MRR/ARR (Monthly/Annual Recurring Revenue)
- ARPU (Average Revenue Per User)
- LTV (Lifetime Value)
- CAC (Customer Acquisition Cost)
- LTV:CAC Ratio (should be >3:1)

**Marketing Metrics**:
- Conversion Rate (funnel stages)
- CTR (Click-Through Rate)
- CPC (Cost Per Click)
- ROAS (Return on Ad Spend)

**Operational Metrics**:
- Order Fulfillment Time
- Customer Support Response Time
- Error Rate (technical issues)
- System Uptime

---

### A/B Testing & Experimentation

**Principales tareas**:
- Design A/B tests (hypothesis, sample size, duration)
- Statistical significance calculation
- Analyze test results (treatment vs control)
- Recommend decisions (ship, iterate, kill)

**A/B test process**:
1. **Hypothesis**: "Changing button color from blue to green will increase CTR by 10%"
2. **Metrics**: Primary (CTR), Secondary (conversion, revenue)
3. **Sample size**: Calculate using power analysis (95% confidence, 80% power)
4. **Randomization**: 50/50 split, ensure no bias
5. **Duration**: Run until statistical significance (min 1-2 weeks)
6. **Analysis**: T-test, chi-square test, Bayesian analysis
7. **Decision**: Ship if significant lift + positive on secondary metrics

**Statistical significance**:
```python
from scipy import stats

# Example: A/B test analysis
control_conversions = 250
control_visitors = 10000
treatment_conversions = 280
treatment_visitors = 10000

control_rate = control_conversions / control_visitors  # 2.5%
treatment_rate = treatment_conversions / treatment_visitors  # 2.8%

# Chi-square test
observed = [[control_conversions, control_visitors - control_conversions],
            [treatment_conversions, treatment_visitors - treatment_conversions]]
chi2, p_value = stats.chi2_contingency(observed)[:2]

print(f"Control rate: {control_rate:.2%}")
print(f"Treatment rate: {treatment_rate:.2%}")
print(f"Lift: {(treatment_rate - control_rate) / control_rate:.2%}")
print(f"P-value: {p_value:.4f}")
print(f"Statistically significant: {p_value < 0.05}")
```

---

### Reporting & Storytelling

**Principales tareas**:
- Create reports (weekly, monthly, quarterly)
- Present findings a stakeholders
- Storytelling con datos (narrative, insights)
- Recommendations (actionable, data-driven)
- Executive summaries (for C-suite)

**Report structure**:
```markdown
# Monthly Product Analytics Report - November 2024

## Executive Summary
- DAU increased 15% MoM (50k → 57.5k users)
- Retention improved from 35% to 38% (Day 30)
- New feature "Export PDF" adopted by 22% of users
- Recommendation: Invest in retention initiatives

## Key Metrics
| Metric | October | November | Change |
|--------|---------|----------|--------|
| DAU | 50,000 | 57,500 | +15% |
| MAU | 180,000 | 200,000 | +11% |
| Retention (D30) | 35% | 38% | +3pp |
| Churn Rate | 8% | 7% | -1pp |

## Deep Dive: Retention Improvement
- Cohort analysis shows Nov cohort 3pp higher retention than Oct
- Hypothesis: New onboarding tutorial (launched Nov 1)
- Supporting data: Tutorial completion rate 75%, retained at 45% vs 30% for non-completers

## Feature Adoption: Export PDF
- Launched Nov 15
- Adoption: 22% of active users (12,650 users)
- Use cases: 60% export reports, 40% export invoices
- Feedback: 4.5/5 satisfaction score (150 responses)

## Recommendations
1. Double down on onboarding tutorial (proven retention impact)
2. Promote Export PDF feature more (high satisfaction, low awareness)
3. Investigate churn drivers (interview churned users)

## Appendix
- Detailed charts, cohort tables, SQL queries
```

---

## 💼 Perfil del Rol

### Seniority

**Nivel**: Junior to Senior (1-8 años de experiencia)

**Progresión típica**:
```
Junior Data Analyst (0-2 años)
    - Tareas: SQL queries, basic dashboards, data cleaning
    ↓
Data Analyst (2-5 años)
    - Tareas: Complex analysis, A/B tests, stakeholder reports
    ↓
Senior Data Analyst (5-8 años)
    - Tareas: Strategic analysis, mentoring, advanced stats
    ↓
Lead Data Analyst / Analytics Manager (8+ años)
    - Manage: 2-5 analysts, analytics strategy
```

**Lateral moves**:
- **Data Scientist**: Si aprendes ML, Python avanzado
- **Business Intelligence Analyst**: Si especializas en dashboards
- **Product Manager**: Si desarrollas product thinking
- **Data Engineer**: Si te interesa más pipelines que análisis

---

### Skills Requeridas

#### SQL (Critical)

**Must have**:
- ✅ **SELECT, WHERE, GROUP BY, HAVING**: Basics
- ✅ **JOINs**: INNER, LEFT, RIGHT, FULL OUTER
- ✅ **Subqueries & CTEs**: Common Table Expressions
- ✅ **Window functions**: ROW_NUMBER, RANK, LAG, LEAD
- ✅ **Aggregations**: SUM, COUNT, AVG, MIN, MAX
- ✅ **Date functions**: DATE_TRUNC, DATE_DIFF, EXTRACT

**Nice to have**:
- 🔶 **Query optimization**: Indexes, execution plans
- 🔶 **Advanced functions**: CASE WHEN, COALESCE, STRING_AGG
- 🔶 **CTEs**: Recursive CTEs

---

#### Data Visualization (Critical)

**Must have**:
- ✅ **Tableau / Power BI / Looker**: Dashboard creation (proficiency in at least one)
- ✅ **Chart selection**: Know when to use bar, line, scatter, etc.
- ✅ **Design principles**: Clarity, hierarchy, color
- ✅ **Storytelling**: Narrative, insights, recommendations

**Nice to have**:
- 🔶 **Python viz**: Matplotlib, Seaborn, Plotly
- 🔶 **D3.js**: Custom visualizations (advanced)

---

#### Statistics (Medium)

**Must have**:
- ✅ **Descriptive stats**: Mean, median, mode, std dev
- ✅ **Distributions**: Normal, skewed, outliers
- ✅ **Hypothesis testing**: T-test, chi-square
- ✅ **Confidence intervals**: 95% CI
- ✅ **A/B testing**: Statistical significance, sample size

**Nice to have**:
- 🔶 **Regression**: Linear, logistic (más Data Scientist)
- 🔶 **Bayesian statistics**: A/B test interpretation
- 🔶 **Time series**: Seasonality, trend analysis

---

#### Programming (Medium)

**Must have**:
- ✅ **Excel**: Advanced (pivot tables, VLOOKUP, INDEX MATCH, charts)
- ✅ **Python basics**: Pandas, NumPy (data manipulation)

**Nice to have**:
- 🔶 **Python advanced**: Matplotlib, Seaborn, Scikit-learn
- 🔶 **R**: Data analysis, ggplot2 (academic backgrounds)
- 🔶 **JavaScript**: D3.js (custom viz)

---

#### Business Acumen (Medium)

**Must have**:
- ✅ **Understanding KPIs**: DAU, retention, churn, revenue, CAC, LTV
- ✅ **Business context**: Why metrics matter (not just calculate)
- ✅ **Metric trade-offs**: E.g., growth vs profitability
- ✅ **Stakeholder communication**: Translate data → insights

---

#### Soft Skills (Critical)

**Must have**:
- ✅ **Communication**: Explain technical findings to non-technical audience
- ✅ **Storytelling**: Narrative con datos (not just charts)
- ✅ **Curiosity**: Always asking "why?"
- ✅ **Attention to detail**: Accurate analysis, no errors
- ✅ **Problem-solving**: Investigative mindset

---

### Stack Tecnológico

El Data Analyst usa **SQL**, **BI tools**, y **Python/R**:

#### Databases & SQL
```yaml
Databases: PostgreSQL, MySQL, SQL Server, Redshift, Snowflake, BigQuery
SQL Tools: DBeaver, DataGrip, pgAdmin, Mode, Redash
```

#### Business Intelligence (BI)
```yaml
Primary: Tableau, Power BI, Looker, Metabase
Alternatives: Qlik, Sisense, Google Data Studio
```

#### Programming & Analysis
```yaml
Python: pandas, NumPy, Matplotlib, Seaborn, Plotly, Jupyter Notebook
R: dplyr, ggplot2, tidyverse (menos común, más academic)
Excel: Advanced (pivot tables, macros)
```

#### Data Warehouses & Cloud
```yaml
Cloud DWH: Snowflake, Google BigQuery, Amazon Redshift
Cloud Platforms: AWS, Azure, GCP (basic familiarity)
```

#### Version Control & Collaboration
```yaml
Git/GitHub: Version control para SQL, Python scripts
Slack: Team communication
Confluence/Notion: Documentation, analysis repos
```

---

## 📊 Métricas de Éxito

### Analysis Output

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Analysis Delivered** | 8-12 analyses/month | Mensual |
| **Dashboards Maintained** | 5-10 dashboards | Continuo |
| **Reports On-Time** | 100% | Semanal/Mensual |
| **Query Performance** | <10s execution time | Por query |

### Business Impact

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **Insights Actioned** | >60% recommendations implemented | Trimestral |
| **A/B Tests Run** | 4-6 tests/quarter | Trimestral |
| **Revenue Impact** | Measurable (e.g., "$X saved via churn analysis") | Anual |

### Stakeholder Satisfaction

| Métrica | Target | Frecuencia |
|---------|--------|------------|
| **PM Satisfaction** | >4/5 (analysis quality, timeliness) | Trimestral |
| **Executive Satisfaction** | >4/5 (dashboard usefulness) | Trimestral |
| **Self-Service Adoption** | >50% stakeholders using dashboards | Trimestral |

---

## 🔄 Interacciones con Otros Equipos

### Con Product Manager

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Define product metrics (KPIs)
- Analyze feature performance (post-launch)
- A/B test design & analysis
- Funnel analysis (conversion optimization)
- User segmentation (cohorts, personas)

**Tools**: SQL, Mixpanel, Amplitude, Tableau, Slack

---

### Con Engineering Team

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Data requests (new tracking events)
- Data pipeline discussions (ETL, data quality)
- Query optimization (performance issues)
- Schema understanding (database structure)

**Tools**: SQL, Jira (for data requests), Slack

---

### Con Marketing Team

**Frecuencia**: Weekly  
**Modo**: **Service Provider** + **Collaboration**

**Actividades**:
- Campaign analysis (CTR, conversion, ROAS)
- Attribution modeling (which channel drives conversions)
- Customer segmentation (targeting)
- Funnel analysis (marketing → signup → conversion)

**Tools**: Google Analytics, SQL, Tableau, Excel

---

### Con Sales Team

**Frecuencia**: Bi-weekly  
**Modo**: **Service Provider**

**Actividades**:
- Sales performance dashboards (pipeline, conversion)
- Customer analysis (LTV, churn risk)
- Territory analysis (sales by region)
- Commission calculations (if needed)

**Tools**: Salesforce, SQL, Excel, Power BI

---

### Con Finance Team

**Frecuencia**: Monthly  
**Modo**: **Service Provider**

**Actividades**:
- Revenue reporting (MRR, ARR)
- Financial forecasting (trend extrapolation)
- Unit economics (CAC, LTV, payback period)
- Budget analysis (spend vs plan)

**Tools**: SQL, Excel, Power BI

---

### Con Data Engineering Team

**Frecuencia**: Weekly  
**Modo**: **Collaboration**

**Actividades**:
- Data pipeline requests (new data sources)
- Data quality issues (missing data, bugs)
- Schema changes (new tables, columns)
- Performance optimization (large queries)

**División**:
- **Data Engineer**: Build & maintain pipelines
- **Data Analyst**: Consume data, analyze, report

---

### Con Data Science Team (si existe)

**Frecuencia**: Monthly  
**Modo**: **Collaboration**

**Actividades**:
- Feature engineering (data prep para ML models)
- Model evaluation (analyze model performance)
- Exploratory analysis (inform model development)

**División**:
- **Data Analyst**: Descriptive & diagnostic (what, why)
- **Data Scientist**: Predictive & prescriptive (what will happen, what to do) + ML

---

## 🎓 Desarrollo Profesional

### Path de Carrera

#### Opción 1: Analytics Specialist

```
Data Analyst (2-5 años)
    ↓
Senior Data Analyst (5-8 años)
    - Complex analysis, stakeholder management
    ↓
Staff Data Analyst / Analytics Manager (8-12 años)
    - Manage 2-5 analysts, analytics strategy
```

#### Opción 2: Data Scientist

```
Data Analyst (2-5 años)
    ↓
Data Scientist (lateral move)
    - Aprender: ML, Python avanzado, stats avanzado
    - Build predictive models, not just dashboards
```

#### Opción 3: Business Intelligence (BI)

```
Data Analyst (2-5 años)
    ↓
BI Analyst / BI Developer (5-8 años)
    - Specialize: Dashboards, data warehousing, ETL
```

#### Opción 4: Product Management

```
Data Analyst (2-5 años)
    ↓
Product Analyst (hybrid Product + Data) (5-7 años)
    ↓
Product Manager
    - Leverage data skills para product decisions
```

---

### Skills a Desarrollar

**Próximos 6-12 meses**:
- [ ] Dominar SQL (advanced: window functions, CTEs, optimization)
- [ ] Aprender Tableau o Power BI (create 5+ dashboards)
- [ ] Python basics (pandas, matplotlib)
- [ ] Statistics refresher (A/B testing, hypothesis testing)
- [ ] Complete 20+ analyses (build portfolio)

**Próximos 1-2 años**:
- [ ] Advanced Python (scikit-learn, statsmodels)
- [ ] A/B testing expertise (run 10+ tests)
- [ ] Stakeholder presentations (present to executives)
- [ ] Mentoring junior analyst
- [ ] Domain expertise (deep knowledge en industria)

**Próximos 3-5 años** (hacia Senior/Data Scientist):
- [ ] Machine Learning fundamentals (if transitioning to DS)
- [ ] Advanced statistics (regression, time series)
- [ ] Business strategy (influence product roadmap)
- [ ] Team management (if analytics manager track)
- [ ] Thought leadership (blog, conferences)

---

### Recursos de Aprendizaje

#### Libros Esenciales

- 📚 **"Storytelling with Data"** - Cole Nussbaumer Knaflic (visualization)
- 📚 **"The Data Warehouse Toolkit"** - Ralph Kimball (data modeling)
- 📚 **"Lean Analytics"** - Alistair Croll & Benjamin Yoskovitz (startup metrics)
- 📚 **"Naked Statistics"** - Charles Wheelan (stats intuition)
- 📚 **"Python for Data Analysis"** - Wes McKinney (pandas creator)

#### Cursos

- **Mode SQL Tutorial**: Free, excellent SQL practice
- **Tableau / Power BI**: Official certifications
- **Coursera**: "Google Data Analytics Professional Certificate"
- **DataCamp**: SQL, Python, R tracks (interactive)
- **Khan Academy**: Statistics refresher (free)

#### Comunidades

- **Locally Optimistic**: Data newsletter, Slack community
- **Data Science Central**: Articles, discussions
- **Reddit**: r/datascience, r/analytics
- **Tableau Community**: Forums, viz of the day

---

## 📝 Herramientas del Día a Día

### SQL & Databases

| Tool | Uso | Nivel |
|------|-----|-------|
| **PostgreSQL / MySQL** | Database querying | Advanced |
| **Snowflake / BigQuery** | Cloud data warehouse | Intermediate |
| **DBeaver / DataGrip** | SQL IDE (write queries) | Advanced |
| **Mode / Redash** | SQL notebooks, reports | Intermediate |

### Business Intelligence

| Tool | Uso | Nivel |
|------|-----|-------|
| **Tableau** | Dashboards, visualizations | Advanced |
| **Power BI** | Microsoft stack alternative | Advanced |
| **Looker** | LookML, embedded analytics | Intermediate |
| **Metabase** | Open-source BI (startups) | Basic |

### Programming & Analysis

| Tool | Uso |
|------|-----|
| **Python** | Pandas, NumPy, Matplotlib, Seaborn, Jupyter |
| **Excel** | Pivot tables, VLOOKUP, charts (still relevant!) |
| **R** | Alternative to Python (more academic) |

### Collaboration

| Tool | Uso |
|------|-----|
| **Git/GitHub** | Version control (SQL, Python scripts) |
| **Slack** | Team communication |
| **Confluence/Notion** | Documentation, analysis repos |
| **Loom** | Video walkthroughs of dashboards |

---

## 🚀 Ejemplo de Semana Típica

### Lunes
- **9:00-10:00**: Weekly sync con PM (define analysis priorities)
- **10:00-12:00**: SQL query: Cohort retention analysis (complex query)
- **14:00-15:00**: Create dashboard (Tableau: retention trends)
- **15:00-17:00**: Exploratory analysis (Python: pandas, matplotlib)

### Martes
- **9:00-10:00**: Review A/B test results (statistical significance check)
- **10:00-12:00**: Deep work: A/B test analysis report (Python + SQL)
- **14:00-15:00**: Stakeholder meeting (present A/B test findings)
- **15:00-17:00**: Dashboard maintenance (fix broken queries, update data)

### Miércoles
- **9:00-12:00**: Deep work: Monthly product metrics report (SQL + Tableau + PowerPoint)
- **14:00-15:00**: Data quality investigation (missing data, anomalies)
- **15:00-16:30**: Collaborate con Data Engineer (new tracking request)
- **16:30-17:00**: 1:1 con Analytics Manager

### Jueves
- **9:00-10:00**: Ad-hoc analysis request de Marketing (campaign performance)
- **10:00-12:00**: Funnel analysis (SQL: conversion rates, drop-off points)
- **14:00-15:00**: Stakeholder presentation (monthly metrics review)
- **15:00-17:00**: Learning time: New Tableau feature, SQL optimization

### Viernes
- **9:00-10:00**: Team analytics sync (share insights, learnings)
- **10:00-12:00**: Deep work: Customer segmentation (Python: clustering)
- **14:00-16:00**: Documentation (analysis repo, SQL queries, findings)
- **16:00-17:00**: Week wrap-up, planning next week

**SQL & data extraction**: ~30%  
**Analysis & insights**: ~25%  
**Dashboard creation**: ~20%  
**Stakeholder communication**: ~15%  
**Learning & admin**: ~10%

---

## 🎯 Señales de que estás listo para este rol

✅ **Tienes**:
- Strong SQL skills (can write complex queries)
- Experience con Excel (advanced: pivot tables, VLOOKUP)
- Analytical mindset (curiosity, problem-solving)
- Basic statistics (mean, median, distributions, hypothesis testing)
- Communication skills (explain findings clearly)

✅ **Puedes**:
- Write SQL queries con JOINs, GROUP BY, window functions
- Create dashboards (Tableau, Power BI, o similar)
- Analyze data en Python (pandas) o Excel
- Interpret A/B test results (statistical significance)
- Present findings a stakeholders (storytelling)

✅ **Te gusta**:
- Working con datos (números, spreadsheets, databases)
- Investigative work (find patterns, answer questions)
- Problem-solving (why did metric X change?)
- Visualization (create beautiful, clear charts)
- Business impact (analysis → decisions → results)

---

## 🔗 Links Relacionados

- [Product Manager](product-manager.md) - Estrategia de producto
- [Business Analyst](business-analyst.md) - Requisitos de negocio
- [Data Architect](../arquitectura/data-architect.md) - Arquitectura de datos
- [Equipo de Producto](README.md) - Visión general del equipo

---

**Última actualización**: Diciembre 2025  
**Mantenido por**: Analytics Manager / Head of Data