# 🏨 Predictive Revenue Management & BI Data Pipeline

Pipeline de Engenharia de Dados ponta a ponta desenvolvido no **Databricks**, com a **Arquitetura Medalhão (Bronze, Silver e Gold)**. O objetivo do projeto é realizar a ingestão, sanitização e enriquecimento de dados operacionais hoteleiros (reservas e ocupação) para fundamentar análises de Business Intelligence (BI) e alimentar modelos preditivos de **Revenue Management (RM)**.

---

## 🎯 Finalidade do Projeto

Este projeto foi desenvolvido como uma **solução Ponta a Ponta** que une **Engenharia e Ciência de Dados** aplicadas ao setor hoteleiro na cidade de Bombinhas - SC. 

O objetivo principal é construir uma infraestrutura robusta de dados que sustente modelos preditivos e prescritivos de **Revenue Management (RM)**, estruturada em duas frentes complementares:

---

### 🧱 1. Engenharia de Dados: Pipelines, Qualidade e Governança
Construção e orquestração de pipelines automatizados na **Arquitetura Medalhão (Bronze, Silver e Gold)** no Databricks com Unity Catalog. A engenharia garante a ingestão, tratamento, anonimização (LGPD) e consolidação de dados primários, secundários e terciários (1st, 2nd e 3rd Party Data):
* **Dados Primários:** Dados históricos internos do hotel (reservas, ocupação diária, diária média e *lead time*).
* **Dados Secundários:** Dados de vendas por canal de distribuição (Omnibees) e monitoramento automatizado de preços da concorrência (*rate scraping*).
* **Dados Terciários:** Variáveis exógenas do destino (histórico de clima, previsão do tempo, calendário de feriados, taxas de câmbio BRL/ARS/USD e dados do fluxo de entrada de veículos na cidade via TPA).

---

### 🔬 2. Ciência de Dados: Analytics Preditivo e Prescritivo (ML)
Utilização das tabelas analíticas otimizadas (Camada Gold) para desenvolver modelos estatísticos e de Machine Learning voltados a responder **três perguntas fundamentais de negócio**:

1. **Previsão de Demanda (Análise Preditiva):**  
   É possível prever com precisão a demanda por hospedagens em Bombinhas - SC combinando os dados históricos do fluxo de entrada de veiculos na cidade com variáveis externas (dados históricos e atuais das taxas de câmbio do peso argentino e dolar, dados históricos do clima e previsão do tempo, calendário de feriados)?

2. **Comportamento de Venda e Preços da Concorrência:**  
   Como o tempo de antecedência de reserva (*lead time*) varia por nacionalidade e como cruzar a velocidade de vendas do hotel (*pickup*) com a precificação dos concorrentes para identificar oportunidades de reajuste tarifário?

3. **Motor de Precificação Dinâmica (Análise Prescritiva):**  
   É viável construir um algoritmo de Machine Learning que não apenas preveja a ocupação futura, mas também atue como um **Recomendador de Tarifas** para otimizar o **RevPAR** (*Revenue Per Available Room*) do hotel?

---

## 📌 Status e Roadmap do Projeto

> **📍 Foco Atual — Fase 1.2: Camada Silver (Em Andamento)**
> A **Camada Bronze está 100% concluída**, contando com pipelines automatizados para ingestão de dados operacionais (reservas/ocupação) e exógenos (câmbio ARS/USD, clima histórico, previsão e feriados). O foco atual do projeto é a **limpeza, tipagem e tratamento de nulos na Camada Silver**.

#### Checkpoints de Desenvolvimento:

* [x] **Fase 1.1 — Camada Bronze (Concluída):**
  * [x] Dados Primários: `reservas_raw` e `ocupacao_diaria_raw` com anonimização LGPD.
  * [x] Dados Exógenos: Câmbio (ARS e USD), Clima histórico, Previsão do tempo e Feriados (2011–2027).
  * [ ] Dados Terciários (TPA): Fluxo de entrada de veículos na cidade *(⏳ Pendente — Aguardando autorização de acesso aos dados públicos da Prefeitura de Bombinhas)*.

* [ ] **Fase 1.2 — Camada Silver (Em Andamento / Foco Atual):**
  * [ ] Tratamento de nulos/zeros *dummy*, tipagem de datas/moedas (`silver.reservas` e `silver.ocupacao_diaria`).
  * [ ] Padronização, limpeza e unificação temporal das tabelas exógenas na Silver (`silver.cambio`, `silver.clima`, etc.).

* [ ] **Fase 1.3 — Camada Gold (Próximo Passo):**
  * [ ] Modelagem dimensional (Fatos e Dimensões) para dashboards de BI.
  * [ ] Consolidação do *Feature Store* unificado para Machine Learning.

* [ ] **Fase 2 — Ciência de Dados & Machine Learning:**
  * [ ] Treinamento dos modelos preditivos de demanda e algoritmo prescritivo de recomendação tarifária.

---

## 🏗️ Arquitetura dos Dados (Medallion Architecture)

```text
[ Fonte de Dados / Unity Catalog ]
                │
                ▼
   ┌──────────────────────────┐
   │    🟤 Camada Bronze      │  -> Ingestão dos dados brutos, padronização de colunas (snake_case)
   │                          │     e pseudonimização de clientes (ex: Hospede_X).
   └────────────┬─────────────┘
                │
                ▼
   ┌──────────────────────────┐
   │    ⚪ Camada Silver      │  -> Tipagem de datas/moedas, substituição de nulos/zeros 'dummy',
   │                          │     e cálculo de métricas (diárias, ADR).
   └────────────┬─────────────┘
                │
                ▼
   ┌──────────────────────────┐
   │    🟡 Camada Gold        │  -> Tabela de fatos e dimensões para dashboards de BI
   │                          │     e preparação de features para Machine Learning.
   └────────────┬─────────────┘

```
## 🛠️ Tecnologias Utilizadas

* Plataforma de Dados: Databricks com Unity Catalog

* Motor de Processamento: PySpark & Spark SQL

* Formato de Armazenamento: Delta Lake

* Linguagens: Python 3.x, SQL

* Controle de Versão: Git / GitHub

