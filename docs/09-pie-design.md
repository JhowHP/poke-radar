# PokéRadar - PIE Design

**Projeto:** PokéRadar
**Documento:** PokéRadar Intelligence Engine (PIE) Design
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                                 | Alteração                    |
| ------ | ---------- | ------------------------------------- | ---------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT (OpenAI) | Criação inicial do documento |

---

# Sumário

1. Objetivo
2. Conceito do PIE
3. Responsabilidades
4. Arquitetura
5. Dados de Entrada
6. Processamento
7. Pokémon Opportunity Score (POS)
8. Indicadores
9. Classificação de Oportunidades
10. Explicabilidade
11. Evolução com IA
12. Considerações Finais

---

# 1. Objetivo

O PokéRadar Intelligence Engine (PIE) é o motor responsável por transformar dados coletados pelo sistema em inteligência de mercado.

Seu objetivo é analisar:

* preços atuais;
* histórico de preços;
* comportamento das lojas;
* disponibilidade;
* tendências;

para gerar recomendações úteis aos usuários.

---

# 2. Conceito do PIE

O PIE responde uma pergunta principal:

> "Este produto representa uma boa oportunidade neste momento?"

---

O PIE não compra.

O PIE não vende.

O PIE não substitui decisão humana.

Ele fornece:

* dados;
* contexto;
* indicadores;
* recomendações.

---

# 3. Responsabilidades

O PIE será responsável por:

## Análise de preço

Comparar:

* preço atual;
* média histórica;
* menor preço;
* maior preço.

---

## Detecção de promoções

Identificar:

* quedas relevantes;
* descontos reais;
* oportunidades fora do padrão.

---

## Classificação

Determinar:

* oportunidade alta;
* oportunidade média;
* oportunidade baixa.

---

## Explicação

Informar o motivo da recomendação.

Exemplo:

"Preço 18% abaixo da média dos últimos 90 dias."

---

# 4. Arquitetura

Fluxo:

```text
Price Snapshots

        ↓

Data Processing

        ↓

PIE Engine

        ↓

Scoring

        ↓

Opportunity

        ↓

Dashboard
```

---

# Componentes

## Analyzer

Responsável pela análise dos dados.

Exemplo:

* média;
* tendência;
* variação.

---

## Scoring Engine

Responsável por calcular pontuação.

---

## Rules Engine

Responsável pelas regras de negócio.

---

## Recommendation Engine

Responsável pela mensagem final.

---

# 5. Dados de Entrada

O PIE utilizará:

## Price Snapshot

Dados:

* preço;
* estoque;
* frete;
* data.

---

## Product

Dados:

* expansão;
* categoria;
* lançamento.

---

## Store

Dados:

* loja;
* histórico de comportamento.

---

## Offer

Dados:

* vendedor;
* disponibilidade;
* URL.

---

# 6. Processamento

Fluxo:

```text
Novo Snapshot

↓

Atualizar Histórico

↓

Calcular Indicadores

↓

Executar Regras

↓

Calcular POS

↓

Gerar Opportunity
```

---

# 7. Pokémon Opportunity Score (POS)

O POS será o principal indicador do PokéRadar.

Representa a oportunidade de compra de um produto.

Escala:

```text
0 - 100
```

---

Exemplo:

```text
90-100

Excelente oportunidade

70-89

Boa oportunidade

50-69

Acompanhar

0-49

Preço normal
```

---

# Composição inicial do POS

## Preço Histórico

Peso sugerido:

30%

Analisa:

* média histórica;
* menor preço;
* distância da média.

---

## Tendência

Peso sugerido:

25%

Analisa:

* queda recente;
* estabilidade;
* valorização.

---

## Disponibilidade

Peso sugerido:

15%

Analisa:

* estoque;
* quantidade de lojas.

---

## Produto

Peso sugerido:

15%

Analisa:

* popularidade;
* expansão;
* procura.

---

## Loja

Peso sugerido:

15%

Analisa:

* confiabilidade;
* histórico de promoções.

---

# 8. Indicadores

O PIE poderá gerar:

---

## Discount Indicator

Mostra desconto atual.

Exemplo:

```text
Preço atual:
R$220

Média:
R$280

Diferença:
21%
```

---

## Historical Position

Posição do preço atual.

Exemplo:

```text
Menor preço histórico:
R$210

Preço atual:
R$220
```

---

## Trend Indicator

Identifica tendência.

Possíveis valores:

* SUBINDO
* ESTÁVEL
* CAINDO

---

## Store Behavior

Analisa comportamento da loja.

Exemplo:

"Amazon possui histórico de queda de preço em finais de semana."

---

# 9. Classificação de Oportunidades

Resultado:

## BUY

Compra recomendada.

Exemplo:

POS >= 85

---

## WATCH

Acompanhar.

Exemplo:

POS entre 60 e 84

---

## HOLD

Sem oportunidade.

Exemplo:

POS < 60

---

# 10. Explicabilidade

Toda recomendação deverá possuir justificativa.

Nunca retornar apenas:

```json
{
"score":95
}
```

---

Deverá retornar:

```json
{
"score":95,

"reason":[

"Preço 22% abaixo da média",

"Menor preço dos últimos 120 dias",

"Produto disponível em 3 lojas"

]
}
```

---

A confiança do usuário será construída através da transparência.

---

# 11. Evolução com IA

O PIE inicialmente utilizará regras determinísticas.

Exemplo:

```text
SE preço < média histórica
E estoque disponível

ENTÃO aumentar score
```

---

No futuro poderá incorporar:

## Machine Learning

Para prever:

* valorização;
* tendência futura;
* comportamento de coleção.

---

## IA Generativa

Para gerar:

* análises;
* resumos;
* explicações personalizadas.

---

Exemplo:

"Essa ETB apresenta oportunidade porque caiu 18% em relação à média dos últimos 90 dias e normalmente volta a subir após períodos promocionais."

---

# 12. Considerações Finais

O PIE é o principal diferencial competitivo do PokéRadar.

Enquanto comparadores tradicionais mostram apenas preços, o PokéRadar transforma dados históricos em inteligência para tomada de decisão.

O objetivo final é permitir que qualquer usuário responda:

> "Eu estou comprando no momento certo?"

---

# Próximo Documento

O próximo documento será:

```text
10-infrastructure.md
```

Ele definirá:

* Docker;
* ambientes;
* servidores;
* banco;
* CI/CD;
* deploy;
* monitoramento.
