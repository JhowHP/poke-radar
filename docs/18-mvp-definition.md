# PokéRadar - MVP Definition

**Projeto:** PokéRadar
**Documento:** MVP Definition
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)

---

# Histórico de Alterações

| Versão | Data       | Autor                        | Alteração                |
| ------ | ---------- | ---------------------------- | ------------------------ |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT | Definição inicial do MVP |

---

# 1. Objetivo

Definir o menor produto funcional capaz de validar o valor do PokéRadar.

---

# 2. Objetivo do MVP

Responder:

> "Consigo encontrar boas oportunidades de compra de Pokémon TCG usando dados automatizados?"

---

# 3. Escopo Incluído

---

# Dashboard Web

Obrigatório.

Exibir:

* produtos;
* preços;
* lojas;
* ranking.

---

# Fontes de Dados

Primeira versão:

## Amazon

Capturar:

* nome;
* preço;
* disponibilidade;
* link.

---

## Mercado Livre

Capturar:

* nome;
* preço;
* vendedor;
* link.

---

## Ri Happy

Capturar:

* nome;
* preço;
* disponibilidade;
* link.

---

# Banco de Dados

Primeiras tabelas:

```text
stores

products

offers

price_snapshots

collector_logs
```

---

# API

Endpoints:

```http
GET /products

GET /offers

GET /opportunities

GET /products/{id}/history
```

---

# PIE v1

Primeiro modelo:

Score baseado em:

```text
30% preço atual

30% histórico

20% comparação lojas

20% disponibilidade
```

---

# Classificação

Resultado:

```text
BUY

WATCH

NORMAL

EXPENSIVE
```

---

# 4. Fora do MVP

Não serão desenvolvidos inicialmente:

❌ WhatsApp
❌ Aplicativo mobile
❌ Login
❌ Comunidade
❌ Machine Learning
❌ Previsão avançada

---

Motivo:

Precisamos validar primeiro:

* qualidade dos dados;
* precisão das análises;
* utilidade do dashboard.

---

# 5. Primeira Versão do Usuário

Usuário consegue:

1. Abrir dashboard.

2. Ver produtos Pokémon.

3. Comparar lojas.

4. Identificar oportunidades.

5. Analisar histórico.

---

# 6. Critério de Sucesso

O MVP será considerado válido quando:

* possuir coleta automática funcionando;
* apresentar histórico real;
* identificar oportunidades coerentes;
* permitir análise de preços.

---

# 7. Próximas Evoluções

Após MVP:

Adicionar:

* alertas;
* WhatsApp;
* usuários;
* favoritos;
* inteligência avançada.

---

# Considerações Finais

O MVP do PokéRadar será simples, porém construído sobre uma arquitetura preparada para crescimento.

A primeira entrega não busca ter todas as funcionalidades, mas provar que dados podem gerar inteligência de mercado Pokémon TCG.

---

# Próxima Etapa

Início da implementação:

```text
Criar backend

Criar frontend

Criar banco

Criar Docker

Primeiro código funcional
```
    