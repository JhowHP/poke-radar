# PokéRadar - Frontend Specification

**Projeto:** PokéRadar
**Documento:** Frontend Specification
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                                 | Alteração                                    |
| ------ | ---------- | ------------------------------------- | -------------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT (OpenAI) | Criação inicial da especificação do frontend |

---

# Sumário

1. Objetivo
2. Visão do Produto
3. Princípios de UX
4. Tecnologia
5. Arquitetura Frontend
6. Estrutura da Aplicação
7. Telas MVP
8. Componentes
9. Estado da Aplicação
10. Integração com API
11. Responsividade
12. Evolução Futura

---

# 1. Objetivo

Este documento define a especificação inicial do frontend do PokéRadar.

O frontend será responsável por apresentar informações de mercado de Pokémon TCG de forma clara, visual e orientada à tomada de decisão.

O objetivo principal não é apenas mostrar preços, mas transformar dados coletados em inteligência.

---

# 2. Visão do Produto

O Dashboard será o centro de operação do PokéRadar.

Ele permitirá que usuários:

* acompanhem preços;
* encontrem oportunidades;
* comparem lojas;
* analisem histórico;
* acompanhem tendências.

---

Fluxo principal:

```
Usuário

↓

Dashboard

↓

Análise de Mercado

↓

Decisão de Compra
```

---

# 3. Princípios de UX

O frontend seguirá os seguintes princípios:

---

## Informação antes de complexidade

O usuário deve encontrar respostas rapidamente.

Exemplo:

Pergunta:

"Vale comprar essa Box?"

Resposta:

* preço atual;
* preço médio;
* menor preço histórico;
* tendência;
* recomendação.

---

## Visualização de dados

Informações importantes deverão possuir:

* gráficos;
* indicadores;
* comparações;
* rankings.

---

## Simplicidade

O usuário não precisa entender o funcionamento interno do sistema.

O PIE deverá traduzir dados complexos em informações simples.

---

# 4. Tecnologia

Stack inicial proposta:

## Framework

```
React + TypeScript
```

---

## Build

```
Vite
```

---

## UI

Proposta:

```
Chakra UI
```

Motivos:

* produtividade;
* componentes prontos;
* acessibilidade;
* boa integração com React.

---

## Gerenciamento de Estado

Inicialmente:

```
React Query
```

Responsável por:

* cache;
* chamadas API;
* sincronização.

---

## Rotas

```
React Router
```

---

## Gráficos

Possíveis opções:

* Recharts
* ECharts

---

# 5. Arquitetura Frontend

Estrutura proposta:

```
src/

├── app/

├── components/

├── pages/

├── features/

├── services/

├── hooks/

├── types/

├── utils/

├── assets/

└── styles/
```

---

# Responsabilidades

## Pages

Representam telas completas.

Exemplo:

```
DashboardPage
ProductsPage
OffersPage
```

---

## Components

Componentes reutilizáveis.

Exemplo:

```
PriceCard

Chart

Table

Badge
```

---

## Features

Organização por domínio.

Exemplo:

```
features/

├── products

├── offers

├── opportunities

└── dashboard
```

---

## Services

Comunicação com API.

Exemplo:

```
productService.ts

offerService.ts
```

---

# 6. Estrutura da Aplicação

Fluxo:

```
User Interface

↓

Components

↓

Hooks

↓

Services

↓

API

↓

Backend
```

---

# 7. Telas MVP

## Dashboard Principal

Objetivo:

Mostrar uma visão geral do mercado.

---

Indicadores:

* produtos monitorados;
* promoções encontradas;
* melhores oportunidades;
* últimas quedas de preço.

---

Exemplo:

```
--------------------------------

PokéRadar

Mercado Atual

[125 Produtos]

[18 Promoções]

[7 Grandes Oportunidades]

--------------------------------

Melhores oportunidades

1 - ETB X
POS 95

2 - Box Y
POS 90

--------------------------------
```

---

# Tela de Produtos

Objetivo:

Consultar produtos monitorados.

Informações:

* nome;
* expansão;
* categoria;
* preço atual;
* menor preço;
* tendência.

---

Filtros:

* expansão;
* categoria;
* loja;
* preço.

---

# Tela de Produto

Página detalhada.

Informações:

## Informações gerais

* nome;
* expansão;
* lançamento.

---

## Preço atual

* lojas;
* menor preço;
* média.

---

## Histórico

Gráfico:

```
Preço

300 |
250 |
200 |
150 |
100 |

----------------
     Tempo
```

---

## Oportunidade

Mostrar:

* POS;
* recomendação;
* justificativa.

---

# Tela de Ofertas

Objetivo:

Comparar lojas.

Exemplo:

| Loja          | Preço |
| ------------- | ----- |
| Amazon        | R$220 |
| Mercado Livre | R$230 |
| Copag         | R$250 |

---

# Tela de Oportunidades

Página dedicada ao PIE.

Exemplo:

```
🔥 Oportunidades de hoje

ETB Evoluções Prismáticas

Preço atual:
R$219

Média:
R$280

Desconto:
21%

POS:
94

Recomendação:
COMPRA
```

---

# 8. Componentes Principais

Componentes previstos:

## Cards

* PriceCard
* OpportunityCard
* ProductCard

---

## Gráficos

* PriceHistoryChart
* PriceComparisonChart
* TrendChart

---

## Tabelas

* ProductTable
* OfferTable

---

## Elementos

* Badge
* Button
* Modal
* Filter
* Search

---

# 9. Estado da Aplicação

Separação:

## Estado local

Exemplo:

* filtros;
* modais;
* menus.

---

## Estado servidor

Gerenciado por:

```
React Query
```

Responsável por:

* produtos;
* ofertas;
* histórico;
* oportunidades.

---

# 10. Integração com API

Comunicação:

```
Frontend

↓

HTTP Client

↓

API REST

```

---

Formato esperado:

```json
{
 "success": true,
 "data": {}
}
```

---

# 11. Responsividade

O Dashboard deverá funcionar em:

## Desktop

Principal experiência.

---

## Tablet

Visualização intermediária.

---

## Mobile

Consulta rápida.

Principalmente para:

* acompanhar oportunidades;
* verificar preços.

---

# 12. Evolução Futura

Possíveis funcionalidades:

## Usuários

* login;
* perfil;
* preferências.

---

## Favoritos

Usuário poderá acompanhar produtos específicos.

---

## Alertas

Integração:

* WhatsApp;
* Telegram;
* Email.

---

## Área de Colecionador

Recursos:

* coleção pessoal;
* valor estimado;
* evolução.

---

## Área Investidor

Recursos:

* valorização;
* tendências;
* histórico.

---

# Considerações Finais

O frontend do PokéRadar deverá funcionar como uma central de inteligência de mercado.

Seu objetivo não é apenas apresentar dados, mas transformar informações complexas em decisões simples.

O Dashboard será o principal produto visual da plataforma.

---

# Próximo Documento

O próximo documento será:

```
08-collectors-design.md
```

Ele definirá:

* arquitetura dos coletores;
* integração com lojas;
* normalização dos dados;
* estratégia de captura;
* tratamento de erros.
