# PokéRadar - Development Guidelines

**Projeto:** PokéRadar
**Documento:** Development Guidelines
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                                 | Alteração                                         |
| ------ | ---------- | ------------------------------------- | ------------------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT (OpenAI) | Criação inicial das diretrizes de desenvolvimento |

---

# Sumário

1. Objetivo
2. Princípios de Desenvolvimento
3. Organização do Código
4. Padrões de Nomenclatura
5. Backend Guidelines
6. Frontend Guidelines
7. Banco de Dados Guidelines
8. Testes
9. Documentação de Código
10. Git Workflow
11. Commits
12. Code Review
13. Segurança
14. Qualidade de Código

---

# 1. Objetivo

Este documento define os padrões técnicos utilizados no desenvolvimento do PokéRadar.

O objetivo é garantir:

* consistência;
* legibilidade;
* facilidade de manutenção;
* qualidade profissional;
* evolução sustentável.

---

# 2. Princípios de Desenvolvimento

## Código simples vence código complexo

Sempre priorizar:

* clareza;
* manutenção;
* entendimento.

Evitar soluções excessivamente sofisticadas sem necessidade.

---

## Separação de responsabilidades

Cada componente deve possuir uma responsabilidade clara.

Exemplo:

Errado:

```text
Controller

+
Regra de negócio

+
Consulta SQL
```

Correto:

```text
Controller

↓

Service

↓

Repository
```

---

## Documentação como parte do código

Toda decisão importante deve ser documentada.

Código sem contexto gera problemas futuros.

---

# 3. Organização do Código

O projeto seguirá uma organização por domínio.

Exemplo Backend:

```text
backend/

app/

├── api/

├── core/

├── models/

├── schemas/

├── services/

├── repositories/

├── collectors/

└── tests/
```

---

Frontend:

```text
frontend/

src/

├── components/

├── features/

├── pages/

├── services/

├── hooks/

└── utils/
```

---

# 4. Padrões de Nomenclatura

## Python

Classes:

```python
ProductService
PriceAnalyzer
AmazonCollector
```

---

Funções:

```python
get_product()

calculate_score()

save_snapshot()
```

---

Variáveis:

```python
current_price

product_id

collector_status
```

---

## TypeScript

Componentes:

```text
ProductCard.tsx

DashboardChart.tsx
```

---

Hooks:

```text
useProducts.ts

useOffers.ts
```

---

Services:

```text
productService.ts
```

---

# 5. Backend Guidelines

Tecnologias:

* Python;
* FastAPI;
* SQLAlchemy;
* Alembic;
* Pydantic.

---

## Camadas

Obrigatório:

```text
Router

↓

Service

↓

Repository

↓

Database
```

---

## Models

Responsabilidade:

Representar entidades do banco.

Exemplo:

```python
class Product:
    name
    category
```

---

## Schemas

Responsabilidade:

Entrada e saída da API.

Exemplo:

```python
ProductResponse
```

---

## Services

Responsabilidade:

Regras de negócio.

Exemplo:

```python
calculate_opportunity_score()
```

---

# 6. Frontend Guidelines

Tecnologias:

* React;
* TypeScript;
* Chakra UI.

---

## Componentes

Devem ser:

* pequenos;
* reutilizáveis;
* independentes.

---

Evitar:

Componentes gigantes:

```text
Dashboard.tsx

2000 linhas
```

---

Preferir:

```text
Dashboard.tsx

↓

DashboardCard

↓

OpportunityTable
```

---

# 7. Banco de Dados Guidelines

Regras:

* Toda tabela deve possuir chave primária.
* Toda alteração deve utilizar migration.
* Nunca alterar produção manualmente.

---

## Nomes

Tabelas:

snake_case:

```text
price_snapshots
```

---

Campos:

snake_case:

```text
created_at

product_id
```

---

# 8. Testes

O projeto utilizará testes desde o início.

---

## Backend

Framework:

```text
pytest
```

---

Tipos:

## Unitários

Testar funções isoladas.

Exemplo:

```text
POS calculation
```

---

## Integração

Testar:

* API;
* banco;
* serviços.

---

## Frontend

Testar:

* componentes;
* hooks;
* fluxos críticos.

---

# 9. Documentação de Código

Funções importantes devem possuir documentação.

Exemplo:

```python
def calculate_pos(price_history):
    """
    Calculates the Pokémon Opportunity Score
    based on historical prices.
    """
```

---

Não documentar código óbvio.

Evitar:

```python
# soma dois números
total = a + b
```

---

# 10. Git Workflow

Fluxo:

```text
feature

↓

develop

↓

main
```

---

Branches:

Exemplos:

```text
feature/product-api

feature/amazon-collector

bugfix/price-calculation
```

---

# 11. Commits

Commits deverão seguir padrão:

```text
tipo: descrição
```

---

Tipos:

| Tipo     | Uso                 |
| -------- | ------------------- |
| feat     | Nova funcionalidade |
| fix      | Correção            |
| docs     | Documentação        |
| refactor | Refatoração         |
| test     | Testes              |
| chore    | Configuração        |

---

Exemplos:

```text
feat: create product endpoint

docs: update database design

fix: correct price calculation
```

---

# 12. Code Review

Toda alteração importante deverá ser revisada.

Avaliar:

* funcionamento;
* legibilidade;
* segurança;
* impacto.

---

Perguntas:

* Esse código será fácil de manter?
* Existe uma solução mais simples?
* Está documentado?

---

# 13. Segurança

Diretrizes:

Nunca armazenar:

* senhas;
* tokens;
* chaves privadas.

---

Sempre utilizar:

* variáveis de ambiente;
* validação de entrada;
* tratamento de erros.

---

# 14. Qualidade de Código

Ferramentas previstas:

## Backend

* Ruff;
* Black;
* Pytest.

---

## Frontend

* ESLint;
* Prettier;
* TypeScript Check.

---

## Controle

Pull Requests deverão passar por validações automáticas.

---

# Considerações Finais

As diretrizes de desenvolvimento do PokéRadar têm como objetivo garantir que o projeto permaneça sustentável durante seu crescimento.

A qualidade do código será tratada como uma característica do produto, não apenas como uma preocupação técnica.

---

# Próximo Documento

O próximo documento será:

```text
12-security-guidelines.md
```

Ele definirá:

* autenticação;
* proteção de dados;
* segurança da API;
* controle de acesso;
* boas práticas de produção.
