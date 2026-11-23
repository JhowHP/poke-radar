# PokéRadar - Product Vision

**Projeto:** PokéRadar
**Documento:** Product Vision
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                        | Alteração                    |
| ------ | ---------- | ---------------------------- | ---------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT | Criação inicial do documento |

---

# Sumário

1. Visão do Produto
2. Problema
3. Nossa Solução
4. Público-Alvo
5. Missão
6. Visão
7. Valores
8. Diferenciais
9. Escopo da Versão 1.0
10. Funcionalidades Futuras
11. Objetivos do Projeto
12. Princípios de Desenvolvimento

---

# 1. Visão do Produto

O **PokéRadar** é uma plataforma de inteligência de mercado voltada ao Pokémon Trading Card Game (TCG) no Brasil.

Seu principal objetivo é centralizar informações de preços, promoções, histórico de valores e comportamento do mercado em um único ambiente, permitindo que colecionadores, investidores e lojistas tomem decisões baseadas em dados.

O projeto nasce com foco em qualidade, organização, escalabilidade e documentação, sendo desenvolvido desde o início seguindo boas práticas de Engenharia de Software.

O PokéRadar não será apenas um comparador de preços.

Nossa visão é construir a principal plataforma brasileira de inteligência de mercado para Pokémon TCG.

---

# 2. Problema

Hoje, acompanhar o mercado brasileiro de Pokémon TCG exige visitar diversas lojas individualmente.

Entre elas:

* Amazon
* Mercado Livre
* Ri Happy
* Copag Store
* Liga Pokémon

Cada loja possui:

* preços diferentes;
* promoções exclusivas;
* disponibilidade variável;
* fretes distintos;
* campanhas temporárias.

Além disso:

* não existe um histórico consolidado de preços;
* não existe comparação automática entre lojas;
* não existe um indicador confiável de oportunidade;
* não existe uma plataforma especializada no mercado brasileiro.

Como consequência, o usuário precisa realizar toda a análise manualmente.

---

# 3. Nossa Solução

O PokéRadar será responsável por:

* Monitorar automaticamente diversas lojas.
* Registrar histórico completo de preços.
* Comparar preços entre lojas.
* Detectar promoções relevantes.
* Gerar indicadores de mercado.
* Construir estatísticas históricas.
* Disponibilizar dashboards analíticos.
* Calcular um índice próprio de oportunidade.
* Futuramente enviar alertas personalizados.

Nosso objetivo não é apenas mostrar onde um produto está mais barato.

Nosso objetivo é responder:

> **"Vale a pena comprar agora?"**

---

# 4. Público-Alvo

## Colecionadores

Pessoas que desejam completar coleções pagando o menor preço possível.

### Principais necessidades

* Comparar preços.
* Encontrar promoções.
* Histórico de preços.
* Acompanhamento de lançamentos.

---

## Investidores

Usuários interessados em produtos lacrados, potencial de valorização e oportunidades de compra.

### Principais necessidades

* Identificação de oportunidades.
* Histórico completo.
* Score de investimento.
* Comparativos entre expansões.

---

## Lojistas

Empresas e vendedores que desejam acompanhar o mercado e seus concorrentes.

### Principais necessidades

* Comparação entre lojas.
* Monitoramento de preços.
* Tendências do mercado.
* Indicadores estratégicos.

---

# 5. Missão

Transformar dados dispersos do mercado brasileiro de Pokémon TCG em informações confiáveis e inteligentes para apoiar a tomada de decisão de colecionadores, investidores e lojistas.

---

# 6. Visão

Ser reconhecido como a principal plataforma brasileira de inteligência de mercado para Pokémon TCG.

---

# 7. Valores

O desenvolvimento do PokéRadar será guiado pelos seguintes princípios:

* Transparência
* Confiabilidade dos dados
* Código limpo
* Arquitetura escalável
* Documentação completa
* Evolução contínua
* Simplicidade
* Foco na comunidade
* Compartilhamento de conhecimento

---

# 8. Diferenciais

O PokéRadar não será apenas um comparador de preços.

Seus diferenciais incluem:

* Histórico completo de preços.
* Comparação entre lojas.
* Dashboard analítico.
* KPIs.
* Indicadores de mercado.
* Sistema próprio de Score.
* Gráficos históricos.
* Arquitetura preparada para expansão.
* Plataforma especializada exclusivamente em Pokémon TCG.

---

# 9. Escopo da Versão 1.0

A primeira versão da plataforma contemplará:

## Dashboard Web

* Página inicial.
* Produtos monitorados.
* Comparação entre lojas.
* Histórico de preços.
* Gráficos.
* Busca e filtros.

---

## Backend

* API REST utilizando FastAPI.
* Scheduler para atualização automática.
* Banco PostgreSQL.
* Estrutura modular.

---

## Monitoramento

As seguintes lojas serão monitoradas:

* Amazon
* Mercado Livre
* Ri Happy
* Copag Store
* Liga Pokémon

---

## Inteligência

Será desenvolvido o **POS — Pokémon Opportunity Score**, responsável por indicar a qualidade de uma oportunidade de compra considerando diversos fatores, como preço atual, histórico, frequência de promoções e comparação entre lojas.

---

# 10. Funcionalidades Futuras

Após a versão 1.0, o projeto poderá evoluir para incluir:

* Alertas via WhatsApp.
* Alertas por Telegram.
* Alertas por e-mail.
* Login de usuários.
* Favoritos.
* Listas personalizadas.
* Aplicativo mobile.
* Inteligência Artificial para previsão de preços.
* Comparação entre expansões.
* Radar de lançamentos.
* Relatórios automáticos.

---

# 11. Objetivos do Projeto

O PokéRadar possui dois objetivos principais.

## Objetivo de Produto

Construir uma plataforma real, útil e escalável para a comunidade brasileira de Pokémon TCG.

---

## Objetivo Técnico

Servir como um projeto de referência em:

* Arquitetura de Software.
* Desenvolvimento Backend.
* Desenvolvimento Frontend.
* Banco de Dados.
* APIs.
* Documentação.
* Engenharia de Software.
* Boas práticas de desenvolvimento.

---

# 12. Princípios de Desenvolvimento

Durante todo o desenvolvimento seguiremos os seguintes princípios:

* Documentar antes de implementar.
* Desenvolver de forma incremental.
* Priorizar qualidade em vez de velocidade.
* Manter arquitetura modular.
* Automatizar testes sempre que possível.
* Registrar decisões arquiteturais (ADR).
* Pensar sempre na escalabilidade.
* Evitar retrabalho.
* Manter o projeto preparado para produção.

---

# Considerações Finais

O PokéRadar nasce com a proposta de ir além de um simples monitor de promoções.

Seu propósito é transformar informações dispersas em inteligência de mercado, oferecendo uma plataforma robusta, confiável e escalável para o ecossistema brasileiro de Pokémon TCG.

Este documento representa a visão estratégica do projeto e servirá como referência para todas as decisões técnicas e de negócio durante seu desenvolvimento.
