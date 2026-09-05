# 📖 Dicionário de Dados

## Registro de Ocupação Hospitalar COVID-19

Este documento descreve as variáveis presentes na base de dados de
**Registro de Ocupação Hospitalar COVID-19**, disponibilizada pelo
Ministério da Saúde por meio do DataSUS e do sistema e-SUS Notifica.

O dicionário foi construído com base:

- na documentação oficial do e-SUS Notifica;
- no conjunto de dados disponibilizado no Portal Brasileiro de Dados Abertos;
- na estrutura observada no arquivo referente ao ano de 2020.

> **Importante:** algumas variáveis presentes no CSV são campos técnicos
> do sistema e não possuem descrição detalhada no dicionário oficial de
> leitos consultado. Esses campos estão identificados neste documento
> como "metadados técnicos" e não serão interpretados como variáveis
> analíticas sem validação adicional.

---

## 🗂️ Estrutura da base de 2020

A base utilizada possui:

- **554.706 registros**
- **26 variáveis**

---

## 📊 Dicionário das Variáveis

| Variável | Grupo | Descrição | Tipo recomendado no R | Uso na análise |
|---|---|---|---|---|
| `V1` | Técnico | Coluna auxiliar presente na exportação do CSV, aparentemente utilizada como índice das linhas. Não faz parte do conjunto de variáveis de ocupação documentadas pelo DataSUS. | `integer` | Não |
| `_id` | Técnico | Identificador interno do registro no sistema. Não possui descrição específica no dicionário oficial de leitos consultado. | `character` | Não |
| `dataNotificacao` | Temporal | Data associada à notificação do registro de ocupação hospitalar. | `Date` | Sim |
| `cnes` | Identificação | Código do estabelecimento de saúde no Cadastro Nacional de Estabelecimentos de Saúde (CNES). | `character` | Sim |
| `ocupacaoSuspeitoCli` | Ocupação COVID-19 | Quantidade associada à ocupação de leitos clínicos/enfermaria por casos suspeitos de COVID-19/SRAG. Campo presente na base de 2020, mas não detalhado individualmente no manual de leitos consultado. | `integer` | Sim |
| `ocupacaoSuspeitoUti` | Ocupação COVID-19 | Quantidade associada à ocupação de leitos de UTI por casos suspeitos de COVID-19/SRAG. Campo presente na base de 2020, mas não detalhado individualmente no manual de leitos consultado. | `integer` | Sim |
| `ocupacaoConfirmadoCli` | Ocupação COVID-19 | Quantidade associada à ocupação de leitos clínicos/enfermaria por casos confirmados de COVID-19/SRAG. Campo presente na base de 2020, mas não detalhado individualmente no manual de leitos consultado. | `integer` | Sim |
| `ocupacaoConfirmadoUti` | Ocupação COVID-19 | Quantidade associada à ocupação de leitos de UTI por casos confirmados de COVID-19/SRAG. Campo presente na base de 2020, mas não detalhado individualmente no manual de leitos consultado. | `integer` | Sim |
| `ocupacaoCovidCli` | Ocupação COVID-19 | Ocupação de leitos clínicos/enfermaria destinados a SRAG/COVID-19, correspondente à soma de casos suspeitos e confirmados. | `integer` | Sim |
| `ocupacaoCovidUti` | Ocupação COVID-19 | Ocupação de leitos de UTI destinados a SRAG/COVID-19, correspondente à soma de casos suspeitos e confirmados. | `integer` | Sim |
| `ocupacaoHospitalarCli` | Ocupação hospitalar | Ocupação total de leitos clínicos/enfermaria. Inclui suspeitos e confirmados de SRAG/COVID-19 e pacientes internados por outras patologias. | `integer` | Sim |
| `ocupacaoHospitalarUti` | Ocupação hospitalar | Ocupação total de leitos de UTI. Inclui suspeitos e confirmados de SRAG/COVID-19 e pacientes internados por outras patologias. | `integer` | Sim |
| `saidaSuspeitaObitos` | Saídas hospitalares | Quantidade de óbitos registrados entre os casos classificados como suspeitos. | `integer` | Sim |
| `saidaSuspeitaAltas` | Saídas hospitalares | Quantidade de altas registradas entre os casos classificados como suspeitos. | `integer` | Sim |
| `saidaConfirmadaObitos` | Saídas hospitalares | Quantidade de óbitos registrados entre os casos confirmados. | `integer` | Sim |
| `saidaConfirmadaAltas` | Saídas hospitalares | Quantidade de altas registradas entre os casos confirmados. | `integer` | Sim |
| `origem` | Técnico | Campo relacionado à origem do registro no sistema. Seu significado detalhado não está especificado no dicionário oficial de leitos consultado e deverá ser investigado antes de qualquer utilização analítica. | `character` | Investigar |
| `_p_usuario` | Técnico | Campo interno associado ao usuário do sistema responsável pelo registro. Não é uma variável de ocupação hospitalar documentada para análise. | `character` | Não |
| `estadoNotificacao` | Geográfica | Estado associado à notificação do registro. | `character` | Sim |
| `municipioNotificacao` | Geográfica | Município associado à notificação do registro. | `character` | Sim |
| `estado` | Geográfica | Estado associado ao registro. O manual oficial apresenta este campo separadamente de `estadoNotificacao`, mas não detalha no dicionário de leitos consultado a diferença operacional entre os dois. | `character` | Sim / Investigar |
| `municipio` | Geográfica | Município associado ao registro. O manual apresenta este campo separadamente de `municipioNotificacao`, sendo recomendável verificar empiricamente as diferenças entre eles antes da análise geográfica. | `character` | Sim / Investigar |
| `excluido` | Técnico | Indicador interno aparentemente relacionado à situação de exclusão do registro. Não possui definição detalhada no dicionário oficial de leitos consultado. | `logical` | Investigar |
| `validado` | Técnico | Indicador interno aparentemente relacionado à situação de validação do registro. Não possui definição detalhada no dicionário oficial de leitos consultado. | `logical` | Investigar |
| `_created_at` | Técnico / Temporal | Data e horário técnicos associados à criação do registro no sistema. Não corresponde necessariamente à data da ocorrência hospitalar. | `POSIXct` | Não / Auditoria |
| `_updated_at` | Técnico / Temporal | Data e horário técnicos associados à última atualização do registro no sistema. | `POSIXct` | Não / Auditoria |

