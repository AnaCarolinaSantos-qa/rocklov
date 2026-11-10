# Rocklov

Repositório de automação de testes para o projeto Rocklov, organizado em duas suítes Ruby:

- `api/`: testes RSpec para a API.
- `web/`: testes end-to-end com Cucumber, Capybara e Selenium.

## Pré-requisitos

As suítes dependem de serviços externos ao repositório. A rede Docker usada pelos Jenkinsfiles precisa disponibilizar:

- MongoDB em `rocklov-db:27017`;
- API em `rocklov-api:3333`;
- aplicação web em `rocklov-web:3000`;
- navegador e dependências Selenium compatíveis com a imagem de agente da suíte web.

Este repositório não inclui os serviços da aplicação nem uma configuração Docker Compose.

## Executar os testes

Para a API:

```bash
cd api
bundle install
bundle exec rspec
```

Para a suíte web, com a rede e serviços acima ativos:

```bash
cd web
bundle install
BROWSER=chrome_headless bundle exec rake seeds
```

A tarefa `seeds` prepara dados de teste e inicia o Cucumber. **A suíte da API apaga o banco configurado antes de rodar**; use apenas um banco descartável de teste.

## Integração contínua

Os Jenkinsfiles em `api/Jenkinsfile` e `web/Jenkinsfile` descrevem os pipelines existentes. Para reproduzir o ambiente, configure a rede e os serviços listados acima antes de executar os agentes.

## Estado de manutenção

As dependências Ruby estão fixadas em versões antigas. Atualize-as em uma mudança separada, depois de confirmar a compatibilidade com as imagens e serviços de teste usados pelo Jenkins.
