# PokéRadar - Database Implementation Plan

**Projeto:** PokéRadar
**Documento:** Database Implementation Plan
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Status:** Em desenvolvimento

---

# Histórico de Alterações

| Versão | Data       | Autor                        | Alteração                               |
| ------ | ---------- | ---------------------------- | --------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT | Plano inicial de implementação do banco |

---

# Sumário

1. Objetivo
2. Tecnologia
3. Estratégia de Banco
4. Modelo Inicial
5. Entidades Principais
6. Tabelas MVP
7. Relacionamentos
8. Índices
9. Migrations
10. Seeds
11. Dados Históricos
12. Evolução Futura

---

# 1. Objetivo

Este documento define o plano de implementação do banco de dados do PokéRadar.

O objetivo é criar uma estrutura capaz de armazenar:

* produtos Pokémon TCG;
* lojas;
* ofertas;
* histórico de preços;
* dados coletados;
* inteligência gerada.

---

# 2. Tecnologia

Banco escolhido:

```text
PostgreSQL
```

Motivos:

* open source;
* robusto;
* excelente suporte;
* compatível com aplicações analíticas;
* preparado para crescimento.

---

ORM Backend:

```text
SQLAlchemy
```

Migrações:

```text
Alembic
```

---

# 3. Estratégia de Banco

O banco será dividido conceitualmente em:

```text
Operational Database

↓

Analytics Layer
```

---

## Operational Database

Responsável pelos dados da aplicação.

Exemplo:

* produtos;
* lojas;
* ofertas.

---

## Analytics Layer

Responsável por:

* indicadores;
* históricos;
* inteligência.

---

# 4. Modelo Inicial

Modelo simplificado:

```text
                 stores

                    |

                    |

products ---- offers ---- price_snapshots

                    |

                    |

              opportunities

```

---

# 5. Entidades Principais

Primeira versão:

```text
Store

Product

Offer

PriceSnapshot

CollectorLog

Opportunity
```

---

# 6. Tabelas MVP

---

# 6.1 stores

Representa lojas monitoradas.

Exemplos:

* Amazon;
* Mercado Livre;
* Ri Happy;
* Copag Store;
* Liga Pokémon.

---

Estrutura:

```sql
stores
```

Campos:

| Campo      | Tipo      | Descrição             |
| ---------- | --------- | --------------------- |
| id         | UUID      | Identificador         |
| name       | VARCHAR   | Nome da loja          |
| slug       | VARCHAR   | Identificador interno |
| url        | TEXT      | Site                  |
| active     | BOOLEAN   | Ativa                 |
| created_at | TIMESTAMP | Criação               |

---

# 6.2 products

Representa produtos Pokémon TCG.

Exemplos:

* ETB;
* Booster Box;
* Mini Box;
* Box promocional.

---

Estrutura:

```sql
products
```

Campos:

| Campo      | Tipo      |
| ---------- | --------- |
| id         | UUID      |
| name       | VARCHAR   |
| category   | VARCHAR   |
| expansion  | VARCHAR   |
| language   | VARCHAR   |
| created_at | TIMESTAMP |

---

Exemplo:

```json
{
"name":
"Elite Trainer Box Evoluções Prismáticas",

"category":
"ETB"
}
```

---

# 6.3 offers

Representa uma oferta encontrada em uma loja.

---

Estrutura:

```sql
offers
```

Campos:

| Campo        | Tipo      |
| ------------ | --------- |
| id           | UUID      |
| product_id   | UUID      |
| store_id     | UUID      |
| seller       | VARCHAR   |
| price        | DECIMAL   |
| availability | BOOLEAN   |
| url          | TEXT      |
| created_at   | TIMESTAMP |

---

Relacionamentos:

```text
Product

1:N

Offers


Store

1:N

Offers
```

---

# 6.4 price_snapshots

Tabela estratégica.

Armazena a evolução de preços.

---

Estrutura:

```sql
price_snapshots
```

Campos:

| Campo        | Tipo      |
| ------------ | --------- |
| id           | UUID      |
| offer_id     | UUID      |
| price        | DECIMAL   |
| collected_at | TIMESTAMP |

---

Exemplo:

```text
Produto:

ETB Pokémon


01/07

R$299


15/07

R$249


23/07

R$219
```

---

# 6.5 collector_logs

Controle dos coletores.

---

Estrutura:

```sql
collector_logs
```

Campos:

| Campo          | Tipo      |
| -------------- | --------- |
| id             | UUID      |
| collector_name | VARCHAR   |
| status         | VARCHAR   |
| records_found  | INTEGER   |
| error_message  | TEXT      |
| executed_at    | TIMESTAMP |

---

Exemplo:

```text
Amazon Collector

SUCCESS

120 produtos encontrados
```

---

# 6.6 opportunities

Resultado do PIE.

---

Estrutura:

```sql
opportunities
```

Campos:

| Campo          | Tipo      |
| -------------- | --------- |
| id             | UUID      |
| product_id     | UUID      |
| score          | INTEGER   |
| classification | VARCHAR   |
| reason         | JSONB     |
| created_at     | TIMESTAMP |

---

Exemplo:

```json
{
"score":92,

"classification":"BUY",

"reason":[
"Preço abaixo da média"
]
}
```

---

# 7. Relacionamentos

Modelo:

```text id="6q1w5j"

STORE

 |
 |
 N

OFFER

 |
 |
 N

PRICE_SNAPSHOT


PRODUCT

 |
 |
 N

OFFER


PRODUCT

 |
 |
 N

OPPORTUNITY
```

---

# 8. Índices

Índices importantes:

## Produtos

```sql
products(name)
```

Motivo:

Busca rápida.

---

## Ofertas

```sql
offers(product_id)

offers(store_id)
```

---

## Histórico

```sql
price_snapshots(collected_at)
```

---

# 9. Migrations

Todas alterações deverão ser versionadas.

Exemplo:

```text
database/

migrations/

001_create_stores.sql

002_create_products.sql

003_create_offers.sql
```

---

Com Alembic:

```bash
alembic revision --autogenerate
```

---

Aplicar:

```bash
alembic upgrade head
```

---

# 10. Seeds

Dados iniciais:

Primeiras lojas:

```text
Amazon

Mercado Livre

Ri Happy

Copag Store

Liga Pokémon
```

---

Exemplo:

```sql
INSERT INTO stores
(name)
VALUES
('Amazon');
```

---

# 11. Dados Históricos

O banco deverá preservar:

* preço encontrado;
* data;
* loja;
* produto.

---

Motivo:

Permitir:

* gráficos;
* tendências;
* previsões.

---

# 12. Evolução Futura

Possíveis novas tabelas:

---

## users

Usuários da plataforma.

---

## favorites

Produtos favoritos.

---

## alerts

Alertas personalizados.

---

## collections

Coleção pessoal.

---

## market_reports

Relatórios de mercado.

---

## cards

Cartas individuais.

---

Futuro:

```text
Card

↓

Price History

↓

Market Analysis
```

---

# Considerações Finais

A estrutura inicial do banco foi criada pensando além do MVP.

O objetivo não é apenas armazenar preços, mas criar uma base histórica capaz de gerar inteligência de mercado Pokémon TCG.

A qualidade dos dados armazenados será um dos maiores diferenciais competitivos do PokéRadar.

---

# Próximo Documento

Próximo passo:

```text
22-backend-implementation-plan.md
```

Definirá:

* criação do FastAPI;
* estrutura inicial;
* primeiros endpoints;
* conexão com banco;
* padrões de código.
