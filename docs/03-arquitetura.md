# PokéRadar - Arquitetura da Plataforma

**Projeto:** PokéRadar
**Documento:** Arquitetura da Plataforma
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
2. Visão Geral da Arquitetura
3. Princípios Arquiteturais
4. Camadas da Aplicação
5. Organização por Domínio
6. Estrutura do Backend
7. Estrutura do Frontend
8. Fluxo de Dados
9. Integração entre Módulos
10. Escalabilidade
11. Decisões Arquiteturais

---

# 1. Objetivo

Definir a arquitetura técnica do PokéRadar, estabelecendo padrões que garantam organização, escalabilidade, manutenção e evolução contínua da plataforma.

Este documento servirá como referência para todas as implementações futuras.

---

# 2. Visão Geral da Arquitetura

O PokéRadar será desenvolvido como um **Monólito Modular (Modular Monolith)**, inspirado em princípios da **Clean Architecture** e do **Domain-Driven Design (DDD)**.

Essa abordagem oferece:

* Separação clara de responsabilidades.
* Alta coesão entre módulos.
* Baixo acoplamento.
* Facilidade de manutenção.
* Escalabilidade para futuras evoluções.

---

# 3. Princípios Arquiteturais

Durante todo o desenvolvimento seguiremos os seguintes princípios:

* Organização por domínio de negócio.
* Código desacoplado.
* Separação entre regras de negócio e infraestrutura.
* Reutilização de componentes.
* Testabilidade.
* Escalabilidade.
* Documentação contínua.
* Simplicidade antes da complexidade.

---

# 4. Camadas da Aplicação

A arquitetura será composta pelas seguintes camadas:

## Frontend

Responsável pela interface do usuário.

Tecnologias:

* React
* TypeScript
* Vite
* Chakra UI

---

## API

Camada responsável por expor os serviços REST.

Tecnologia:

* FastAPI

---

## Application Layer

Responsável por coordenar os casos de uso da aplicação.

Não contém regras de persistência.

---

## Domain Layer

Contém toda a regra de negócio.

É considerada o núcleo da aplicação.

Inclui:

* PIE (PokéRadar Intelligence Engine)
* POS (Pokémon Opportunity Score)
* Serviços de domínio
* Regras de negócio

---

## Infrastructure Layer

Responsável por:

* Banco de dados
* Scheduler
* Coletores
* Cache
* Integrações externas
* Logs

---

# 5. Organização por Domínio

O backend será organizado por domínios de negócio.

Domínios previstos para a versão 1.0:

* Products
* Stores
* Prices
* History
* Analytics
* Score
* Collectors
* Notifications (estrutura preparada para versões futuras)

Cada domínio possuirá autonomia e responsabilidade bem definidas.

---

# 6. Estrutura do Backend

Cada domínio seguirá uma estrutura padronizada:

```text
domain/

api.py

service.py

repository.py

models.py

schemas.py

exceptions.py
```

Além disso, existirão módulos compartilhados:

```text
core/
```

Responsável por:

* Configurações
* Banco de dados
* Segurança
* Logger
* Dependências
* Utilitários
* Variáveis de ambiente

---

# 7. Estrutura do Frontend

O frontend será organizado por funcionalidades.

Estrutura prevista:

```text
src/

components/

pages/

services/

hooks/

layouts/

contexts/

routes/

assets/

utils/
```

Essa organização favorece reutilização e manutenção.

---

# 8. Fluxo de Dados

Fluxo padrão de uma requisição:

1. Usuário acessa o Dashboard.
2. Frontend envia requisição para a API.
3. API encaminha para o domínio responsável.
4. O domínio executa as regras de negócio.
5. O Repository realiza acesso ao banco.
6. O resultado retorna ao frontend.

Para atualização de preços:

1. Scheduler inicia os coletores.
2. Coletores obtêm dados das lojas.
3. Dados são normalizados.
4. Banco é atualizado.
5. PIE recalcula indicadores.
6. POS é atualizado.
7. Dashboard passa a refletir as novas informações.

---

# 9. Integração entre Módulos

Os módulos deverão interagir por meio de interfaces bem definidas.

Regras:

* Um domínio não deverá acessar diretamente o banco de outro domínio.
* Regras de negócio deverão permanecer na camada de domínio.
* A camada de infraestrutura não conterá regras de negócio.

---

# 10. Escalabilidade

A arquitetura foi planejada para permitir:

* Inclusão de novas lojas.
* Inclusão de novos dashboards.
* Novos algoritmos no PIE.
* Novos tipos de Score.
* Integração com notificações.
* Evolução para microsserviços, caso necessário no futuro.

---

# 11. Decisões Arquiteturais

Para a versão 1.0 foram definidas as seguintes tecnologias:

| Camada          | Tecnologia         |
| --------------- | ------------------ |
| Backend         | FastAPI            |
| Frontend        | React + TypeScript |
| Banco de Dados  | PostgreSQL         |
| ORM             | SQLAlchemy         |
| Migrações       | Alembic            |
| Scheduler       | APScheduler        |
| Cache (futuro)  | Redis              |
| Containerização | Docker             |
| Versionamento   | Git + GitHub       |

---

# Considerações Finais

A arquitetura do PokéRadar foi concebida para suportar crescimento contínuo, mantendo simplicidade no início do projeto e flexibilidade para evoluções futuras.

Toda implementação deverá respeitar os princípios definidos neste documento, garantindo consistência, qualidade e facilidade de manutenção ao longo do ciclo de vida da plataforma.