---

# 🏥 Grupos de Variáveis

## 1. Identificação do estabelecimento

### `cnes`

Código utilizado para identificar o estabelecimento de saúde.

Essa variável permite, por exemplo:

- identificar registros referentes ao mesmo estabelecimento;
- analisar a quantidade de estabelecimentos presentes na base;
- realizar agregações por unidade de saúde;
- eventualmente relacionar os dados com outras bases do CNES.

O CNES deve ser tratado preferencialmente como uma variável
**categórica/identificadora**, e não como uma variável numérica para
cálculos.

---

# 📅 2. Variável Temporal

### `dataNotificacao`

Representa a data associada ao registro/notificação da ocupação.

Será uma das principais variáveis do projeto, pois permite construir
análises como:

- ocupação ao longo do tempo;
- evolução mensal;
- identificação de períodos críticos;
- comparação entre meses;
- comparação entre anos.

No R, a variável deverá ser convertida para o tipo `Date`.

---

# 🦠 3. Ocupação por COVID-19 / SRAG

## Casos suspeitos

### `ocupacaoSuspeitoCli`

Quantidade associada à ocupação de leitos clínicos/enfermaria por
pacientes classificados como casos suspeitos.

### `ocupacaoSuspeitoUti`

Quantidade associada à ocupação de leitos de UTI por pacientes
classificados como casos suspeitos.

---

## Casos confirmados

### `ocupacaoConfirmadoCli`

Quantidade associada à ocupação de leitos clínicos/enfermaria por
casos confirmados.

### `ocupacaoConfirmadoUti`

Quantidade associada à ocupação de leitos de UTI por casos
confirmados.

---

## Ocupação total SRAG/COVID-19

### `ocupacaoCovidCli`

Representa a ocupação dos leitos clínicos/enfermaria relacionada
a SRAG/COVID-19.

Segundo o manual do e-SUS Notifica:

**ocupação COVID clínica = suspeitos + confirmados SRAG/COVID**

---

### `ocupacaoCovidUti`

Representa a ocupação de leitos de UTI relacionada a
SRAG/COVID-19.

Segundo o manual:

**ocupação COVID UTI = suspeitos + confirmados SRAG/COVID**

---

# 🏨 4. Ocupação Hospitalar Total

É importante distinguir essas variáveis das variáveis de ocupação
específica de COVID-19.

## `ocupacaoHospitalarCli`

Representa a ocupação **total dos leitos clínicos/enfermaria**.

Inclui:

- casos suspeitos de SRAG/COVID-19;
- casos confirmados de SRAG/COVID-19;
- pacientes internados por outras patologias.

Portanto:

**ocupação hospitalar total não representa apenas pacientes com
COVID-19.**

---

## `ocupacaoHospitalarUti`

Representa a ocupação **total de leitos de UTI**.

Inclui:

- casos suspeitos de SRAG/COVID-19;
- casos confirmados de SRAG/COVID-19;
- internações decorrentes de outras patologias.

