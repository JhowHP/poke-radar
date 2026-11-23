# PokéRadar - Product Requirements Document (PRD)

**Projeto:** PokéRadar
**Documento:** Product Requirements Document (PRD)
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                        | Alteração              |
| ------ | ---------- | ---------------------------- | ---------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT | Criação inicial do PRD |

---

# Sumário

1. Objetivo
2. Escopo
3. Personas
4. Requisitos Funcionais
5. Requisitos Não Funcionais
6. Fluxo Geral
7. Critérios de Aceitação
8. Métricas de Sucesso
9. Fora do Escopo
10. Riscos
11. Premissas

---

# 1. Objetivo

Definir todos os requisitos necessários para o desenvolvimento da primeira versão do PokéRadar.

Este documento servirá como referência para o desenvolvimento do backend, frontend, banco de dados e infraestrutura.

---

# 2. Escopo

A versão 1.0 deverá permitir que o usuário:

* Consulte preços de produtos Pokémon TCG.
* Compare preços entre lojas.
* Visualize histórico de preços.
* Identifique oportunidades de compra.
* Acompanhe indicadores de mercado.
* Utilize um dashboard analítico.

---

# 3. Personas

## Colecionador

Objetivo:

Comprar produtos pelo menor preço possível.

Principais necessidades:

* Histórico de preços.
* Comparação entre lojas.
* Promoções.

---

## Investidor

Objetivo:

Identificar produtos com potencial de valorização.

Principais necessidades:

* Histórico de longo prazo.
* Tendências.
* Score de oportunidade.

---

## Lojista

Objetivo:

Acompanhar concorrentes e tendências.

Principais necessidades:

* Comparativo entre lojas.
* Monitoramento contínuo.
* Indicadores estratégicos.

---

# 4. Requisitos Funcionais

## RF-001

O sistema deverá cadastrar lojas monitoradas.

---

## RF-002

O sistema deverá cadastrar produtos.

---

## RF-003

O sistema deverá coletar automaticamente os preços das lojas suportadas.

---

## RF-004

O sistema deverá armazenar o histórico de preços.

---

## RF-005

O sistema deverá comparar preços entre diferentes lojas.

---

## RF-006

O sistema deverá exibir gráficos de evolução de preços.

---

## RF-007

O sistema deverá calcular o POS (Pokémon Opportunity Score).

---

## RF-008

O sistema deverá disponibilizar filtros por:

* Loja
* Expansão
* Categoria
* Faixa de preço
* Disponibilidade

---

## RF-009

O sistema deverá permitir pesquisa por nome do produto.

---

## RF-010

O sistema deverá apresentar um Dashboard com indicadores estratégicos.

---

# 5. Requisitos Não Funcionais

* Arquitetura modular.
* API REST.
* Banco PostgreSQL.
* Frontend React + TypeScript.
* Backend FastAPI.
* Código documentado.
* Tempo de resposta otimizado.
* Sistema preparado para expansão.
* Docker para desenvolvimento.
* Versionamento via Git.

---

# 6. Fluxo Geral

1. O coletor acessa as lojas.
2. Os preços são normalizados.
3. Os dados são armazenados.
4. O PIE analisa os dados.
5. O POS é calculado.
6. O Dashboard apresenta os resultados ao usuário.

---

# 7. Critérios de Aceitação

Uma funcionalidade será considerada concluída quando:

* Estiver documentada.
* Possuir testes compatíveis com sua criticidade.
* Estiver integrada aos demais módulos.
* Estiver validada funcionalmente.
* Não possuir defeitos conhecidos de alta severidade.

---

# 8. Métricas de Sucesso

O sucesso da versão 1.0 será medido por indicadores como:

* Quantidade de lojas monitoradas.
* Produtos cadastrados.
* Produtos atualizados diariamente.
* Tempo médio de atualização.
* Precisão dos preços.
* Tempo médio de resposta da aplicação.

---

# 9. Fora do Escopo da Versão 1.0

As funcionalidades abaixo ficam planejadas para versões futuras:

* Login de usuários.
* Favoritos.
* Alertas via WhatsApp.
* Alertas via Telegram.
* Alertas por e-mail.
* Aplicativo mobile.
* Inteligência Artificial preditiva.
* API pública.

---

# 10. Riscos

* Alterações nas páginas das lojas podem impactar os coletores.
* Restrições de acesso (anti-bot, rate limit ou CAPTCHA) podem exigir adaptações.
* Diferenças de nomenclatura entre lojas exigirão mecanismos de normalização.
* Crescimento do volume de dados exigirá otimizações de desempenho.

---

# 11. Premissas

* O sistema iniciará monitorando Amazon, Mercado Livre, Ri Happy, Copag Store e Liga Pokémon.
* O PIE será o principal motor de inteligência da plataforma.
* O POS será recalculado sempre que houver atualização relevante de preços.
* Todo novo módulo deverá possuir documentação correspondente antes da implementação.

---

# Considerações Finais

Este PRD representa a especificação funcional da primeira versão do PokéRadar.

Todas as implementações deverão estar alinhadas a este documento. Novas funcionalidades deverão ser avaliadas quanto ao impacto no escopo e, quando necessário, registradas em um RFC antes do desenvolvimento.
