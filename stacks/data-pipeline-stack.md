# Data Pipeline Stack - Azure Data Services

## 📋 Overview

Stack optimizado para pipelines de procesamiento de datos, ETL/ELT, analytics, y data science workflows en Azure.

### Ideal Para
- ✅ ETL/ELT pipelines
- ✅ Data warehousing
- ✅ Real-time streaming analytics
- ✅ Batch processing
- ✅ Data lake ingestion
- ✅ ML data preparation
- ✅ Business intelligence pipelines

### NO Usar Cuando
- ❌ Transactional workloads (usar SQL Database)
- ❌ Simple CRUD operations
- ❌ Real-time OLTP

### Ventajas
- 📊 Escalabilidad masiva
- 🔄 Procesamiento batch y streaming
- 🤖 Integración ML/AI nativa
- 💰 Almacenamiento económico (Data Lake)
- 🔧 Low-code/no-code options
- 📈 Analytics integrado

## 🏗️ Architecture

```
Data Sources
    │
    ├─── Databases (SQL, NoSQL)
    ├─── APIs (REST, GraphQL)
    ├─── Files (CSV, JSON, Parquet)
    ├─── Streaming (IoT, Events)
    └─── SaaS (Salesforce, etc.)
         │
         ▼
┌────────────────────────────────────┐
│    Azure Data Factory / Synapse    │
│    (Orchestration & ETL)           │
└────────┬───────────────────────────┘
         │
         ▼
┌────────────────────────────────────┐
│    Azure Data Lake Storage Gen2   │
│    (Bronze → Silver → Gold)        │
└────────┬───────────────────────────┘
         │
         ├──────────────┬──────────────┬──────────────┐
         ▼              ▼              ▼              ▼
   ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
   │ Databricks  │ Synapse  │    │ Azure   │    │ Power   │
   │ (Transform) │ Analytics│    │ ML      │    │ BI      │
   └─────────┘    └─────────┘    └─────────┘    └─────────┘
```

## 🛠️ Technology Stack

### Orchestration & ETL
```yaml
Azure Data Factory (ADF):
  - Visual ETL designer
  - 100+ connectors
  - Scheduling & monitoring
  - CI/CD integration
  - Mapping data flows

Azure Synapse Pipelines:
  - ADF capabilities + analytics
  - Integrated environment
  - Spark pools
  - SQL pools

Apache Airflow:
  - Code-first orchestration
  - Python DAGs
  - Self-hosted on AKS
  - Azure Managed Airflow (preview)
```

### Data Storage
```yaml
Azure Data Lake Storage Gen2 (ADLS):
  - Hierarchical namespace
  - Massive scale (exabytes)
  - Hadoop compatible
  - ACL permissions
  - Lifecycle management

Layered Architecture:
  - Bronze: Raw data (as-is)
  - Silver: Cleaned/validated
  - Gold: Business-ready aggregates

File Formats:
  - Parquet (recommended)
  - Delta Lake (ACID transactions)
  - ORC
  - Avro
  - JSON/CSV (raw ingestion)
```

### Data Processing
```yaml
Azure Databricks:
  - Apache Spark managed
  - Collaborative notebooks
  - ML workflows (MLflow)
  - Delta Lake support
  - Auto-scaling clusters

Azure Synapse Analytics:
  - Serverless SQL pools
  - Dedicated SQL pools (DW)
  - Apache Spark pools
  - Integrated environment

Azure HDInsight:
  - Hadoop ecosystem
  - Spark, Hive, HBase
  - Kafka for streaming
```

### Streaming
```yaml
Azure Event Hubs:
  - Kafka-compatible
  - Millions events/sec
  - Capture to Data Lake
  - Integration with Stream Analytics

Azure Stream Analytics:
  - Real-time SQL queries
  - Windowing functions
  - ML integration
  - Output to multiple sinks

Azure Databricks Streaming:
  - Structured Streaming
  - Delta Live Tables
  - Auto-scaling
```

### Data Warehouse
```yaml
Azure Synapse Dedicated SQL Pool:
  - MPP architecture
  - Petabyte scale
  - PolyBase (external tables)
  - Columnstore indexes

Alternatives:
  - Azure SQL Database (smaller scale)
  - Databricks SQL Warehouse
  - Snowflake on Azure
```

