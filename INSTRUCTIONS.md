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

---

## Parte 3: Configurar a Base de Dados (Cloud Firestore) ☁️

Para que a sincronização em tempo real funcione, precisa de ativar a base de dados Firestore no seu projeto Firebase:

### 1. Ativar o Cloud Firestore
1. Vá à [Consola do Firebase](https://console.firebase.google.com/) e entre no seu projeto.
2. No menu lateral, clique em **Build** (Construir) -> **Firestore Database**.
3. Clique em **Create database** (Criar base de dados).
4. Escolha a localização da base de dados mais próxima de si (ex: `europe-west` ou similar).
5. Selecione **Start in test mode** (Iniciar em modo de teste) para poder começar a ler e escrever dados imediatamente.
6. Clique em **Create** (Criar).

> [!WARNING]
> O modo de teste deixa a base de dados aberta a qualquer utilizador por um período inicial (normalmente 30 dias). Para produção, configure as regras de segurança no separador **Rules** do Firestore para restringir o acesso.

### 2. Obter as Credenciais da Web App
1. No menu lateral da consola do Firebase, clique na **Engrenagem** ao lado de "Project Overview" -> **Project settings** (Definições do projeto).
2. Na secção **Your apps**, clique no ícone **`Web (</>)`** para registar a aplicação se ainda não o tiver feito.
3. Copie o objeto `firebaseConfig` gerado, que se parece com isto:
   ```javascript
   const firebaseConfig = {
     apiKey: "AIzaSy...",
     authDomain: "seu-projeto.firebaseapp.com",
     projectId: "seu-projeto",
     storageBucket: "seu-projeto.appspot.com",
     messagingSenderId: "...",
     appId: "..."
   };
   ```

### 3. Ligar a Aplicação à Base de Dados
1. Abra a sua aplicação no navegador (pode ser o arquivo local [index.html](file:///c:/Users/KandalSPA/Desktop/Pagamento%20Professores/index.html) ou a versão publicada).
2. Clique na **Engrenagem (⚙️)** que surge no topo do ecrã, abaixo do título.
3. Cole as credenciais que copiou no passo anterior e clique em **Conectar e Sincronizar**.
4. O indicador mudará para **Firebase: Ligado (Sincronizado)** (ponto verde) e todos os seus dados (professores, aulas e grelha de horários) passarão a ser guardados e atualizados na nuvem em tempo real!
