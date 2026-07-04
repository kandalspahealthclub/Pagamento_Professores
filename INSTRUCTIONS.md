# Guia de Implantação: GitHub e Firebase Hosting 🚀

Este guia fornece o passo a passo para enviar o código para o **GitHub** (e ativar o **GitHub Pages**) e hospedar a aplicação no **Firebase Hosting**.

---

## Parte 1: Hospedagem no GitHub e GitHub Pages 🐙

O GitHub Pages permite hospedar o seu PWA gratuitamente diretamente a partir de um repositório Git.

### 1. Criar um Repositório no GitHub
1. Aceda a [github.com](https://github.com) e inicie sessão.
2. Clique em **New** (Novo repositório).
3. Dê o nome ao repositório (ex: `gestao-ginasio`).
4. Selecione se deseja o repositório **Public** (Público) - *obrigatório para GitHub Pages gratuito*.
5. Deixe as opções de inicializar com README, .gitignore desmarcadas.
6. Clique em **Create repository**.

### 2. Inicializar o Git Localmente e Fazer o Push
Abra o terminal (PowerShell ou Command Prompt) na pasta do seu projeto (`C:\Users\KandalSPA\Desktop\Pagamento Professores`) e execute os seguintes comandos:

```bash
# Inicializar o repositório Git
git init

# Adicionar todos os ficheiros ao commit (HTML, manifest, sw, ícones)
git add .

# Criar o primeiro commit
git commit -m "feat: inicializar PWA de Gestão de Ginásio"

# Definir a branch principal como main
git branch -M main

# Associar ao repositório remoto do GitHub (Substitua o link pelo seu repositório criado)
git remote add origin https://github.com/SEU_UTILIZADOR/NOME_DO_REPOSITORIO.git

# Enviar os ficheiros para o GitHub
git push -u origin main
```

### 3. Ativar o GitHub Pages
1. No seu repositório no GitHub, clique no separador **Settings** (Definições) no topo.
2. No menu lateral esquerdo, clique em **Pages**.
3. Na secção **Build and deployment** -> **Source**, selecione **Deploy from a branch**.
4. Em **Branch**, selecione `main` e a pasta `/ (root)`.
5. Clique em **Save**.
6. Aguarde 1 a 2 minutos. O GitHub gerará um link público para aceder à sua aplicação (ex: `https://seu-utilizador.github.io/nome-do-repositorio/`).

---

## Parte 2: Hospedagem no Firebase Hosting 🔥

O Firebase Hosting oferece uma CDN global super rápida, suporte HTTPS automático e compatibilidade ideal com PWAs.

### 1. Instalar as Ferramentas do Firebase
Caso não as tenha instaladas, instale o Node.js e o CLI do Firebase globalmente no seu computador através do terminal:

```bash
# Instalar o Firebase CLI globalmente
npm install -g firebase-tools
```

### 2. Login e Inicialização do Firebase
Execute os seguintes comandos na pasta do seu projeto:

```bash
# Fazer login na sua conta Google / Firebase
firebase login
```
*Isso abrirá uma janela no navegador para autorizar o acesso.*

```bash
# Inicializar o projeto do Firebase na pasta local
firebase init hosting
```

Durante a inicialização do Firebase Hosting, responda às perguntas assim:
1. **Choose an option**: Selecione `Use an existing project` (se já criou no console do Firebase) ou `Create a new project`.
2. **What do you want to use as your public directory?**: Escreva `.` (ponto) e pressione Enter, para usar a pasta atual em vez de criar uma pasta `public`.
3. **Configure as a single-page app (rewrite all urls to /index.html)?**: Responda `No` (ou `Yes` se pretender que todas as rotas apontem para o index.html, mas como é um app estático simples com service worker personalizado, `No` é o recomendado).
4. **Set up automatic builds and deploys with GitHub?**: Responda `No` (pode configurar depois se quiser integração contínua).
5. **File ./index.html already exists. Overwrite?**: Responda **`No`** (Muito importante para não apagar a sua aplicação).

### 3. Publicar a Aplicação
Sempre que fizer alterações e quiser publicar a versão mais recente, execute no terminal:

```bash
firebase deploy
```

O Firebase disponibilizará um link de acesso seguro (ex: `https://seu-projeto.web.app`), perfeito para o correto funcionamento de PWAs e instalação offline.
