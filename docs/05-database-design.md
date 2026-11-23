# PokéRadar - Database Design

**Projeto:** PokéRadar
**Documento:** Database Design (Projeto do Banco de Dados)
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

1. Objetivo
2. Filosofia do Banco de Dados
3. Objetivos de Negócio
4. Classificação dos Dados
5. Estratégia de Modelagem
6. Integridade dos Dados
7. Estratégia de Crescimento
8. Performance
9. Versionamento
10. Backup e Recuperação
11. Diretrizes de Desenvolvimento
12. Próximos Documentos

---

# 1. Objetivo

Este documento define as diretrizes para o projeto do banco de dados do PokéRadar.

Seu propósito é garantir que a estrutura de dados seja consistente, escalável, auditável e preparada para suportar o crescimento da plataforma ao longo dos anos.

Este documento não define tabelas ou colunas específicas. Essas informações serão documentadas posteriormente no Modelo ER e no Dicionário de Dados.

---

# 2. Filosofia do Banco de Dados

O banco de dados do PokéRadar será construído seguindo os seguintes princípios:

* Integridade acima de conveniência.
* Histórico nunca será perdido.
* Dados devem ser rastreáveis.
* Estrutura preparada para crescimento contínuo.
* Baixo acoplamento entre entidades.
* Modelo orientado ao domínio de negócio.

O banco será uma representação fiel do domínio definido no documento **04-domain-model.md**.

---

# 3. Objetivos de Negócio

O banco deverá ser capaz de responder, de forma eficiente, perguntas como:

* Qual o menor preço histórico de um produto?
* Qual loja apresenta o menor preço atualmente?
* Como o preço evoluiu ao longo do tempo?
* Quais produtos apresentam oportunidade de compra?
* Quais expansões tiveram maior valorização?
* Quais lojas realizam promoções com maior frequência?
* Qual foi a última captura realizada para uma oferta?

Esses objetivos orientarão toda a modelagem física do banco.

---

# 4. Classificação dos Dados

Os dados da plataforma serão organizados em três categorias.

## Dados Mestres

Informações com baixa frequência de alteração.

Exemplos:

* Produtos
* Expansões
* Lojas
* Categorias

---

## Dados Operacionais

Informações atualizadas continuamente pelos coletores.

Exemplos:

* Ofertas
* Price Snapshots
* Execuções dos Coletores

---

## Dados Analíticos

Informações produzidas pelo PIE.

Exemplos:

* Opportunity Score (POS)
* Promoções Detectadas
* Indicadores
* Estatísticas

---

# 5. Estratégia de Modelagem

O modelo de dados seguirá os seguintes princípios:

## Identificadores

Cada entidade possuirá:

* Identificador técnico (UUID).
* Código interno amigável (ex.: PKR-PROD-000001), quando fizer sentido para o domínio.

---

## Auditoria

As principais entidades deverão possuir:

* created_at
* updated_at

Quando houver autenticação de usuários, poderão ser adicionados:

* created_by
* updated_by

---

## Exclusão Lógica

Entidades principais utilizarão exclusão lógica (Soft Delete) quando aplicável.

Sempre que possível, registros históricos serão preservados.

---

## Histórico Imutável

Entidades históricas, como os **Price Snapshots**, serão somente de inserção.

Atualizações e exclusões não deverão ocorrer, exceto em situações excepcionais de manutenção.

---

## Responsabilidade Única

Cada entidade representará apenas um conceito de negócio.

Exemplo:

* Produto representa um produto.
* Oferta representa uma oferta.
* Snapshot representa uma captura daquela oferta.

---

# 6. Integridade dos Dados

O banco deverá garantir:

* Chaves primárias consistentes.
* Chaves estrangeiras entre entidades relacionadas.
* Restrições de unicidade quando aplicável.
* Valores obrigatórios para informações essenciais.
* Integridade referencial entre produtos, ofertas e capturas.

Sempre que possível, regras de integridade deverão ser aplicadas no banco de dados e complementadas pela camada de aplicação.

---

# 7. Estratégia de Crescimento

A modelagem deverá permitir:

* Inclusão de novas lojas sem alterações estruturais significativas.
* Inclusão de novos tipos de produtos.
* Inclusão de novos indicadores.
* Crescimento do histórico de preços.
* Inclusão futura de usuários, favoritos e portfólios.

O crescimento da base de dados não deverá exigir remodelagem do domínio.

---

# 8. Performance

A estratégia inicial de performance incluirá:

* Índices para consultas frequentes.
* Índices compostos quando necessário.
* Consultas otimizadas para histórico de preços.
* Planejamento para particionamento futuro das tabelas históricas, caso o volume de dados justifique.

Toda otimização deverá ser baseada em medições reais de desempenho.

---

# 9. Versionamento

Toda alteração estrutural do banco será realizada por meio de migrações utilizando **Alembic**.

Não serão permitidas alterações manuais diretamente no banco de produção.

Cada migração deverá possuir:

* Objetivo claro.
* Descrição da alteração.
* Compatibilidade com versões anteriores, sempre que possível.

---

# 10. Backup e Recuperação

O banco deverá possuir uma estratégia de recuperação que contemple:

* Backups periódicos.
* Testes de restauração.
* Proteção contra perda de dados.
* Procedimentos documentados para recuperação em caso de falha.

Os detalhes operacionais serão definidos na documentação de infraestrutura.

---

# 11. Diretrizes de Desenvolvimento

Durante a implementação deverão ser seguidas as seguintes diretrizes:

* Evitar duplicação de dados.
* Utilizar tipos de dados apropriados.
* Não utilizar campos genéricos sem propósito definido.
* Não armazenar informações derivadas quando puderem ser calculadas.
* Priorizar clareza na nomenclatura das entidades e atributos.
* Toda alteração estrutural deverá ser acompanhada de documentação.

---

# 12. Próximos Documentos

Este documento será complementado pelos seguintes artefatos:

* **05.1-er-diagram.md** — Modelo Entidade-Relacionamento.
* **05.2-data-dictionary.md** — Dicionário de Dados.
* Migrações do Alembic.
* Scripts de criação do banco.

---

# Considerações Finais

O banco de dados do PokéRadar foi concebido para ser um dos pilares da plataforma.

Seu objetivo não é apenas armazenar informações, mas preservar a evolução do mercado de Pokémon TCG, permitindo análises históricas, geração de indicadores e suporte à tomada de decisão.

Todas as futuras implementações deverão respeitar as diretrizes estabelecidas neste documento para garantir consistência, desempenho e facilidade de manutenção.
