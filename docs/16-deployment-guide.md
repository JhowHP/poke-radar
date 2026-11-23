# PokéRadar - Deployment Guide

**Projeto:** PokéRadar
**Documento:** Deployment Guide
**Versão:** 1.0.0
**Autor(es):** Jonnathan Henrique e ChatGPT (OpenAI)
**Data de criação:** 23/07/2026
**Última atualização:** 23/07/2026
**Status:** Em elaboração

---

# Histórico de Alterações

| Versão | Data       | Autor                                 | Alteração                              |
| ------ | ---------- | ------------------------------------- | -------------------------------------- |
| 1.0.0  | 23/07/2026 | Jonnathan Henrique e ChatGPT (OpenAI) | Criação inicial do guia de implantação |

---

# Sumário

1. Objetivo
2. Requisitos do Ambiente
3. Estrutura de Execução
4. Ambiente Local
5. Configuração Inicial
6. Docker
7. Banco de Dados
8. Backend
9. Frontend
10. Variáveis de Ambiente
11. Migrações
12. Execução dos Collectors
13. Testes
14. Deploy em Produção
15. Monitoramento
16. Troubleshooting
17. Evolução Futura

---

# 1. Objetivo

Este documento define os procedimentos para executar o PokéRadar em diferentes ambientes.

Os ambientes considerados são:

* desenvolvimento;
* homologação;
* produção.

---

# 2. Requisitos do Ambiente

## Sistema Operacional

Suportado inicialmente:

* Windows;
* Linux;
* macOS.

---

## Ferramentas necessárias

### Git

Controle de versão.

---

### Docker

Execução dos containers.

---

### Docker Compose

Orquestração dos serviços.

---

### Node.js

Necessário para frontend.

Versão recomendada:

```text
Node.js LTS
```

---

### Python

Necessário para backend.

Versão recomendada:

```text
Python 3.12+
```

---

# 3. Estrutura de Execução

Ambiente local:

```text id="7g5h6z"
PokéRadar

|

├── Frontend

├── Backend

├── PostgreSQL

└── Redis
```

---

# 4. Ambiente Local

Objetivo:

Permitir desenvolvimento rápido.

Fluxo:

```text id="g7i3m8"
Clone Repository

↓

Configurar Ambiente

↓

Subir Containers

↓

Executar Aplicação
```

---

# 5. Configuração Inicial

Clonar projeto:

```bash
git clone https://github.com/seuusuario/pokeradar.git
```

---

Entrar na pasta:

```bash
cd pokeradar
```

---

Criar arquivos de ambiente:

```bash
.env
```

---

Copiar exemplo:

```bash
.env.example
.env
```

---

# 6. Docker

O projeto utilizará Docker Compose.

Arquivo:

```text
docker-compose.yml
```

---

Serviços:

```yaml
services:

 backend:

 frontend:

 postgres:

 redis:
```

---

Subir ambiente:

```bash
docker compose up -d
```

---

Verificar containers:

```bash
docker ps
```

---

Parar ambiente:

```bash
docker compose down
```

---

# 7. Banco de Dados

Banco:

```text
PostgreSQL
```

---

Configuração exemplo:

```env
DATABASE_HOST=postgres

DATABASE_PORT=5432

DATABASE_NAME=pokeradar

DATABASE_USER=pokeradar

DATABASE_PASSWORD=password
```

---

Acesso local:

```text
localhost:5432
```

---

# 8. Backend

Tecnologias:

* FastAPI;
* Python;
* SQLAlchemy.

---

Instalação manual:

```bash
cd backend
```

---

Criar ambiente virtual:

```bash
python -m venv venv
```

---

Ativar:

Windows:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
source venv/bin/activate
```

---

Instalar dependências:

```bash
pip install -r requirements.txt
```

---

Executar:

```bash
uvicorn app.main:app --reload
```

---

API disponível:

```text
http://localhost:8000
```

---

Documentação automática:

```text
http://localhost:8000/docs
```

---

# 9. Frontend

Tecnologias:

* React;
* TypeScript;
* Vite.

---

Instalação:

```bash
cd frontend
```

---

Dependências:

```bash
npm install
```

---

Executar:

```bash
npm run dev
```

---

Frontend:

```text
http://localhost:5173
```

---

# 10. Variáveis de Ambiente

Nunca versionar:

```text
.env
```

---

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

REDIS_HOST=localhost

API_URL=http://localhost:8000
```

---

# 11. Migrações

O banco será controlado pelo:

```text
Alembic
```

---

Criar migration:

```bash
alembic revision --autogenerate -m "create products table"
```

---

Executar:

```bash
alembic upgrade head
```

---

Voltar:

```bash
alembic downgrade -1
```

---

# 12. Execução dos Collectors

Inicialmente:

Execução manual:

```bash
python collector.py
```

---

Futuro:

Scheduler:

```text
Collector

↓

Queue

↓

Worker
```

---

# 13. Testes

Backend:

```bash
pytest
```

---

Frontend:

```bash
npm run test
```

---

Validação completa:

```text
Backend OK

Frontend OK

Database OK

Collectors OK
```

---

# 14. Deploy em Produção

Arquitetura inicial:

```text
Servidor Linux

↓

Docker

↓

Nginx

↓

Aplicação
```

---

Componentes:

```text
Frontend Container

Backend Container

Database Container

Redis Container
```

---

Processo:

```text
Merge main

↓

Build Docker

↓

Deploy

↓

Health Check
```

---

# 15. Monitoramento

Produção deverá possuir:

## Logs

Monitorar:

* erros;
* falhas;
* collectors.

---

## Saúde da aplicação

Endpoint:

```text
/api/v1/health
```

---

## Banco

Monitorar:

* espaço;
* conexões;
* backups.

---

# 16. Troubleshooting

## Backend não inicia

Verificar:

```bash
docker logs backend
```

---

## Banco indisponível

Verificar:

```bash
docker logs postgres
```

---

## Frontend sem comunicação

Verificar:

* API_URL;
* CORS;
* backend ativo.

---

## Collector falhando

Verificar:

* alteração da página;
* dados inválidos;
* bloqueio externo.

---

# 17. Evolução Futura

Possíveis melhorias:

## Cloud

Migração para:

* AWS;
* Azure;
* Google Cloud.

---

## CI/CD completo

Automatizar:

* testes;
* build;
* deploy.

---

## Infraestrutura como código

Possíveis ferramentas:

* Terraform;
* Ansible.

---

# Considerações Finais

O processo de implantação do PokéRadar foi planejado para ser simples no início e preparado para crescimento futuro.

A utilização de containers, documentação e automação permitirá que o projeto evolua mantendo organização e confiabilidade.

---

# Próximo Documento

O próximo documento será:

```text
17-project-roadmap.md
```

Ele definirá:

* fases do projeto;
* prioridades;
* entregas;
* MVP;
* evolução da plataforma.
