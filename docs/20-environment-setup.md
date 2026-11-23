# PokéRadar - Environment Setup

**Projeto:** PokéRadar
**Documento:** Environment Setup
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Status:** Em desenvolvimento

---

# Histórico de Alterações

| Versão | Data       | Autor                        | Alteração                           |
| ------ | ---------- | ---------------------------- | ----------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT | Criação inicial do guia de ambiente |

---

# Sumário

1. Objetivo
2. Requisitos da Máquina
3. Ferramentas Necessárias
4. Configuração do Git
5. Configuração do Backend
6. Configuração do Frontend
7. Configuração do Banco
8. Docker Environment
9. Variáveis de Ambiente
10. Executando o Projeto
11. Validação Inicial
12. Problemas Comuns

---

# 1. Objetivo

Este documento descreve todos os passos necessários para configurar o ambiente de desenvolvimento do PokéRadar.

Após seguir este guia, o desenvolvedor deverá conseguir:

* executar backend;
* executar frontend;
* conectar banco;
* rodar testes;
* iniciar desenvolvimento.

---

# 2. Requisitos da Máquina

## Hardware recomendado

Mínimo:

| Recurso       | Valor       |
| ------------- | ----------- |
| Processador   | 4 cores     |
| Memória RAM   | 8GB         |
| Armazenamento | 20GB livres |

---

Recomendado:

| Recurso     | Valor       |
| ----------- | ----------- |
| Processador | 6+ cores    |
| Memória RAM | 16GB        |
| SSD         | 50GB livres |

---

# 3. Ferramentas Necessárias

## Git

Responsável pelo controle de versão.

Verificar instalação:

```bash
git --version
```

---

## Docker

Responsável pelos containers.

Verificar:

```bash
docker --version
```

---

## Docker Compose

Verificar:

```bash
docker compose version
```

---

## Python

Versão:

```text
Python 3.12+
```

Verificar:

```bash
python --version
```

---

## Node.js

Versão:

```text
Node.js LTS
```

Verificar:

```bash
node --version
```

---

## Editor

Recomendado:

```text
Visual Studio Code
```

Extensões:

* Python;
* Docker;
* ESLint;
* Prettier;
* GitLens.

---

# 4. Configuração do Git

Configurar usuário:

```bash
git config --global user.name "Seu Nome"
```

---

Configurar email:

```bash
git config --global user.email "seu@email.com"
```

---

Clonar projeto:

```bash
git clone URL_DO_REPOSITORIO
```

---

Entrar:

```bash
cd pokeradar
```

---

# 5. Configuração do Backend

Entrar:

```bash
cd backend
```

---

Criar ambiente virtual:

```bash
python -m venv venv
```

---

Ativar ambiente:

## Windows

```bash
venv\Scripts\activate
```

---

## Linux/macOS

```bash
source venv/bin/activate
```

---

Instalar dependências:

```bash
pip install -r requirements.txt
```

---

Teste:

```bash
python --version
```

---

# 6. Configuração do Frontend

Entrar:

```bash
cd frontend
```

---

Instalar dependências:

```bash
npm install
```

---

Verificar:

```bash
npm --version
```

---

# 7. Configuração do Banco

Banco inicial:

```text
PostgreSQL
```

---

Configuração:

```text
Database:
pokeradar

User:
pokeradar

Password:
definido no .env
```

---

Banco será executado preferencialmente via Docker.

---

# 8. Docker Environment

O ambiente utilizará:

```text
docker-compose.yml
```

---

Serviços iniciais:

```text
PostgreSQL

Backend

Frontend
```

---

Subir ambiente:

```bash
docker compose up -d
```

---

Verificar:

```bash
docker ps
```

---

Visualizar logs:

```bash
docker compose logs -f
```

---

Parar:

```bash
docker compose down
```

---

# 9. Variáveis de Ambiente

O projeto utilizará:

```text
.env
```

---

Nunca criar diretamente no Git.

Utilizar:

```text
.env.example
```

---

Exemplo:

```env
APP_ENV=development


DATABASE_HOST=localhost

DATABASE_PORT=5432

DATABASE_NAME=pokeradar

DATABASE_USER=pokeradar

DATABASE_PASSWORD=password


API_URL=http://localhost:8000
```

---

# 10. Executando o Projeto

## Opção 1 - Docker

Recomendado:

```bash
docker compose up
```

---

## Opção 2 - Manual

### Backend

Terminal:

```bash
cd backend

uvicorn app.main:app --reload
```

Disponível:

```text
http://localhost:8000
```

---

### Frontend

Outro terminal:

```bash
cd frontend

npm run dev
```

Disponível:

```text
http://localhost:5173
```

---

# 11. Validação Inicial

Após iniciar:

## Backend

Acessar:

```text
http://localhost:8000/docs
```

Esperado:

Swagger FastAPI funcionando.

---

## Frontend

Acessar:

```text
http://localhost:5173
```

Esperado:

Dashboard inicial.

---

## Banco

Validar conexão:

```text
PostgreSQL conectado
```

---

# Primeiro teste funcional

Executar:

```http
GET /health
```

Resposta esperada:

```json
{
 "status":"healthy"
}
```

---

# 12. Problemas Comuns

---

# Docker não inicia

Verificar:

```bash
docker ps
```

Reiniciar:

```bash
docker restart container
```

---

# Porta ocupada

Exemplo:

```text
Port 5432 already in use
```

Solução:

Verificar processo utilizando a porta.

---

# Erro no npm install

Limpar:

```bash
npm cache clean --force
```

Executar novamente:

```bash
npm install
```

---

# Erro Python

Verificar ambiente:

```bash
where python
```

ou:

```bash
which python
```

---

# Banco não conecta

Validar:

* usuário;
* senha;
* porta;
* container ativo.

---

# Considerações Finais

O ambiente de desenvolvimento do PokéRadar foi projetado para permitir evolução organizada.

A utilização de Docker, variáveis de ambiente e documentação garante que o projeto possa crescer mantendo estabilidade e facilidade de manutenção.

---

# Próximo Documento

Próximo passo:

```text
21-database-implementation-plan.md
```

Definirá:

* criação inicial do banco;
* tabelas do MVP;
* migrations;
* primeiros modelos.
