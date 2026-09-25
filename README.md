# 🛡️ Guia: Organizações, Projetos e Proteção de Branches no GitHub

Este guia prático ensina passo a passo como criar uma **Organização no GitHub**, inicializar um novo repositório/projeto, criar a branch `develop` e configurar regras de proteção de branch (**Branch Protection Rules**) para impedir commits diretos nas branches principais (`main` e `develop`).

---

## 📑 Sumário

1. [Por que proteger branches?](#-por-que-proteger-branches)
2. [Passo 1: Criando uma Organização no GitHub](#-passo-1-criando-uma-organização-no-github)
3. [Passo 2: Inicializando um Projeto (Repositório) e Criando a Branch develop](#-passo-2-inicializando-um-projeto-repositório-e-criando-a-branch-develop)
4. [Passo 3: Configurando o Bloqueio de Branches (main e develop)](#-passo-3-configurando-o-bloqueio-de-branches-main-e-develop)
5. [Fluxo de Trabalho Recomendado (Pull Request Flow)](#-fluxo-de-trabalho-recomendado-pull-request-flow)

---

## 🎯 Por que proteger branches?

Em projetos colaborativos ou profissionais, permitir commits diretos nas branches principais (`main` e `develop`) pode causar:
- Subida de código quebrado ou sem testes.
- Conflitos de merge desnecessários.
- Falta de revisão por pares (*Code Review*).

Ao bloquear commits diretos, toda alteração deve passar obrigatoriamente por uma branch de funcionalidade/correção e por um **Pull Request (PR)** com aprovação.

---

## 🏢 Passo 1: Criando uma Organização no GitHub

Uma organização permite gerenciar times, repositórios compartilhados e permissões granulares de forma centralizada.

1. Faça login na sua conta no [GitHub](https://github.com).
2. No canto superior direito, clique na sua **foto de perfil**.
3. Selecione a opção **"Your organizations"** (Suas organizações).
4. Clique no botão verde **"New organization"** (Nova organização).
5. Escolha o plano desejado (o plano **Free** atende perfeitamente para times e estudos):
   - Clique em **"Create a free organization"**.
6. Preencha os campos obrigatórios:
   - **Organization account name**: Nome único da sua organização.
   - **Contact email**: E-mail para contato/administração.
   - Selecione se a organização pertence à sua conta pessoal ou a uma empresa/instituição.
7. Conclua a verificação de segurança (captcha) e clique em **"Next"**.
8. *(Opcional)* Convide membros para fazerem parte da organização informando os usuários do GitHub ou e-mails. Se preferir fazer isso depois, clique em **"Complete setup"**.

---

## 🚀 Passo 2: Inicializando um Projeto (Repositório) e Criando a Branch develop

Com a organização criada, crie o repositório do projeto e inicialize a branch `develop`:

### 2.1 Criando o Repositório

1. Na página inicial da organização, clique no botão verde **"Create a new repository"** (ou na aba **Repositories** > **"New repository"**).
2. Defina os detalhes do projeto:
   - **Repository name**: Nome do repositório (ex.: `app-block-branches`).
   - **Description**: Breve descrição sobre o que é o projeto.
   - **Visibility**:
     - `Public`: Qualquer pessoa na internet pode ver o repositório.
     - `Private`: Apenas você e membros autorizados da organização têm acesso.
   - **Initialize this repository with**:
     - Marque **Add a README file** (importante para que a branch padrão `main` já seja criada imediatamente).
     - *(Opcional)* Escolha um modelo de `.gitignore` (ex.: Java, Node) e licença, se aplicável.
3. Clique em **"Create repository"**.

### 2.2 Criando a Branch `develop`

Logo após a criação do repositório, crie a branch `develop` (a partir da `main`). Ela será a branch de integração do dia a dia do time. Você pode criá-la de duas formas:

**Opção A — Pela Interface Web do GitHub:**
1. Na página principal do seu repositório, clique no seletor de branches (o menu suspenso que mostra **`main`** 🌿).
2. Digite `develop` no campo de busca/texto.
3. Clique em **"Create branch: develop from 'main'"**.

**Opção B — Pelo Terminal (Git CLI):**
Se você já clonou o projeto em sua máquina:
```bash
git checkout -b develop
git push -u origin develop
```

---

## 🔒 Passo 3: Configurando o Bloqueio de Branches (main e develop)

Agora vamos configurar as regras de proteção (**Branch Protection Rules**) para impedir que desenvolvedores (inclusive administradores) façam `git push` direto tanto na branch `main` quanto na `develop`.

### 1. Acessando as Configurações

1. Acesse a página principal do seu repositório no GitHub.
2. Na barra de navegação superior, clique na aba **"Settings"** (ícone de engrenagem ⚙️).
3. No menu lateral esquerdo, na seção **Code and automation**, clique em **"Branches"**.
4. Ao lado de **Branch protection rules**, clique no botão **"Add branch protection rule"** (ou **"Add rule"**).

---

### 2. Bloqueando a Branch `main`

Preencha os campos e ative as seguintes opções essenciais para a branch `main`:

1. **Branch name pattern**:
   - Digite: `main`

2. Selecione: **`Require a pull request before merging`**
   - Esta opção impede o push direto, exigindo que todo código venha através de um Pull Request.
   - Logo abaixo, selecione: **`Require approvals`**
     - Defina a quantidade mínima de aprovações necessárias antes do merge (ex.: `1` aprovação).

3. Selecione: **`Do not allow bypassing the above settings`**
   - Esta regra garante que **ninguém**, nem mesmo os administradores ou donos do repositório, possa ignorar as proteções e fazer commits diretos.

4. Role até o final da página e clique no botão verde **"Create"** (ou **"Save changes"**). Confirme sua senha/2FA se solicitado.

---

### 3. Bloqueando a Branch `develop`

Agora, aplique **exatamente o mesmo procedimento** para proteger a branch `develop`:

1. Ainda na página de **Branches** (*Settings > Branches*), clique novamente em **"Add branch protection rule"** (ou **"Add rule"**).
2. No campo **Branch name pattern**:
   - Digite: `develop`
3. Ative as mesmas opções:
   - Marque **`Require a pull request before merging`**
   - Marque **`Require approvals`** (ex.: `1` aprovação)
   - Marque **`Do not allow bypassing the above settings`**
4. Role até o final da página e clique em **"Create"**.

> [!TIP]
> **Alternativa com GitHub Rulesets:** Em contas de organizações, você também pode usar o menu *Settings > Rules > Rulesets*. Com ele, é possível criar uma única regra que englobe ambas as branches (`main` e `develop`) ao mesmo tempo no campo *Target branches*.

---

## 🔄 Fluxo de Trabalho Recomendado (Pull Request Flow)

Com as duas branches protegidas, ninguém conseguirá rodar `git push origin main` nem `git push origin develop`. O fluxo diário passa a ser:

1. **Atualizar a `develop` e criar uma branch para sua funcionalidade:**
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/minha-nova-funcionalidade
   ```

2. **Fazer as alterações e commitar:**
   ```bash
   git add .
   git commit -m "feat: implementa nova funcionalidade"
   ```

3. **Enviar a branch para o repositório remoto:**
   ```bash
   git push origin feature/minha-nova-funcionalidade
   ```

4. **Abrir um Pull Request no GitHub:**
   - Acesse o repositório no GitHub.
   - Clique em **"Compare & pull request"**.
   - Defina a branch base como **`develop`** (para receber a nova feature).
   - Descreva as mudanças realizadas e solicite a revisão dos colegas de time.

5. **Revisão e Merge:**
   - Outro membro do time revisa o código e clica em **"Approve"**.
   - Com os requisitos atendidos, o botão **"Merge pull request"** será liberado para integrar o código à `develop`.
   - *(Posteriormente, em momentos de deploy/release, um Pull Request é aberto de `develop` para `main` com as mesmas proteções).*
