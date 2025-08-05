
# 🏆 Pipeline de Dados End-to-End com Azure Databricks

## 📋 Visão Geral do Projeto

Este projeto demonstra a implementação de uma arquitetura de dados moderna e escalável utilizando **Azure Databricks** com a metodologia **Medallion Architecture**. O projeto simula um cenário real de e-commerce, processando dados de **vendas**, **produtos**, **clientes** e **regiões** através de pipelines automatizados que seguem as melhores práticas da engenharia de dados moderna.

![Excalidraw](https://raw.githubusercontent.com/ViniciusLabruna/pipeline-vendas-azure-databricks/main/excalidraw_databricks_pipeline.png)

---

## 🎯 Objetivos Principais

- Implementar uma arquitetura de dados robusta e escalável na nuvem Azure  
- Aplicar conceitos avançados de engenharia de dados usando ferramentas de ponta  
- Demonstrar expertise em processamento de dados em tempo real e batch  
- Construir pipelines de dados automatizados e reutilizáveis  

---

## 🏗️ Arquitetura do Projeto

**Medallion Architecture** → Bronze → Silver → Gold → Power BI

```mermaid
graph TD
    A[📁 Source Data (Parquet)] --> B[🥉 Bronze Layer (Raw Data Ingestion)]
    B --> C[🥈 Silver Layer (Data Transformation & Quality)]
    C --> D[🥇 Gold Layer (Business-Ready Analytics)]
    D --> E[📊 Power BI Dashboard]
```

![Diagrama da Arquitetura](https://raw.githubusercontent.com/ViniciusLabruna/pipeline-vendas-azure-databricks/main/azure_databricks_pipeline.png)

---

## 🛠️ Stack Tecnológico

### 🔹 Cloud & Plataforma de Dados
- **Azure Databricks** – Plataforma de analytics unificada
- **Azure Data Lake Storage Gen2** – Data Lake escalável
- **Unity Catalog** – Governança de dados centralizada
- **Delta Lake** – Storage layer otimizado para analytics

### 🔹 Linguagens & Frameworks
- **Python** – Linguagem principal para transformações
- **PySpark** – Processamento distribuído de big data
- **SQL** – Queries analíticas e transformações
- **Delta Live Tables** – Framework declarativo para ETL

### 🔹 Ferramentas de Desenvolvimento
- **Databricks Notebooks** – Ambiente colaborativo de desenvolvimento
- **Databricks Workflows** – Orquestração de pipelines
- **Azure Resource Manager (ARM)** – Infraestrutura como código

---

## 🔧 Componentes Técnicos Implementados

### 1. 🥉 Bronze Layer – Ingestão de Dados

```python
df = spark.readStream.format("cloudFiles") \
  .option("cloudFiles.format", "parquet") \
  .option("cloudFiles.schemaLocation", f"abfss://bronze@databricksete1956.dfs.core.windows.net/checkpoint_{p_file_name}") \
  .load(f"abfss://source@databricksete1956.dfs.core.windows.net/{p_file_name}")
```

**Técnicas:**
- Auto Loader – Ingestão incremental
- Schema Evolution – Adaptação automática a mudanças
- Checkpointing – Exactly-once processing

---

### 2. 🥈 Silver Layer – Transformação e Qualidade

```python
from pyspark.sql.functions import *
from pyspark.sql.types import *

df_with_discount = df.withColumn("discounted_price", col("price") * 0.9)
df_cleaned = df.withColumn("brand_standardized", upper(col("brand")))
```

**Técnicas:**
- Data Quality Checks
- Window Functions
- Column Transformations
- Domain Extraction

---

### 3. 🥇 Gold Layer – Modelagem Dimensional

```python
def create_scd_type2_table(df_new, table_name):
    # Identificar registros novos e alterados
    # Criar surrogate keys
    # Manter histórico de mudanças
    pass
```

**Técnicas Avançadas:**
- Star Schema
- SCD Type 2 (Slowly Changing Dimensions)
- Surrogate Keys
- Delta Live Tables

---

### 4. 🔁 Funcionalidades Dinâmicas

```python
datasets = [
    {"file_name": "orders"},
    {"file_name": "customers"},
    {"file_name": "products"}
]
dbutils.jobs.taskValues.set("output_datasets", datasets)
```

---

## 📊 Benefícios Técnicos

### 🧠 Performance & Escalabilidade
- Particionamento Inteligente
- Z-Ordering
- Caching
- Compute Autoscaling

### 🔒 Confiabilidade & Qualidade
- ACID Transactions
- Time Travel
- Data Lineage
- Automated Testing

### 🛡️ Governança & Segurança
- Unity Catalog
- Column-Level Security
- Audit Logging
- Data Classification

---

## 🔄 Pipelines Implementados

### 🔹 Pipeline de Ingestão (Bronze)
✅ Streaming com Autoloader  
✅ Schema evolution  
✅ Checkpointing  
✅ Monitoramento contínuo  

### 🔹 Pipeline de Transformação (Silver)
✅ Limpeza e padronização  
✅ Regras de negócio  
✅ Métricas derivadas  
✅ Validação de qualidade  

### 🔹 Pipeline Analítico (Gold)
✅ Tabelas dimensionais  
✅ SCD Type 2  
✅ Otimizações analíticas  
✅ Agregações pré-computadas  

---

## 📁 Estrutura do Projeto

```bash
pipeline-vendas-azure-databricks/
├── README.md
├── Parameters.ipynb               # Configurações dinâmicas
├── Bronze_Layer.ipynb             # Ingestão de dados raw
├── Silver_Products.ipynb          # Transformação de produtos
├── Silver_Customers.ipynb         # Transformação de clientes
├── Silver_Orders.ipynb            # Transformação de pedidos
├── Silver_Regions.ipynb           # Transformação de regiões
├── Gold_Products.ipynb            # Dimensão produtos
├── Gold_Customers.ipynb           # Dimensão clientes
└── Gold_Orders.ipynb              # Fato pedidos
```

---

## 🚀 Como Executar

### ✅ Pré-requisitos
- Azure Subscription ativa  
- Azure Databricks Workspace  
- Azure Data Lake Storage Gen2  
- Unity Catalog habilitado  

### ⚙️ Configuração Rápida

```bash
# Clone o repositório
git clone https://github.com/ViniciusLabruna/pipeline-vendas-azure-databricks.git
```

1. Importe os notebooks no Databricks  
2. Configure as variáveis de ambiente (storage, containers, credenciais)  
3. Execute os notebooks na seguinte ordem:

### 📌 Ordem de Execução

1. `Parameters.ipynb` – Configuração  
2. `Bronze_Layer.ipynb` – Ingestão para cada dataset  
3. `Silver_*.ipynb` – Transformações (em paralelo)  
4. `Gold_*.ipynb` – Modelagem dimensional (em paralelo)  

---

## 🔍 Principais Aprendizados

### 📐 Arquitetura Moderna
- Medallion Architecture implementada na prática  
- Separação por camadas (Bronze, Silver, Gold)  
- Processamento incremental com performance  

### 💡 Tecnologias de Ponta
- Azure Databricks como plataforma unificada  
- Delta Lake com suporte a ACID e Time Travel  
- Unity Catalog para governança de dados  

### ⚙️ Engenharia de Dados Avançada
- Streaming com Autoloader  
- SCD Type 2 e modelagem dimensional  
- Performance tuning com Z-Ordering  

---

## 🧪 Engenharia de Dados Moderna

✅ Arquitetura Cloud-native  
✅ Streaming + Batch  
✅ Governança e Qualidade  
✅ Otimização e Escalabilidade  
✅ Design de Pipelines Reutilizáveis  

---

## 🧰 Ferramentas Enterprise

- Azure Databricks  
- PySpark  
- Delta Lake  
- Delta Live Tables  
- Unity Catalog  
- Azure Data Lake  
- Databricks Workflows  
- Azure Resource Manager  
