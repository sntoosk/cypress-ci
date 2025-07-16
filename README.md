# Testes End-to-End com Cypress e GitHub Actions

Este projeto utiliza **Cypress** para testes e **GitHub Actions** para CI (Integração Contínua).

## Índice

1. [Pré-requisitos](#pré-requisitos)
2. [Instalação](#instalação)
3. [Rodando os Testes Localmente](#rodando-os-testes-localmente)
4. [GitHub Actions](#github-actions)

---

## 1. Pré-requisitos

* [Node.js](https://nodejs.org/)
* [npm](https://www.npmjs.com/)
* [Git](https://git-scm.com/)

---

## 2. Instalação

1. Clone o repositório:

   ```bash
   git clone https://github.com/sntoosk/cypress-ci.git
   cd cypress-ci
   ```

2. Instale as dependências:

   ```bash
   npm install
   ```

---

## 3. Rodando os Testes Localmente

1. Para rodar os testes com interface gráfica:

   ```bash
   npx cypress open
   ```

2. Para rodar os testes sem interface gráfica (headless):

   ```bash
   npx cypress run
   ```

---

## 4. GitHub Actions

Este projeto executa os testes automaticamente a cada push usando **GitHub Actions**.

### Workflow

O arquivo `.github/workflows/ci.yml` está configurado para rodar os testes em um ambiente Ubuntu. Ele também faz o upload de capturas de tela e vídeos em caso de falha.

```yaml
name: End-to-end tests

on: push

jobs:
  cypress-run:
    runs-on: ubuntu-24.04
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Cypress run
        uses: cypress-io/github-action@v6

      - uses: actions/upload-artifact@v4
        if: failure()
        with:
          name: cypress-screenshots
          path: cypress/screenshots
          if-no-files-found: ignore

      - uses: actions/upload-artifact@v4
        with:
          name: cypress-videos
          path: cypress/videos
          if-no-files-found: ignore
```

### Arquivos Importantes:

* **cypress/integration/todo.spec.js**: Arquivo com os testes.
* **.github/workflows/ci.yml**: Configuração do GitHub Actions.
* **package.json**: Dependências do projeto e scripts.

