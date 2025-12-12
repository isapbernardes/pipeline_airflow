# 🚗 NovaDrive: Modern Data Stack ELT

> **Pipeline de Engenharia de Dados ponta a ponta: AWS, Airflow, Snowflake, dbt e Looker.**

Projeto prático simulando a modernização de dados de um e-commerce automotivo. O objetivo foi sair de um banco transacional isolado para um **Data Lakehouse** com governança e análise em tempo real.

---

## 🛠️ Tech Stack
* **Cloud & Infra:** AWS EC2 (T2.Micro), Linux Ubuntu, Docker.
* **Orquestração:** Apache Airflow (Python).
* **Data Warehouse:** Snowflake.
* **Engenharia de Analytics:** dbt Core & Cloud (Modelagem Star Schema).
* **Visualização:** Looker Studio.

---

## 🚀 Diferenciais de Engenharia (Desafios Reais)

Este projeto vai além do básico, implementando soluções para problemas reais de produção:

### 1. Robustez na Ingestão (Airflow)
* **Carga Incremental:** Pipeline otimizado para buscar apenas novos registros (CDC lógico via `MAX(ID)`).
* **Tratamento de Concorrência:** Solução de *Race Conditions* e duplicidade de dados utilizando travas de execução (`max_active_runs=1`) e limpeza via SQL (`QUALIFY`).

### 2. Infraestrutura e Segurança (AWS/Networking)
* Configuração manual de **Security Groups** na AWS e tunelamento para acesso seguro ao banco de dados.

### 3. Governança e Transformação (dbt)
* **Ambiente Cloud:** Utilização do dbt Cloud para orquestrar as transformações de dados, garantindo que o processamento ocorra em um ambiente controlado fora da máquina local.
* **Execução de Pipelines:** Configuração de Jobs de Deploy para materializar as tabelas Fato e Dimensão no Data Warehouse (Schema `ANALYTIC`).
* **Testes de Regra de Negócio:** Implementação de testes personalizados (*Singular Tests*) utilizando SQL e Jinja para auditar a integridade financeira das vendas (ex: verificar descontos acima do permitido).

---

## 📸 Resultados

### Orquestração e Monitoramento
O Airflow gerenciando as dependências e executando o pipeline com sucesso.
![Grid do Airflow](./images/dag.png)

### Linhagem de Dados (Data Lineage)
Visualização do dbt mostrando o fluxo de transformação: de dados brutos (Stage) para o modelo dimensional (Fatos e Dimensões).
![Linhagem dbt](./images/linhagem.png)

### Visualização Final
Dashboard no Looker Studio consumindo a tabela `fct_vendas` processada.
![Dashboard Looker](./images/vendas_concessionarias.png)

---

### Autor
**Isadora**
[Linkedin: https://www.linkedin.com/in/isadorapbernards]
