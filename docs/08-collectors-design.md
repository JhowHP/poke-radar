# PokéRadar - Collectors Design

**Projeto:** PokéRadar
**Documento:** Collectors Design
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                                 | Alteração                                    |
| ------ | ---------- | ------------------------------------- | -------------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT (OpenAI) | Criação inicial da arquitetura dos coletores |

---

# Sumário

1. Objetivo
2. Responsabilidade dos Collectors
3. Arquitetura Geral
4. Fluxo de Coleta
5. Lojas Monitoradas
6. Estrutura de um Collector
7. Normalização de Dados
8. Tratamento de Erros
9. Agendamento
10. Histórico de Execuções
11. Escalabilidade
12. Evolução Futura

---

# 1. Objetivo

Este documento define a arquitetura dos coletores responsáveis pela captura de informações de produtos Pokémon TCG em diferentes plataformas de venda.

Os collectors serão responsáveis por:

* buscar produtos;
* capturar preços;
* identificar disponibilidade;
* capturar informações comerciais;
* transformar dados externos em um formato padrão.

---

# 2. Responsabilidade dos Collectors

Os collectors possuem uma única responsabilidade:

> Capturar dados externos e convertê-los para o modelo interno do PokéRadar.

---

## O Collector faz:

✅ Buscar informações na loja.

✅ Extrair dados relevantes.

✅ Normalizar formato.

✅ Registrar execução.

✅ Enviar dados para processamento.

---

## O Collector não faz:

❌ Definir promoção.

❌ Calcular POS.

❌ Decidir compra.

❌ Alterar regras de negócio.

---

Fluxo:

```text
Loja

↓

Collector

↓

Dados Normalizados

↓

Database

↓

PIE
```

---

# 3. Arquitetura Geral

Estrutura:

```text
                 Collector Manager

                       |

        --------------------------------

        |              |              |

    Amazon        Mercado Livre    Ri Happy

    Collector     Collector        Collector


                       |

                       ↓

              Normalization Layer

                       |

                       ↓

                 PostgreSQL
```

---

# 4. Fluxo de Coleta

Cada execução seguirá:

```text
1 - Iniciar Job

↓

2 - Consultar Loja

↓

3 - Capturar Produtos

↓

4 - Extrair Informações

↓

5 - Normalizar Dados

↓

6 - Validar Dados

↓

7 - Persistir Snapshot

↓

8 - Registrar Resultado
```

---

# 5. Lojas Monitoradas

## MVP Inicial

Primeiras integrações:

| Loja          | Tipo               |
| ------------- | ------------------ |
| Amazon        | Marketplace        |
| Mercado Livre | Marketplace        |
| Ri Happy      | Varejo             |
| Copag Store   | Loja oficial       |
| Liga Pokémon  | Loja especializada |

---

Cada loja possuirá seu próprio collector.

Exemplo:

```text
collectors/

├── amazon/

├── mercado_livre/

├── ri_happy/

├── copag/

└── liga_pokemon/
```

---

# 6. Estrutura de um Collector

Todos os collectors deverão seguir o mesmo padrão.

Exemplo:

```text
amazon/

├── collector.py

├── scraper.py

├── parser.py

├── mapper.py

├── validator.py

└── tests/
```

---

## Collector

Responsável por controlar o processo.

---

## Scraper

Responsável por buscar dados.

---

## Parser

Responsável por interpretar respostas.

---

## Mapper

Responsável por transformar em modelo PokéRadar.

---

## Validator

Responsável por validar informações obrigatórias.

---

# 7. Normalização de Dados

Um dos maiores desafios será transformar diferentes formatos em um padrão único.

Exemplo:

Amazon:

```json
{
"name":
"Pokemon Elite Trainer Box"
}
```

Mercado Livre:

```json
{
"title":
"ETB Pokemon"
}
```

Resultado interno:

```json
{
"product_name":
"Elite Trainer Box Pokemon"
}
```

---

Todos os collectors deverão gerar um objeto padrão:

```json
{
"store": "amazon",
"name": "Produto",
"price": 219.90,
"stock": true,
"url": "https://...",
"seller": "Amazon",
"captured_at": "2026-07-23T10:00:00"
}
```

---

# 8. Tratamento de Erros

Os collectors devem tratar:

## Falha de conexão

Exemplo:

* timeout;
* indisponibilidade da loja.

---

## Mudança de página

Exemplo:

* HTML alterado;
* API alterada.

---

## Dados inválidos

Exemplo:

Preço:

```text
R$ --
```

Produto:

```text
sem nome
```

---

Todos os erros devem ser registrados no CollectorJob.

---

# 9. Agendamento

Os collectors serão executados automaticamente.

Possíveis estratégias:

## MVP

Scheduler interno.

Exemplo:

```text
Amazon

Executar:

a cada 6 horas
```

---

## Futuro

Uso de:

* Celery;
* RabbitMQ;
* Kubernetes CronJob.

---

# 10. Histórico de Execuções

Toda execução deverá gerar um CollectorJob.

Informações:

* início;
* término;
* status;
* quantidade processada;
* erros.

Exemplo:

```json
{
"collector":
"amazon",

"status":
"SUCCESS",

"processed":
120
}
```

---

# 11. Escalabilidade

A arquitetura deverá permitir:

* adicionar novas lojas;
* executar collectors paralelos;
* reprocessar dados;
* monitorar falhas.

---

Novo collector:

```text
Pokemon Center

↓

pokemon_center_collector
```

Sem alteração nos collectors existentes.

---

# 12. Evolução Futura

Possíveis melhorias:

## Inteligência Artificial

Uso de IA para:

* identificar produtos equivalentes;
* melhorar normalização;
* detectar mudanças de página.

---

## APIs Oficiais

Quando disponíveis:

* substituir scraping por APIs oficiais.

---

## Machine Learning

Modelos para:

* prever quedas de preço;
* identificar tendências;
* sugerir compra.

---

# Considerações Finais

Os Collectors representam a camada de aquisição de dados do PokéRadar.

Seu objetivo é fornecer informações confiáveis e padronizadas para que as camadas superiores possam gerar inteligência.

A separação entre coleta e análise garante que novas lojas possam ser adicionadas sem impacto nas regras de negócio.

---

# Próximo Documento

O próximo documento será:

```text
09-pie-design.md
```

Ele definirá o:

**PokéRadar Intelligence Engine (PIE)**

Responsável por transformar dados coletados em inteligência de mercado.

Serão definidos:

* POS (Pokémon Opportunity Score);
* regras de promoção;
* análise histórica;
* indicadores;
* recomendações.
