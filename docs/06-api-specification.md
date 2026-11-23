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

| Versão | Data       | Autor                        | Alteração                               |
| ------ | ---------- | ---------------------------- | --------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT | Criação inicial da especificação da API |

---

# Sumário

1. Objetivo
2. Princípios da API
3. Arquitetura de Comunicação
4. Padrões da API
5. Versionamento
6. Autenticação
7. Estrutura de Resposta
8. Tratamento de Erros
9. Paginação e Filtros
10. Endpoints MVP
11. Evolução Futura

---

# 1. Objetivo

Este documento define a especificação inicial da API do PokéRadar.

A API será responsável por disponibilizar os dados da plataforma para:

* Dashboard Web;
* Aplicações futuras;
* Integrações externas;
* Sistemas de notificação;
* Aplicativos móveis.

A API será construída seguindo princípios REST e arquitetura orientada ao domínio.

---

# 2. Princípios da API

A API seguirá os seguintes princípios:

## REST First

Os recursos serão representados como entidades de negócio.

Exemplo:

Correto:

```
GET /api/v1/products
```

Evitar:

```
GET /api/v1/getProductsTable
```

---

## Domínio acima do Banco

A API nunca deverá refletir diretamente a estrutura do banco.

Exemplo:

Banco:

```
price_snapshot
```

API:

```
/products/{id}/price-history
```

---

## Compatibilidade

Mudanças incompatíveis deverão criar uma nova versão da API.

Exemplo:

```
/api/v1

/api/v2
```

---

# 3. Arquitetura de Comunicação

Fluxo padrão:

```
Frontend

     ↓

API Gateway / FastAPI

     ↓

Controllers

     ↓

Services

     ↓

Repositories

     ↓

Database
```

---

Responsabilidades:

## Controller

Responsável por:

* Receber requisição;
* Validar entrada;
* Retornar resposta.

---

## Service

Responsável por:

* Regras de negócio;
* Cálculos;
* Processamentos.

---

## Repository

Responsável por:

* Comunicação com banco;
* Consultas;
* Persistência.

---

# 4. Padrões da API

## Protocolo

Inicialmente:

```
HTTP/HTTPS
```

---

## Formato

Entrada e saída:

```
JSON
```

---

## Base URL

Desenvolvimento:

```
http://localhost:8000/api/v1
```

Produção:

```
https://api.pokeradar.com.br/api/v1
```

---

# 5. Versionamento

Todas as rotas possuirão versão.

Formato:

```
/api/v1/{resource}
```

Exemplo:

```
GET /api/v1/products
```

---

# 6. Autenticação

## MVP

A primeira versão será pública para consulta.

Não haverá autenticação obrigatória.

---

## Futuro

Possível implementação:

* JWT;
* OAuth;
* Controle de usuários;
* Planos premium.

---

# 7. Estrutura de Resposta

Todas as respostas seguirão um padrão.

## Sucesso

Exemplo:

```json
{
    "success": true,
    "data": {},
    "message": null
}
```

---

## Lista

Exemplo:

```json
{
    "success": true,
    "data": [],
    "pagination": {
        "page": 1,
        "limit": 20,
        "total": 100
    }
}
```

---

# 8. Tratamento de Erros

Formato padrão:

```json
{
    "success": false,
    "error": {
        "code": "PRODUCT_NOT_FOUND",
        "message": "Produto não encontrado"
    }
}
```

---

Principais códigos:

| Código | Descrição               |
| ------ | ----------------------- |
| 400    | Requisição inválida     |
| 401    | Não autorizado          |
| 403    | Acesso proibido         |
| 404    | Registro não encontrado |
| 500    | Erro interno            |

---

# 9. Paginação e Filtros

Todas as listagens deverão suportar paginação.

Exemplo:

```
GET /api/v1/products?page=1&limit=20
```

---

Filtros deverão utilizar parâmetros.

Exemplo:

```
GET /api/v1/offers?store=amazon
```

---

Ordenação:

```
GET /api/v1/products?sort=price_desc
```

---

# 10. Endpoints MVP

---

# Products

## Listar produtos

```
GET /api/v1/products
```

Retorna produtos monitorados.

---

## Detalhar produto

```
GET /api/v1/products/{product_id}
```

Retorna informações completas.

---

## Histórico de preço

```
GET /api/v1/products/{product_id}/price-history
```

Retorna evolução histórica.

---

# Stores

## Listar lojas

```
GET /api/v1/stores
```

Retorna lojas monitoradas.

---

# Offers

## Listar ofertas

```
GET /api/v1/offers
```

Retorna ofertas disponíveis.

Filtros:

* loja;
* produto;
* menor preço;
* disponibilidade.

---

## Detalhar oferta

```
GET /api/v1/offers/{offer_id}
```

---

# Opportunities

## Listar oportunidades

```
GET /api/v1/opportunities
```

Retorna produtos classificados pelo PIE.

Exemplo:

Resposta:

```json
{
    "product": "ETB Evoluções Prismáticas",
    "pos_score": 92,
    "recommendation": "BUY"
}
```

---

# Dashboard

## Resumo geral

```
GET /api/v1/dashboard/summary
```

Retorna:

* quantidade de produtos;
* promoções encontradas;
* melhores oportunidades;
* variação de preços.

---

# Health Check

Endpoint obrigatório:

```
GET /api/v1/health
```

Resposta:

```json
{
    "status": "healthy"
}
```

Utilizado para:

* Docker;
* Monitoramento;
* Deploy.

---

# 11. Evolução Futura

A API poderá futuramente suportar:

## Usuários

```
/users
```

---

## Favoritos

```
/favorites
```

---

## Alertas

```
/alerts
```

---

## Integrações

```
/webhooks
```

---

## API Pública

Possibilidade futura:

```
/api/public/v1
```

---

# Considerações Finais

A API do PokéRadar será construída como uma camada independente do banco de dados, permitindo evolução da plataforma sem grandes impactos.

O objetivo principal é fornecer informações confiáveis de mercado de Pokémon TCG, transformando dados coletados em inteligência para tomada de decisão.

---

# Próximo Documento

O próximo documento será:

```
07-frontend-specification.md
```

Ele definirá:

* arquitetura do dashboard;
* tecnologias;
* telas;
* componentes;
* fluxo de usuário;
* experiência visual.
