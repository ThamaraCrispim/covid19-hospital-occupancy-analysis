# Análise da Ocupação Hospitalar por COVID-19 no Brasil

## Sobre o projeto

Este projeto tem como objetivo realizar uma análise exploratória dos dados de ocupação hospitalar relacionados à COVID-19 no Brasil.

A análise utiliza dados públicos disponibilizados pelo Ministério da Saúde, por meio do DataSUS, referentes à ocupação de **leitos clínicos e de Unidade de Terapia Intensiva (UTI)** destinados ao atendimento de pacientes com casos suspeitos ou confirmados de COVID-19 / Síndrome Respiratória Aguda Grave (SRAG).

O projeto busca aplicar técnicas de preparação, limpeza, exploração e visualização de dados para compreender o comportamento da ocupação hospitalar ao longo do período analisado.

---

##  Objetivos

O principal objetivo deste projeto é explorar os dados de ocupação hospitalar e identificar padrões relevantes relacionados à utilização de leitos durante a pandemia de COVID-19.

Entre os objetivos específicos estão:

- analisar a evolução da ocupação hospitalar ao longo do tempo;
- identificar períodos de maior ocupação;
- comparar a ocupação entre diferentes regiões ou estados;
- analisar a distribuição de leitos clínicos e de UTI;
- identificar valores ausentes, inconsistências e possíveis duplicidades;
- criar visualizações que facilitem a interpretação dos dados;
- apresentar os principais insights encontrados durante a análise.

---

##  Fonte dos Dados — DataSUS

O Ministério da Saúde, por meio da **Secretaria de Atenção Especializada em Saúde (SAES)**, implementou, devido à pandemia de COVID-19, o registro das internações por meio do **Sistema e-SUS Notifica — Módulo Internações SUS**.

O banco de dados de ocupação hospitalar está disponível a partir de **abril de 2020** e reúne informações referentes à ocupação dos estabelecimentos de saúde.

O Módulo Internações foi desenvolvido para registrar a ocupação de:

- leitos clínicos SUS;
- leitos de Unidade de Terapia Intensiva (UTI);
- atendimentos destinados a pacientes com casos suspeitos ou confirmados de COVID-19 / SRAG.

Alguns estados possuem sistemas próprios de registro de ocupação. Nesses casos, foi disponibilizada uma API para transferência dos dados estaduais para o sistema **e-SUS Notifica — Módulo Internações SUS**.

Devido ao grande volume de registros, alguns estados possuem mais de **um milhão de observações**, fazendo com que os dados sejam disponibilizados em formato CSV e demandem ferramentas adequadas para processamento e análise.

A partir de **2022**, novos campos foram adicionados ao conjunto de dados. Por esse motivo, registros anteriores a 2022 não apresentam preenchimento para essas variáveis.

### 🔗 Fonte oficial

[Portal Brasileiro de Dados Abertos — Registro de Ocupação Hospitalar COVID-19](https://dados.gov.br/dados/conjuntos-dados/registro-de-ocupacao-hospitalar-covid-19)

---

## 🔎 Etapas da Análise

O desenvolvimento do projeto será dividido nas seguintes etapas:

### 1. Entendimento dos Dados

- identificação das variáveis disponíveis;
- análise da estrutura do conjunto de dados;
- verificação dos tipos das variáveis;
- compreensão da unidade de observação;
- identificação do período disponível.

### 2. Limpeza e Preparação

Serão avaliados:

- valores ausentes;
- registros duplicados;
- tipos incorretos de dados;
- padronização das datas;
- possíveis inconsistências nos registros;
- variáveis necessárias para a análise.

### 3. Análise Exploratória de Dados

Serão realizadas análises **univariadas e bivariadas** para compreender a distribuição e o comportamento das principais variáveis.

Algumas análises previstas incluem:

- distribuição da ocupação hospitalar;
- comportamento da ocupação ao longo do tempo;
- comparação entre estados e regiões;
- análise de leitos clínicos;
- análise de leitos de UTI.

### 4. Análise Temporal

A análise temporal buscará identificar:

- evolução da ocupação;
- períodos de crescimento e redução;
- possíveis picos de ocupação;
- diferenças entre os períodos analisados.

### 5. Análise Geográfica

A análise geográfica será utilizada para investigar diferenças na ocupação hospitalar entre diferentes localidades.

### 6. Visualização dos Dados

Serão utilizados diferentes tipos de gráficos, de acordo com a característica da análise, incluindo:

- gráficos de barras;
- gráficos de linhas;
- mapas de calor;
- outras visualizações consideradas adequadas durante a exploração.

---

## 💡 Pergunta Norteadora

> Como a ocupação de leitos clínicos e de UTI destinados ao atendimento de casos de COVID-19/SRAG evoluiu ao longo do período analisado e quais localidades apresentaram os períodos de maior ocupação?

---

## 🛠️ Tecnologias

Este projeto será desenvolvido utilizando **R**, seguindo uma abordagem
voltada à análise estatística e exploração de dados.

Principais ferramentas:

- R
- RStudio
- data.table
- dplyr
- tidyr
- ggplot2
- lubridate
- plotly
---

## 📁 Estrutura do Projeto

```text
covid19-hospital-occupancy-analysis/
│
├── data/
│   └── README.md
│
├── notebooks/
│   ├── 01_entendimento_dos_dados.ipynb
│   ├── 02_limpeza_dos_dados.ipynb
│   └── 03_analise_exploratoria.ipynb
│
├── images/
│
├── README.md
│
└── requirements.txt