---

# 🚪 5. Saídas Hospitalares

As variáveis de saída permitem analisar altas e óbitos registrados
nos estabelecimentos.

## Casos suspeitos

### `saidaSuspeitaObitos`

Quantidade de óbitos registrados entre casos classificados como
suspeitos.

### `saidaSuspeitaAltas`

Quantidade de altas registradas entre casos classificados como
suspeitos.

---

## Casos confirmados

### `saidaConfirmadaObitos`

Quantidade de óbitos registrados entre casos confirmados.

### `saidaConfirmadaAltas`

Quantidade de altas registradas entre casos confirmados.

---

# 🗺️ 6. Variáveis Geográficas

## `estadoNotificacao`

Estado associado à notificação.

## `municipioNotificacao`

Município associado à notificação.

## `estado`

Estado presente no registro.

## `municipio`

Município presente no registro.

Antes da análise geográfica será verificado se:

- `estado` e `estadoNotificacao` possuem os mesmos valores;
- `municipio` e `municipioNotificacao` possuem os mesmos valores;
- existem divergências entre o local do registro e o local da
  notificação.

Essa verificação será realizada antes da escolha das variáveis
geográficas utilizadas na análise.

---

# ⚙️ 7. Metadados Técnicos

As variáveis abaixo fazem parte da estrutura técnica do arquivo e não
representam diretamente características da ocupação hospitalar:

- `V1`
- `_id`
- `origem`
- `_p_usuario`
- `excluido`
- `validado`
- `_created_at`
- `_updated_at`

Essas variáveis serão estudadas durante a etapa de entendimento dos
dados antes de qualquer decisão de exclusão.

Campos não descritos explicitamente pelo dicionário oficial não terão
seu significado presumido durante a análise.

---

# ⚠️ Observação importante sobre valores ausentes

A documentação utilizada para o envio dos dados de leitos informa
que os campos quantitativos devem ser preenchidos utilizando números
inteiros.

A documentação também orienta que, quando o quantitativo for igual a
zero, o campo seja deixado em branco.

Essa característica é especialmente importante durante o tratamento
de valores ausentes.

Dessa forma, valores `NA` encontrados nas variáveis quantitativas
não serão automaticamente removidos ou substituídos antes da análise
do padrão de preenchimento dos dados.

Será necessário avaliar se o valor ausente representa:

1. ausência de informação;
2. quantidade igual a zero;
3. problema de preenchimento;
4. diferença na estrutura dos dados entre períodos.

---

# 🔄 Diferenças entre os anos

Os dados estão disponíveis para os anos de 2020, 2021 e 2022.

A partir de 2022, novos campos foram acrescentados ao sistema para
descrever a ocupação dos leitos.

Por esse motivo, antes da integração das bases será realizada uma
comparação da estrutura dos arquivos:

- variáveis existentes em 2020;
- variáveis existentes em 2021;
- variáveis existentes em 2022;
- variáveis comuns aos três períodos;
- variáveis exclusivas de determinados períodos.

Somente após essa etapa será definida a estratégia para integração
dos dados.

---

# 🔎 Variáveis prioritárias para a análise

Inicialmente, as seguintes variáveis serão consideradas prioritárias:

| Dimensão | Variáveis |
|---|---|
| Tempo | `dataNotificacao` |
| Estabelecimento | `cnes` |
| Localização | `estado`, `municipio`, `estadoNotificacao`, `municipioNotificacao` |
| Ocupação COVID clínica | `ocupacaoCovidCli` |
| Ocupação COVID UTI | `ocupacaoCovidUti` |
| Ocupação hospitalar clínica | `ocupacaoHospitalarCli` |
| Ocupação hospitalar UTI | `ocupacaoHospitalarUti` |
| Altas | `saidaSuspeitaAltas`, `saidaConfirmadaAltas` |
| Óbitos | `saidaSuspeitaObitos`, `saidaConfirmadaObitos` |

A seleção definitiva será realizada após a análise de qualidade,
completude e consistência das variáveis.

---

# 📚 Fontes

- Ministério da Saúde
- DataSUS
- e-SUS Notifica
- Manual de Envio de Dados do e-SUS Notifica
- Dicionário dos Dados de Leitos
- Portal Brasileiro de Dados Abertos — Registro de Ocupação Hospitalar COVID-19

---

## 📝 Nota metodológica

Este dicionário poderá ser atualizado durante o desenvolvimento do
projeto caso sejam encontradas novas informações sobre a estrutura,
preenchimento ou significado das variáveis.

A documentação das decisões tomadas durante a análise faz parte do
processo de construção deste projeto.