### Analytics & BI
```yaml
Power BI:
  - Interactive dashboards
  - DirectQuery / Import
  - Premium capacity
  - Embedded analytics

Azure Analysis Services:
  - Tabular models
  - In-memory caching
  - DAX queries

Azure Synapse Analytics:
  - Integrated SQL analytics
  - Serverless querying
```

### Machine Learning
```yaml
Azure Machine Learning:
  - AutoML
  - Model training
  - Model deployment
  - MLOps pipelines

Databricks ML:
  - MLflow tracking
  - Feature Store
  - Model serving
  - AutoML
```

### Data Governance
```yaml
Microsoft Purview:
  - Data catalog
  - Data lineage
  - Data classification
  - Compliance scanning

Azure Policy:
  - Governance rules
  - Compliance enforcement
  - Resource tagging
```

## 📁 Project Structure

### Data Factory Project
```
my-data-pipeline/
├── adf/
│   ├── pipeline/
│   │   ├── IngestData.json
│   │   ├── TransformData.json
│   │   └── LoadWarehouse.json
│   ├── dataset/
│   │   ├── SourceDB.json
│   │   ├── DataLakeBronze.json
│   │   ├── DataLakeSilver.json
│   │   └── DataLakeGold.json
│   ├── linkedService/
│   │   ├── AzureDataLake.json
│   │   ├── AzureSqlDatabase.json
│   │   └── Databricks.json
│   ├── dataflow/
│   │   └── CleanCustomers.json
│   └── trigger/
│       ├── DailySchedule.json
│       └── BlobTrigger.json
├── databricks/
│   ├── notebooks/
│   │   ├── bronze_to_silver.py
│   │   ├── silver_to_gold.py
│   │   └── ml_training.py
│   ├── jobs/
│   │   └── daily_processing.json
│   └── libraries/
│       └── requirements.txt
├── sql/
│   ├── schema/
│   │   ├── dim_customer.sql
│   │   ├── dim_product.sql
│   │   └── fact_sales.sql
│   └── stored_procedures/
│       └── usp_load_sales.sql
├── infrastructure/
│   ├── main.bicep
│   └── parameters.json
├── tests/
│   ├── test_data_quality.py
│   └── test_transformations.py
├── .github/
│   └── workflows/
│       └── deploy-pipeline.yml
└── README.md
```

## 🚀 Sample Implementations

### Data Factory Pipeline (JSON)
```json
{
  "name": "IngestCustomerData",
  "properties": {
    "activities": [
      {
        "name": "CopyFromSQL",
        "type": "Copy",
        "inputs": [
          {
            "referenceName": "SourceSQLDB",
            "type": "DatasetReference"
          }
        ],
        "outputs": [
          {
            "referenceName": "DataLakeBronze",
            "type": "DatasetReference",
            "parameters": {
              "fileName": "@concat('customers_', formatDateTime(utcnow(), 'yyyyMMdd'), '.parquet')"
            }
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "sqlReaderQuery": "SELECT * FROM dbo.Customers WHERE ModifiedDate > '@{pipeline().parameters.watermark}'"
          },
          "sink": {
            "type": "ParquetSink",
            "storeSettings": {
              "type": "AzureBlobFSWriteSettings"
            }
          }
        }
      },
      {
        "name": "TriggerDatabricksNotebook",
        "type": "DatabricksNotebook",
        "dependsOn": [
          {
            "activity": "CopyFromSQL",
            "dependencyConditions": ["Succeeded"]
          }
        ],
        "typeProperties": {
          "notebookPath": "/notebooks/bronze_to_silver",
          "baseParameters": {
            "input_path": "@activity('CopyFromSQL').output.filePath",
            "date": "@formatDateTime(utcnow(), 'yyyy-MM-dd')"
          }
        }
      }
    ],
    "parameters": {
      "watermark": {
        "type": "String",
        "defaultValue": "1900-01-01"
      }
    }
  }
}
```

