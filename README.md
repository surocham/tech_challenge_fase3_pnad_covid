# Análise do Comportamento da População Brasileira Durante a Pandemia de COVID-19

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![BigQuery](https://img.shields.io/badge/Google_BigQuery-Cloud-orange)
![Colab](https://img.shields.io/badge/Google_Colab-Notebook-yellow)
![FIAP](https://img.shields.io/badge/FIAP-Tech_Challenge_Fase_3-red)
![Status](https://img.shields.io/badge/Status-Concluído-green)

> Tech Challenge Fase 3 — Pós-graduação em Data Analytics — FIAP  
> Autores: Edgard Joseph Kiriyama e Matheus Pavani

---

## Sumário

- [Sobre o Projeto](#sobre-o-projeto)
- [Estrutura do Repositório](#estrutura-do-repositório)
- [Base de Dados](#base-de-dados)
- [Variáveis Selecionadas](#variáveis-selecionadas)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Como Reproduzir](#como-reproduzir)
- [Banco de Dados em Nuvem](#banco-de-dados-em-nuvem)
- [Análise e Resultados](#análise-e-resultados)
- [Recomendações ao Hospital](#recomendações-ao-hospital)
- [Referências](#referências)

---

## Sobre o Projeto

Este projeto foi desenvolvido como entregável obrigatório do Tech Challenge Fase 3 da pós-graduação em Data Analytics da FIAP. O objetivo é analisar o comportamento da população brasileira durante a pandemia de COVID-19, com base nos microdados da PNAD-COVID 19 do IBGE, identificando indicadores clínicos, comportamentais e econômicos relevantes para o planejamento hospitalar em caso de novo surto da doença.

O projeto simula o trabalho de um Expert em Data Analytics contratado por um grande hospital para:

- Entender o comportamento da população na época da pandemia
- Identificar indicadores importantes para planejamento hospitalar
- Organizar uma base de dados em nuvem para análise contínua
- Gerar insights acionáveis para tomada de decisão

---

## Estrutura do Repositório

```
pnad-covid-analise/
│
├── notebook/
│   └── tech_challenge_fase3_pnad_covid.ipynb   # Notebook principal no Google Colab
│
├── graficos/
│   ├── grafico_01_sintomas_por_mes.png
│   ├── grafico_02_sintomas_por_sexo.png
│   ├── grafico_03_faixa_etaria.png
│   ├── grafico_04_regioes.png
│   ├── grafico_05_perfil_economico.png
│   ├── grafico_05b_trabalho.png
│   ├── grafico_06_plano_hospital.png
│   └── grafico_07_cor_raca.png
│
├── relatorio/
│   └── tech_challenge_fase3_relatorio.pdf      # Relatório final em ABNT
│
└── README.md
```

---

## Base de Dados

Os dados utilizados são os microdados mensais da PNAD-COVID 19, disponibilizados pelo IBGE.

| Mês | Arquivo | Entrevistados |
|---|---|---|
| Setembro/2020 | PNAD_COVID_092020.csv | 387.298 |
| Outubro/2020 | PNAD_COVID_102020.csv | 380.461 |
| Novembro/2020 | PNAD_COVID_112020.csv | 381.438 |
| **Total** | | **1.149.197** |

**Download dos microdados:** https://covid19.ibge.gov.br/pnad-covid/

---

## Variáveis Selecionadas

Foram selecionadas 20 variáveis organizadas em três eixos temáticos, conforme exigência do projeto.

### Sintomas Clínicos

| Variável | Descrição |
|---|---|
| B0011 | Teve febre? |
| B0012 | Teve tosse? |
| B0013 | Teve dificuldade para respirar? |
| B0014 | Teve dor de cabeça? |
| B0015 | Teve dor no peito? |
| B002 | Teve algum sintoma na semana passada? |
| B0103 | Buscou atendimento em hospital? |

### Comportamento da População

| Variável | Descrição |
|---|---|
| A002 | Idade |
| A003 | Sexo |
| A004 | Cor ou raça |
| B006 | Ficou em casa na semana passada? |
| B009B | Tipo de estabelecimento de saúde buscado |
| B0101 | Buscou atendimento em posto de saúde? |
| B011 | Tem plano de saúde? |

### Características Econômicas

| Variável | Descrição |
|---|---|
| C001 | Trabalhou na semana passada? |
| C002 | Foi afastado do trabalho? |
| C007 | Setor de atividade |
| C01012 | Rendimento habitual do trabalho (R$) |
| D0011 | Número de moradores no domicílio |
| UF | Unidade da Federação |

---

## Tecnologias Utilizadas

| Ferramenta | Uso | Custo |
|---|---|---|
| Python 3.10+ | Linguagem principal de análise | Gratuito |
| Google Colab | Ambiente de desenvolvimento | Gratuito |
| Google BigQuery | Banco de dados em nuvem | Gratuito (até 10 GB) |
| Google Cloud | Plataforma de nuvem | Gratuito |
| pandas | Manipulação de dados | Gratuito |
| matplotlib | Visualização de dados | Gratuito |
| seaborn | Visualização estatística | Gratuito |
| plotly | Gráficos interativos | Gratuito |

---

## Como Reproduzir

### Pré-requisitos

- Conta Google (Gmail)
- Acesso ao Google Colab: https://colab.research.google.com
- Acesso ao Google Cloud: https://console.cloud.google.com
- Arquivos de microdados baixados do IBGE

### Passo 1 — Configurar o Google Cloud

1. Acesse https://console.cloud.google.com
2. Crie um novo projeto com o nome `pnad-covid-fiap`
3. Anote o ID do projeto gerado (ex: `pnad-covid-19-494513`)
4. Acesse o BigQuery e crie um dataset chamado `pnad_covid`

### Passo 2 — Configurar o Google Colab

1. Acesse https://colab.research.google.com
2. Abra o notebook `tech_challenge_fase3_pnad_covid.ipynb`
3. Faça upload dos três arquivos CSV dos microdados

### Passo 3 — Instalar as dependências

```python
!pip install pandas matplotlib seaborn plotly google-cloud-bigquery db-dtypes openpyxl pandas-gbq
```

### Passo 4 — Autenticar e conectar ao BigQuery

```python
from google.colab import auth
from google.cloud import bigquery
import pandas_gbq

auth.authenticate_user()

PROJECT_ID = "seu-projeto-id"
client = bigquery.Client(project=PROJECT_ID)
```

### Passo 5 — Carregar os dados

```python
colunas = [
    'UF', 'A002', 'A003', 'A004',
    'B0011', 'B0012', 'B0013', 'B0014', 'B0015',
    'B002', 'B0103', 'B006', 'B009B', 'B0101', 'B011',
    'C001', 'C002', 'C007', 'C01012', 'D0011'
]

import pandas as pd

df_set = pd.read_csv('PNAD_COVID_092020.csv', sep=',', usecols=colunas)
df_set['mes'] = 'Setembro'
df_set['mes_num'] = 9

df_out = pd.read_csv('PNAD_COVID_102020.csv', sep=',', usecols=colunas)
df_out['mes'] = 'Outubro'
df_out['mes_num'] = 10

df_nov = pd.read_csv('PNAD_COVID_112020.csv', sep=',', usecols=colunas)
df_nov['mes'] = 'Novembro'
df_nov['mes_num'] = 11

df = pd.concat([df_set, df_out, df_nov], ignore_index=True)
```

### Passo 6 — Enviar para o BigQuery

```python
pandas_gbq.to_gbq(
    df,
    destination_table='pnad_covid.microdados',
    project_id=PROJECT_ID,
    if_exists='replace',
    progress_bar=True
)
```

### Passo 7 — Consultas SQL no BigQuery

```sql
-- Sintomas por mês
SELECT
  mes,
  mes_num,
  COUNT(*) AS total_entrevistados,
  ROUND(AVG(A002), 1) AS idade_media,
  COUNTIF(B0011 = 1) AS total_com_febre,
  COUNTIF(B0012 = 1) AS total_com_tosse,
  COUNTIF(B0013 = 1) AS total_com_dif_respirar
FROM `projeto-id.pnad_covid.microdados`
GROUP BY mes, mes_num
ORDER BY mes_num
```

```sql
-- Perfil econômico por mês
SELECT
  mes,
  COUNTIF(C001 = 1) AS trabalharam,
  COUNTIF(C001 = 2) AS nao_trabalharam,
  COUNTIF(C002 = 1) AS afastados,
  ROUND(AVG(CASE WHEN C01012 > 0 THEN C01012 END), 2) AS renda_media,
  COUNTIF(B011 = 1) AS tem_plano_saude,
  COUNTIF(B011 = 2) AS nao_tem_plano_saude
FROM `projeto-id.pnad_covid.microdados`
GROUP BY mes, mes_num
ORDER BY mes_num
```

```sql
-- Sintomas por região
SELECT
  regiao,
  mes,
  COUNT(*) AS total,
  COUNTIF(B0011 = 1) AS febre,
  COUNTIF(B0012 = 1) AS tosse,
  COUNTIF(B0013 = 1) AS dif_respirar,
  COUNTIF(B0103 = 1) AS foram_ao_hospital
FROM `projeto-id.pnad_covid.microdados`
GROUP BY regiao, mes, mes_num
ORDER BY mes_num, regiao
```

---

## Banco de Dados em Nuvem

Os dados foram armazenados no Google BigQuery com a seguinte estrutura:

```
Projeto: pnad-covid-19-494513
  Dataset: pnad_covid
    Tabela: microdados
      Linhas: 1.149.197
      Colunas: 26
```

---

## Análise e Resultados

### Sintomas Clínicos

- A dor no peito foi o sintoma com maior prevalência nos três meses
- A tosse se manteve como segundo sintoma mais frequente
- A dificuldade para respirar apresentou leve crescimento em novembro, sinalizando agravamento dos casos
- A faixa etária de 30 a 59 anos concentrou o maior número absoluto de casos

### Comportamento da População

- Mulheres representaram mais de 53% dos casos de febre nos três meses
- O Nordeste apresentou o maior número absoluto de casos, seguido do Sudeste
- Novembro registrou crescimento de casos no Nordeste e Sudeste, sinalizando início da segunda onda
- A população parda concentrou o maior número de casos, refletindo desigualdades sociais

### Características Econômicas

- Apenas 37% da população trabalhava formalmente no período analisado
- Renda média dos trabalhadores: R$ 2.239 em setembro, R$ 2.217 em outubro e R$ 2.216 em novembro
- Mais de 90% da população não possuía plano de saúde privado
- Cerca de 5% dos entrevistados buscou atendimento hospitalar em cada mês

---

## Recomendações ao Hospital

Com base na análise dos dados, as principais recomendações para planejamento hospitalar em caso de novo surto são:

1. **Ampliar capacidade de atendimento respiratório** — manter estoque adequado de oxigênio e equipamentos de ventilação mecânica
2. **Preparar para alta demanda do SUS** — mais de 90% da população depende do sistema público
3. **Priorizar faixa etária de 30 a 59 anos** — maior número absoluto de casos
4. **Protocolos específicos para idosos** — maior risco de complicações graves acima de 60 anos
5. **Atendimento humanizado para população vulnerável** — baixa renda e ausência de plano de saúde aumentam vulnerabilidade
6. **Implementar monitoramento contínuo** — dados mostram que novembro sinalizou crescimento de casos em múltiplas regiões

---

## Referências

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA. **PNAD COVID19**: microdados. Rio de Janeiro: IBGE, 2020. Disponível em: https://covid19.ibge.gov.br/pnad-covid/. Acesso em: 26 abr. 2026.

INSTITUTO BRASILEIRO DE GEOGRAFIA E ESTATÍSTICA. **PNAD COVID19**: nota técnica. Rio de Janeiro: IBGE, 2020. Disponível em: https://covid19.ibge.gov.br/pnad-covid/. Acesso em: 26 abr. 2026.

GOOGLE. **BigQuery**: data warehouse em nuvem. Disponível em: https://cloud.google.com/bigquery. Acesso em: 26 abr. 2026.

HUNTER, John D. Matplotlib: a 2D graphics environment. **Computing in Science and Engineering**, v. 9, n. 3, p. 90-95, 2007.

MCKINNEY, Wes. **Python para análise de dados**. 2. ed. São Paulo: Novatec, 2019.

---

## Licença

Este projeto foi desenvolvido para fins acadêmicos como parte da pós-graduação em Data Analytics da FIAP.
