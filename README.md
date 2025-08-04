<<<<<<< HEAD
# Pipeline de Dados de Vendas com Azure Databricks e Arquitetura Medallion

Este repositório contém o código para uma pipeline de Engenharia de Dados que processa dados de vendas (clientes, produtos, pedidos) utilizando Azure Databricks. A arquitetura segue o padrão **Medallion (Bronze, Silver, Gold)** para garantir qualidade, governança e performance.

---

### 🎯 Objetivo do Projeto

O principal objetivo é transformar dados brutos (vindos de um Data Lake) em um modelo de dados dimensional (Star Schema) na camada Gold, pronto para ser consumido por ferramentas de Business Intelligence como Power BI ou Tableau para análises gerenciais.

---

### 🛠️ Arquitetura e Ferramentas

A pipeline utiliza uma combinação de tecnologias nativas do ecossistema Azure e Databricks para construir um fluxo de dados robusto e escalável.

**Diagrama do Fluxo de Dados:**
```
graph TD
    A[Fonte de Dados <br> (ADLS Gen2)] -->|Notebook Bronze_Layer.ipynb <br> (Auto Loader)| B(Camada Bronze <br> Raw Data);
    B -->|Notebooks Silver_* <br> (PySpark/SQL)| C(Camada Silver <br> Dados Limpos e Enriquecidos);
    C -->|Notebooks Gold_* <br> (PySpark/DLT)| D(Camada Gold <br> Modelos de Negócio);
    D --> E[Analytics e BI <br> (Power BI, etc.)];
```

*   **Cloud:** Microsoft Azure
*   **Processamento:** Azure Databricks (com PySpark e SQL)
*   **Armazenamento:** Azure Data Lake Storage (ADLS) Gen2
*   **Formato dos Dados:** Delta Lake
*   **Orquestração:** Databricks Jobs
*   **Modelagem Dimensional:**
    *   **DimCustomer:** Implementado como **SCD Tipo 1** (Slowly Changing Dimension que sobrescreve os dados).
    *   **DimProducts:** Implementado como **SCD Tipo 2** (Slowly Changing Dimension que mantém o histórico de mudanças) usando Delta Live Tables (DLT).
    *   **FactOrders:** Tabela fato que conecta as dimensões e contém as métricas de negócio.

---

### 📂 Estrutura dos Notebooks

*   **Camada Bronze (`Bronze_Layer.ipynb`):** Ingestão incremental dos dados brutos utilizando o Auto Loader do Databricks.
*   **Camada Silver (`Silver_*.ipynb`):** Scripts para limpeza, padronização e enriquecimento dos dados. Cada script é focado em uma entidade (clientes, pedidos, produtos).
*   **Camada Gold (`Gold_*.ipynb`):** Construção do modelo dimensional, aplicando regras de negócio e criando as tabelas dimensão e fato.

---

### 🚀 Como Executar

Este projeto foi desenhado para ser executado como um **Job no Databricks**.

1.  **Clone o Repositório:** Utilize a funcionalidade "Repos" no Databricks para clonar este projeto do GitHub.
2.  **Configure as Conexões:** Assegure que o cluster do Databricks possui as permissões necessárias para ler e escrever no Azure Data Lake Storage.
3.  **Execute o Job:** Orquestre a execução dos notebooks na sequência correta: Bronze -> Silver -> Gold. Utilize a parametrização dos notebooks, como `init_load_flag`, para controlar o comportamento da carga (inicial vs. incremental).

---
```

=======
README
>>>>>>> 762966cd72bb380b7931b7e1e9fd47054d5cc609