### Databricks Notebook (Bronze to Silver)
```python
# bronze_to_silver.py
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from delta.tables import DeltaTable

# Initialize Spark with Delta Lake
spark = SparkSession.builder \
    .appName("BronzeToSilver") \
    .config("spark.sql.extensions", "io.delta.sql.DeltaSparkSessionExtension") \
    .config("spark.sql.catalog.spark_catalog", "org.apache.spark.sql.delta.catalog.DeltaCatalog") \
    .getOrCreate()

# Parameters (passed from ADF)
dbutils.widgets.text("input_path", "")
dbutils.widgets.text("date", "")

input_path = dbutils.widgets.get("input_path")
process_date = dbutils.widgets.get("date")

# Read Bronze data
bronze_df = spark.read.parquet(f"abfss://bronze@mydatalake.dfs.core.windows.net/{input_path}")

# Data Quality & Transformation
silver_df = bronze_df \
    .filter(col("CustomerId").isNotNull()) \
    .filter(col("Email").rlike("^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$")) \
    .withColumn("FullName", concat_ws(" ", col("FirstName"), col("LastName"))) \
    .withColumn("ProcessedDate", lit(process_date)) \
    .withColumn("Hash", sha2(concat_ws("||", *bronze_df.columns), 256)) \
    .dropDuplicates(["CustomerId"]) \
    .select(
        "CustomerId",
        "FullName",
        "Email",
        "Phone",
        "City",
        "Country",
        "CreatedDate",
        "ProcessedDate",
        "Hash"
    )

# Write to Silver layer using Delta Lake (ACID transactions)
silver_path = "abfss://silver@mydatalake.dfs.core.windows.net/customers"

if DeltaTable.isDeltaTable(spark, silver_path):
    # Merge (upsert) if table exists
    silver_table = DeltaTable.forPath(spark, silver_path)
    
    silver_table.alias("target") \
        .merge(
            silver_df.alias("source"),
            "target.CustomerId = source.CustomerId"
        ) \
        .whenMatchedUpdate(
            condition="target.Hash != source.Hash",
            set={
                "FullName": "source.FullName",
                "Email": "source.Email",
                "Phone": "source.Phone",
                "City": "source.City",
                "Country": "source.Country",
                "ProcessedDate": "source.ProcessedDate",
                "Hash": "source.Hash"
            }
        ) \
        .whenNotMatchedInsertAll() \
        .execute()
else:
    # Create table if doesn't exist
    silver_df.write \
        .format("delta") \
        .mode("overwrite") \
        .option("overwriteSchema", "true") \
        .save(silver_path)

# Data Quality Metrics
total_records = silver_df.count()
null_emails = silver_df.filter(col("Email").isNull()).count()
invalid_phones = silver_df.filter(~col("Phone").rlike("^\\+?[0-9]{10,15}$")).count()

print(f"Processed {total_records} records")
print(f"Null emails: {null_emails}")
print(f"Invalid phones: {invalid_phones}")

# Log metrics to Application Insights (optional)
dbutils.notebook.exit({
    "total_records": total_records,
    "null_emails": null_emails,
    "invalid_phones": invalid_phones
})
```

### Silver to Gold Aggregation
```python
# silver_to_gold.py
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from pyspark.sql.window import Window

spark = SparkSession.builder.appName("SilverToGold").getOrCreate()

# Read Silver layer
customers_df = spark.read.format("delta").load("abfss://silver@mydatalake.dfs.core.windows.net/customers")
orders_df = spark.read.format("delta").load("abfss://silver@mydatalake.dfs.core.windows.net/orders")

# Business aggregations
customer_metrics = orders_df \
    .join(customers_df, "CustomerId") \
    .groupBy("CustomerId", "FullName", "Country", "City") \
    .agg(
        count("OrderId").alias("TotalOrders"),
        sum("OrderAmount").alias("TotalRevenue"),
        avg("OrderAmount").alias("AvgOrderValue"),
        max("OrderDate").alias("LastOrderDate"),
        min("OrderDate").alias("FirstOrderDate")
    ) \
    .withColumn(
        "CustomerLifetimeValue",
        when(col("TotalOrders") > 10, col("TotalRevenue") * 1.2)
        .otherwise(col("TotalRevenue"))
    ) \
    .withColumn(
        "CustomerSegment",
        when(col("TotalRevenue") > 10000, "Premium")
        .when(col("TotalRevenue") > 5000, "Gold")
        .when(col("TotalRevenue") > 1000, "Silver")
        .otherwise("Bronze")
    )

# Write to Gold layer
gold_path = "abfss://gold@mydatalake.dfs.core.windows.net/customer_metrics"

customer_metrics.write \
    .format("delta") \
    .mode("overwrite") \
    .option("overwriteSchema", "true") \
    .partitionBy("Country") \
    .save(gold_path)

# Create external table for SQL access
spark.sql(f"""
    CREATE TABLE IF NOT EXISTS gold.customer_metrics
    USING DELTA
    LOCATION '{gold_path}'
""")

print(f"Created gold table with {customer_metrics.count()} records")
```

