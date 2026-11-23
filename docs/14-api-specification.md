# PokéRadar - API Specification

**Projeto:** PokéRadar
**Documento:** API Specification
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                                 | Alteração                               |
| ------ | ---------- | ------------------------------------- | --------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT (OpenAI) | Criação inicial da especificação da API |

---

# Sumário

1. Objetivo
2. Princípios da API
3. Arquitetura de Comunicação
4. Padrões Gerais
5. Versionamento
6. Autenticação
7. Estrutura de Resposta
8. Códigos HTTP
9. Endpoints
10. Produtos
11. Ofertas
12. Histórico de Preços
13. Oportunidades
14. Collectors
15. PIE
16. Health Check
17. Evolução Futura

---

# 1. Objetivo

Este documento define os contratos da API do PokéRadar.

A API será responsável por disponibilizar dados processados para:

* Dashboard Web;
* integrações futuras;
* aplicativos;
* sistemas externos.

---

# 2. Princípios da API

A API seguirá:

## REST

Comunicação baseada em recursos.

Exemplo:

```text
/products

/offers

/opportunities
```

---

## Padronização

Todas respostas devem seguir o mesmo formato.

---

## Segurança

A API deverá:

* validar entradas;
* controlar acesso;
* registrar erros.

---

# 3. Arquitetura de Comunicação

Fluxo:

```text
Frontend

   ↓

REST API

   ↓

Backend Services

   ↓

Database

   ↓

PIE / Collectors
```

---

# 4. Padrões Gerais

## Base URL

Desenvolvimento:

```text
http://localhost:8000/api/v1
```

Produção:

```text
https://api.pokeradar.com.br/api/v1
```

---

## Formato

Todas as mensagens utilizarão:

```json
application/json
```

---

## Datas

Padrão:

```text
ISO 8601
```

Exemplo:

```text
2026-07-23T15:30:00Z
```

---

## Valores monetários

Sempre enviados como número decimal.

Exemplo:

```json
{
"price":219.90
}
```

---

# 5. Versionamento

A API utilizará versionamento por URL.

Exemplo:

```text
/api/v1/products
```

---

Futuro:

```text
/api/v2/products
```

---

# 6. Autenticação

## MVP

Endpoints públicos para consulta.

---

## Futuro

Utilizar:

```text
Bearer Token JWT
```

Exemplo:

```http
Authorization: Bearer TOKEN
```

---

# 7. Estrutura de Resposta

Todas respostas seguirão:

```json
{
"success": true,
"data": {},
"message": null
}
```

---

Exemplo erro:

```json
{
"success": false,
"data": null,
"message":
"Product not found"
}
```

---

# 8. Códigos HTTP

| Código | Uso             |
| ------ | --------------- |
| 200    | Sucesso         |
| 201    | Criado          |
| 400    | Dados inválidos |
| 401    | Não autenticado |
| 403    | Sem permissão   |
| 404    | Não encontrado  |
| 500    | Erro interno    |

---

# 9. Endpoints

Estrutura inicial:

```text
/api/v1

├── products

├── offers

├── opportunities

├── collectors

├── analytics

└── health
```

---

# 10. Produtos

## Listar produtos

Endpoint:

```http
GET /products
```

---

Resposta:

```json
{
"success":true,
"data":[
 {
  "id":1,
  "name":"Elite Trainer Box",
  "expansion":"Evoluções Prismáticas",
  "category":"ETB"
 }
]
}
```

---

Filtros:

```text
/products?

expansion=

category=

search=
```

---

## Buscar produto por ID

Endpoint:

```http
GET /products/{id}
```

---

Resposta:

```json
{
"id":1,
"name":"ETB Pokémon",
"current_price":219.90
}
```

---

# 11. Ofertas

## Listar ofertas

Endpoint:

```http
GET /offers
```

---

Resposta:

```json
{
"product":
"ETB Pokémon",

"store":
"Amazon",

"price":
219.90,

"url":
"https://..."
}
```

---

Filtros:

```text
/offers?

store=

min_price=

max_price=
```

---

# 12. Histórico de Preços

## Consultar histórico

Endpoint:

```http
GET /products/{id}/history
```

---

Resposta:

```json
{
"product_id":1,

"history":[

{
"date":"2026-07-01",
"price":250
},

{
"date":"2026-07-23",
"price":219.90
}

]
}
```

---

# 13. Oportunidades

Endpoint principal do PIE.

---

## Listar oportunidades

```http
GET /opportunities
```

---

Resposta:

```json
{
"product":
"Box Pokémon",

"score":
92,

"classification":
"BUY",

"reason":[

"Preço abaixo da média",

"Queda de 20%"

]
}
```

---

Filtros:

```text
/opportunities?

score_min=

classification=
```

---

# 14. Collectors

Área administrativa.

---

## Status dos collectors

Endpoint:

```http
GET /collectors/status
```

---

Resposta:

```json
{
"collector":
"amazon",

"status":
"RUNNING",

"last_execution":
"2026-07-23T10:00:00"
}
```

---

# 15. PIE

Endpoints analíticos.

---

## Análise de produto

```http
GET /analytics/products/{id}
```

---

Resposta:

```json
{
"pos":94,

"trend":
"DOWN",

"recommendation":
"BUY"
}
```

---

# 16. Health Check

Endpoint:

```http
GET /health
```

---

Resposta:

```json
{
"status":
"healthy",

"database":
"connected"
}
```

---

# 17. Evolução Futura

Possíveis endpoints:

## Usuários

```text
/users
```

---

## Favoritos

```text
/favorites
```

---

## Alertas

```text
/notifications
```

---

## WhatsApp

```text
/webhooks/whatsapp
```

---

## Coleção pessoal

```text
/collection
```

---

# Considerações Finais

A API do PokéRadar será a ponte entre dados coletados, inteligência gerada e experiência do usuário.

A definição antecipada dos contratos permite crescimento organizado e facilita futuras integrações.

A API deverá permanecer simples, consistente e orientada ao produto.

---

# Próximo Documento

O próximo documento será:

```text
15-data-pipeline-design.md
```

Ele definirá:

* fluxo completo dos dados;
* ingestão;
* processamento;
* armazenamento;
* geração de inteligência;
* atualização do Dashboard.
