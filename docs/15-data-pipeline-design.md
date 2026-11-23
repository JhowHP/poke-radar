# PokéRadar - Data Pipeline Design

**Projeto:** PokéRadar
**Documento:** Data Pipeline Design
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                                 | Alteração                                           |
| ------ | ---------- | ------------------------------------- | --------------------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT (OpenAI) | Criação inicial da arquitetura de pipeline de dados |

---

# Sumário

1. Objetivo
2. Conceito do Pipeline
3. Arquitetura Geral
4. Camadas de Dados
5. Fluxo de Coleta
6. Dados Brutos
7. Normalização
8. Persistência
9. Processamento Analítico
10. Geração de Inteligência
11. Atualização do Dashboard
12. Controle de Qualidade
13. Histórico e Auditoria
14. Escalabilidade
15. Evolução Futura

---

# 1. Objetivo

Este documento define a arquitetura de processamento de dados do PokéRadar.

O objetivo é estabelecer como os dados serão:

* coletados;
* armazenados;
* tratados;
* analisados;
* transformados em inteligência.

---

# 2. Conceito do Pipeline

O Data Pipeline representa o caminho completo que uma informação percorre dentro da plataforma.

Exemplo:

Um preço encontrado na Amazon:

```text
R$219,90
```

deve passar por:

```text
Captura

↓

Validação

↓

Normalização

↓

Armazenamento

↓

Análise

↓

Recomendação
```

---

# 3. Arquitetura Geral

Fluxo principal:

```text
                  Fontes Externas

                         |

                         ↓

                    Collectors

                         |

                         ↓

                  Raw Data Layer

                         |

                         ↓

              Normalization Layer

                         |

                         ↓

                   PostgreSQL

                         |

                         ↓

                    PIE Engine

                         |

                         ↓

                 Intelligence Layer

                         |

                         ↓

               Dashboard / Alertas
```

---

# 4. Camadas de Dados

O PokéRadar utilizará separação por camadas.

---

# Raw Data Layer

Responsável por armazenar dados exatamente como foram coletados.

Exemplo:

```json
{
"title":
"Pokemon ETB Scarlet",

"price":
"R$219,90",

"source":
"amazon"
}
```

---

Objetivo:

* auditoria;
* reprocessamento;
* análise futura.

---

# Normalization Layer

Responsável por transformar diferentes formatos em um padrão.

Exemplo:

Antes:

```text
Preço: R$219,90
```

Depois:

```json
{
"price":219.90
}
```

---

# Business Layer

Dados já tratados.

Exemplo:

```text
Produto

Oferta

Histórico

Score
```

---

# Intelligence Layer

Dados gerados pelo PIE.

Exemplo:

```json
{
"POS":92,

"recommendation":
"BUY"
}
```

---

# 5. Fluxo de Coleta

Processo:

```text
Scheduler

↓

Executa Collector

↓

Consulta Loja

↓

Captura Produto

↓

Salva Raw Data

↓

Normaliza

↓

Atualiza Banco
```

---

# 6. Dados Brutos

Toda coleta deverá gerar um registro bruto.

Exemplo:

Tabela futura:

```text
collector_raw_data
```

Possíveis campos:

| Campo      | Descrição       |
| ---------- | --------------- |
| id         | Identificador   |
| source     | Origem          |
| payload    | Dados originais |
| created_at | Data coleta     |

---

Motivo:

Caso uma regra seja alterada, poderemos reprocessar dados antigos.

---

# 7. Normalização

Cada loja possui uma estrutura diferente.

Exemplo:

Amazon:

```text
product_title
```

Mercado Livre:

```text
title
```

Ri Happy:

```text
name
```

---

Resultado interno:

```json
{
"name":
"Elite Trainer Box Pokémon",

"price":
249.90,

"store":
"ri_happy"
}
```

---

A normalização deverá tratar:

* nomes;
* preços;
* moedas;
* disponibilidade;
* vendedores.

---

# 8. Persistência

Após normalização:

Dados são armazenados no PostgreSQL.

Principais entidades:

```text
products

stores

offers

price_snapshots

collector_jobs

opportunities
```

---

# 9. Processamento Analítico

Após armazenamento, o sistema executará análises.

Exemplos:

## Média histórica

```text
Preço médio últimos 90 dias
```

---

## Menor preço

```text
Menor valor encontrado
```

---

## Tendência

```text
Subindo

Estável

Caindo
```

---

## Comparação entre lojas

Exemplo:

| Loja          | Preço |
| ------------- | ----- |
| Amazon        | 219   |
| Mercado Livre | 229   |
| Copag         | 249   |

---

# 10. Geração de Inteligência

Após análise:

O PIE gera:

## POS

Pokémon Opportunity Score.

---

## Recomendação

Exemplo:

```json
{
"score":94,

"action":
"BUY"
}
```

---

## Explicação

Exemplo:

```text
Preço 20% abaixo da média histórica.
```

---

# 11. Atualização do Dashboard

Após processamento:

O frontend consulta:

```text
API

↓

Intelligence Layer

↓

Dashboard
```

---

Informações exibidas:

* melhores oportunidades;
* produtos em queda;
* rankings;
* histórico.

---

# 12. Controle de Qualidade

O pipeline deverá validar:

## Dados incompletos

Exemplo:

Produto sem preço.

---

## Dados inconsistentes

Exemplo:

Preço:

```text
R$0,01
```

---

## Duplicidade

Evitar:

Mesmo produto:

```text
100 vezes
```

na mesma coleta.

---

# 13. Histórico e Auditoria

O sistema deverá registrar:

* quando coletou;
* de onde veio;
* qual valor encontrado;
* quando mudou.

---

Exemplo:

```text
23/07

Amazon

ETB Pokémon

R$249


24/07

Amazon

ETB Pokémon

R$219
```

---

Esse histórico será um dos maiores ativos do PokéRadar.

---

# 14. Escalabilidade

A arquitetura permitirá:

## Mais lojas

Adicionar:

```text
Shopee

Cardmarket

Pokemon Center
```

---

## Mais produtos

Processamento em lote.

---

## Mais usuários

Cache e filas.

---

# 15. Evolução Futura

Possíveis melhorias:

## Data Warehouse

Separação analítica:

```text
Operational Database

↓

Data Warehouse
```

---

## Machine Learning

Modelos para:

* previsão de preço;
* valorização;
* tendência.

---

## Data Lake

Armazenamento massivo de dados históricos.

---

# Considerações Finais

O Data Pipeline é a base de inteligência do PokéRadar.

A qualidade da plataforma dependerá diretamente da qualidade dos dados coletados, tratados e armazenados.

A estratégia definida garante que o sistema possa evoluir de um monitor de preços para uma verdadeira plataforma de inteligência de mercado Pokémon TCG.

---

# Próximo Documento

O próximo documento será:

```text
16-deployment-guide.md
```

Ele definirá:

* preparação de ambiente;
* execução local;
* Docker;
* deploy;
* produção.