### Synapse SQL Pool Schema
```sql
-- sql/schema/dim_customer.sql
CREATE TABLE dim_customer (
    customer_key INT IDENTITY(1,1) NOT NULL,
    customer_id NVARCHAR(50) NOT NULL,
    full_name NVARCHAR(200),
    email NVARCHAR(255),
    phone NVARCHAR(50),
    city NVARCHAR(100),
    country NVARCHAR(100),
    customer_segment NVARCHAR(50),
    created_date DATETIME2,
    effective_date DATETIME2 NOT NULL,
    expiration_date DATETIME2 NOT NULL,
    is_current BIT NOT NULL,
    row_hash VARBINARY(32)
)
WITH (
    DISTRIBUTION = REPLICATE,
    CLUSTERED COLUMNSTORE INDEX
);

-- sql/schema/fact_sales.sql
CREATE TABLE fact_sales (
    sale_key BIGINT IDENTITY(1,1) NOT NULL,
    customer_key INT NOT NULL,
    product_key INT NOT NULL,
    date_key INT NOT NULL,
    order_id NVARCHAR(50),
    quantity INT,
    unit_price DECIMAL(18,2),
    total_amount DECIMAL(18,2),
    discount_amount DECIMAL(18,2),
    net_amount DECIMAL(18,2)
)
WITH (
    DISTRIBUTION = HASH(customer_key),
    CLUSTERED COLUMNSTORE INDEX,
    PARTITION (
        date_key RANGE RIGHT FOR VALUES (
            20240101, 20240201, 20240301, 20240401,
            20240501, 20240601, 20240701, 20240801,
            20240901, 20241001, 20241101, 20241201
        )
    )
);
```

### Data Quality Tests (pytest)
```python
# tests/test_data_quality.py
import pytest
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

@pytest.fixture(scope="session")
def spark():
    return SparkSession.builder \
        .appName("DataQualityTests") \
        .getOrCreate()

def test_no_null_customer_ids(spark):
    """Verify no null customer IDs in silver layer"""
    df = spark.read.format("delta").load("abfss://silver@mydatalake.dfs.core.windows.net/customers")
    null_count = df.filter(col("CustomerId").isNull()).count()
    assert null_count == 0, f"Found {null_count} null customer IDs"

def test_email_format(spark):
    """Verify all emails match expected format"""
    df = spark.read.format("delta").load("abfss://silver@mydatalake.dfs.core.windows.net/customers")
    invalid_emails = df.filter(
        ~col("Email").rlike("^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$")
    ).count()
    assert invalid_emails == 0, f"Found {invalid_emails} invalid email formats"

def test_no_duplicates(spark):
    """Verify no duplicate customer IDs"""
    df = spark.read.format("delta").load("abfss://silver@mydatalake.dfs.core.windows.net/customers")
    total_count = df.count()
    distinct_count = df.select("CustomerId").distinct().count()
    assert total_count == distinct_count, "Found duplicate customer IDs"

def test_revenue_consistency(spark):
    """Verify revenue calculations are consistent"""
    df = spark.read.format("delta").load("abfss://gold@mydatalake.dfs.core.windows.net/customer_metrics")
    invalid_revenue = df.filter(col("TotalRevenue") < 0).count()
    assert invalid_revenue == 0, f"Found {invalid_revenue} records with negative revenue"
```

## 🏗️ Infrastructure as Code

