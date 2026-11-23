# PokéRadar - Initial Project Structure

**Projeto:** PokéRadar
**Documento:** Initial Project Structure
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Status:** Em desenvolvimento

---

# Histórico de Alterações

| Versão | Data       | Autor                        | Alteração                               |
| ------ | ---------- | ---------------------------- | --------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT | Criação da estrutura inicial do projeto |

---

# Sumário

1. Objetivo
2. Arquitetura Inicial
3. Estrutura do Repositório
4. Backend
5. Frontend
6. Database
7. Docker
8. Scripts
9. Configurações
10. Primeiro Ciclo de Desenvolvimento

---

# 1. Objetivo

Este documento define a estrutura inicial do código-fonte do PokéRadar.

O objetivo é criar uma base organizada, escalável e preparada para evolução futura.

---

# 2. Arquitetura Inicial

O MVP seguirá uma arquitetura baseada em:

```text
Frontend
React + TypeScript

        ↓

Backend
FastAPI + Python

        ↓

Database
PostgreSQL

        ↓

Collectors + PIE
```

---

# 3. Estrutura do Repositório

Estrutura inicial:

```text
pokeradar/

│
├── backend/
│
├── frontend/
│
├── database/
│
├── docker/
│
├── scripts/
│
├── docs/
│
├── .env.example
│
├── docker-compose.yml
│
├── README.md
│
└── .gitignore
```

---

# 4. Backend

Responsável por:

* API;
* regras de negócio;
* processamento;
* integração com banco.

Estrutura:

```text
backend/

app/

├── main.py

├── api/

├── core/

├── models/

├── schemas/

├── services/

├── repositories/

├── collectors/

├── pie/

└── tests/
```

---

## main.py

Ponto inicial da aplicação.

Responsável por:

* iniciar FastAPI;
* registrar rotas;
* configurar aplicação.

---

## api/

Camada HTTP.

Exemplo:

```text
products.py

offers.py

opportunities.py
```

Responsável por:

* endpoints;
* validações de entrada.

---

## core/

Configurações globais.

Exemplo:

```text
database.py

security.py

settings.py
```

---

## models/

Representação das entidades do banco.

Exemplo:

```text
product.py

offer.py

store.py
```

---

## schemas/

Contratos de entrada e saída.

Exemplo:

```text
product_schema.py
```

---

## services/

Regras de negócio.

Exemplo:

```text
price_service.py

opportunity_service.py
```

---

## repositories/

Comunicação com banco.

Exemplo:

```text
product_repository.py
```

---

## collectors/

Coletores externos.

Estrutura futura:

```text
collectors/

├── amazon/

├── mercado_livre/

└── ri_happy/
```

---

## pie/

Motor de inteligência.

Estrutura futura:

```text
pie/

├── scoring.py

├── rules.py

└── analysis.py
```

---

# 5. Frontend

Responsável pelo Dashboard.

Tecnologias:

* React;
* TypeScript;
* Vite;
* Chakra UI.

Estrutura:

```text
frontend/

src/

├── components/

├── pages/

├── features/

├── services/

├── hooks/

├── types/

└── utils/
```

---

# components/

Componentes reutilizáveis.

Exemplo:

```text
PriceCard.tsx

OpportunityCard.tsx
```

---

# pages/

Páginas completas.

Exemplo:

```text
Dashboard.tsx

ProductDetails.tsx
```

---

# features/

Funcionalidades agrupadas.

Exemplo:

```text
products/

offers/

analytics/
```

---

# services/

Comunicação com API.

Exemplo:

```text
api.ts

productService.ts
```

---

# 6. Database

Responsável pela persistência.

Estrutura:

```text
database/

├── migrations/

├── seeds/

└── scripts/
```

---

## migrations

Alterações estruturais.

Exemplo:

```text
001_create_products.sql
```

---

## seeds

Dados iniciais.

Exemplo:

```text
initial_stores.sql
```

---

Primeiras entidades:

```text
stores

products

offers

price_snapshots

collector_logs
```

---

# 7. Docker

Responsável pelo ambiente.

Estrutura:

```text
docker/

├── backend/

├── frontend/

└── database/
```

---

Serviços iniciais:

```yaml
backend

frontend

postgres
```

---

Futuro:

```yaml
redis

worker

scheduler
```

---

# 8. Scripts

Automação.

Estrutura:

```text
scripts/

├── dev/

└── deploy/
```

---

Exemplos:

```text
start-dev.sh

backup-db.sh
```

---

# 9. Configurações

Arquivos principais:

---

## .env.example

Modelo de variáveis.

Exemplo:

```env
DATABASE_HOST=
DATABASE_USER=
DATABASE_PASSWORD=
API_URL=
```

---

## .gitignore

Nunca versionar:

```text
.env

venv/

node_modules/

__pycache__/
```

---

# 10. Primeiro Ciclo de Desenvolvimento

A implementação seguirá:

---

## Etapa 1

Criar estrutura:

```text
backend/

frontend/

database/
```

---

## Etapa 2

Configurar ambiente:

* Docker;
* PostgreSQL;
* FastAPI;
* React.

---

## Etapa 3

Criar primeiro endpoint:

```http
GET /health
```

---

## Etapa 4

Criar primeira entidade:

```text
Store
```

---

## Etapa 5

Criar primeiro Collector:

```text
Amazon Collector
```

---

# Primeiro Commit Planejado

Após criação da estrutura:

```bash
git add .

git commit -m "chore: initialize Pokeradar project structure"
```

---

# Considerações Finais

A estrutura inicial do PokéRadar foi definida pensando em crescimento.

O projeto começa simples, porém preparado para:

* novos coletores;
* novos usuários;
* novas análises;
* inteligência avançada;
* expansão comercial.

A organização inicial será a base para transformar o PokéRadar em uma plataforma profissional de inteligência Pokémon TCG.

---

# Próximo Documento

Próximo passo:

```text
20-environment-setup.md
```

Definirá:

* instalação das ferramentas;
* configuração local;
* Docker;
* primeiro ambiente de desenvolvimento.