```bicep
// infrastructure/main.bicep
param location string = resourceGroup().location
param dataLakeName string
param dataFactoryName string
param synapseWorkspaceName string

// Data Lake Storage Gen2
resource dataLake 'Microsoft.Storage/storageAccounts@2023-01-01' = {
  name: dataLakeName
  location: location
  sku: {
    name: 'Standard_LRS'
  }
  kind: 'StorageV2'
  properties: {
    isHnsEnabled: true // Hierarchical namespace
    minimumTlsVersion: 'TLS1_2'
    accessTier: 'Hot'
  }
}

// Create containers (layers)
resource bronzeContainer 'Microsoft.Storage/storageAccounts/blobServices/containers@2023-01-01' = {
  name: '${dataLake.name}/default/bronze'
  properties: {
    publicAccess: 'None'
  }
}

resource silverContainer 'Microsoft.Storage/storageAccounts/blobServices/containers@2023-01-01' = {
  name: '${dataLake.name}/default/silver'
  properties: {
    publicAccess: 'None'
  }
}

resource goldContainer 'Microsoft.Storage/storageAccounts/blobServices/containers@2023-01-01' = {
  name: '${dataLake.name}/default/gold'
  properties: {
    publicAccess: 'None'
  }
}

// Data Factory
resource dataFactory 'Microsoft.DataFactory/factories@2018-06-01' = {
  name: dataFactoryName
  location: location
  identity: {
    type: 'SystemAssigned'
  }
  properties: {
    publicNetworkAccess: 'Enabled'
  }
}

// Synapse Workspace
resource synapseWorkspace 'Microsoft.Synapse/workspaces@2021-06-01' = {
  name: synapseWorkspaceName
  location: location
  identity: {
    type: 'SystemAssigned'
  }
  properties: {
    defaultDataLakeStorage: {
      accountUrl: dataLake.properties.primaryEndpoints.dfs
      filesystem: 'synapse'
    }
    sqlAdministratorLogin: 'sqladmin'
    sqlAdministratorLoginPassword: '<secure-password>'
  }
}

// Synapse Spark Pool
resource sparkPool 'Microsoft.Synapse/workspaces/bigDataPools@2021-06-01' = {
  parent: synapseWorkspace
  name: 'sparkpool1'
  location: location
  properties: {
    sparkVersion: '3.3'
    nodeSize: 'Medium'
    nodeSizeFamily: 'MemoryOptimized'
    autoScale: {
      enabled: true
      minNodeCount: 3
      maxNodeCount: 10
    }
    autoPause: {
      enabled: true
      delayInMinutes: 15
    }
  }
}
```

## 💰 Cost Estimation

```yaml
Small Pipeline (< 1TB/month):
  - Data Lake Storage: ~$20/month
  - Data Factory: ~$100/month
  - Databricks (Standard): ~$200/month
  - Synapse Serverless: ~$50/month
  Total: ~$370/month

Medium Pipeline (1-10TB/month):
  - Data Lake Storage: ~$100/month
  - Data Factory: ~$300/month
  - Databricks (Premium): ~$800/month
  - Synapse Dedicated Pool (DW100c): ~$1,200/month
  - Event Hubs: ~$100/month
  Total: ~$2,500/month

Large Pipeline (>10TB/month):
  - Data Lake Storage: ~$500/month
  - Data Factory: ~$1,000/month
  - Databricks (Premium, large cluster): ~$3,000/month
  - Synapse Dedicated Pool (DW500c): ~$6,000/month
  - Event Hubs (Dedicated): ~$1,000/month
  Total: ~$11,500/month
```

## ⚡ Quick Start

```bash
# 1. Create resource group
az group create --name rg-datapipeline --location eastus

# 2. Deploy infrastructure
az deployment group create \
  --resource-group rg-datapipeline \
  --template-file infrastructure/main.bicep \
  --parameters dataLakeName=mydatalake dataFactoryName=myadf

# 3. Create Data Factory pipeline (via Portal or ARM)

# 4. Upload Databricks notebooks
databricks workspace import_dir ./databricks/notebooks /notebooks

# 5. Create ADF linked services and datasets

# 6. Trigger pipeline
az datafactory pipeline create-run \
  --resource-group rg-datapipeline \
  --factory-name myadf \
  --name IngestCustomerData
```

## 📊 Monitoring & Alerts

```yaml
Key Metrics:
  - Pipeline success rate
  - Data processing duration
  - Data quality violations
  - Storage growth rate
  - Compute utilization

Alerts:
  - Pipeline failure
  - Data quality thresholds
  - Cost anomalies
  - Performance degradation

Tools:
  - Azure Monitor
  - Application Insights
  - Data Factory monitoring
  - Synapse Studio
  - Power BI dashboards
```

---

**Owner**: Data Engineer / Platform Engineer  
**Última actualización**: Diciembre 2025
