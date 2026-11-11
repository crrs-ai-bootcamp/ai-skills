# 🚀 Guia do Dia Zero — Preparação de Ambiente (Pré-Bootcamp)

Bem-vindo ao **Bootcamp de Engenharia Assistida por IA (TechDesk)**!
Como nossas sessões diárias têm **1 hora de duração (15 min de teoria + 45 min de prática mão na massa)**, precisamos que o seu ambiente local esteja **100% configurado antes do Dia 1**.

Reserve **15 minutos** para concluir os 4 passos abaixo.

---

## Passo 1: Criar seu Repositório Privado a partir do Template Oficial

Cada participante trabalhará em seu próprio repositório **Privado** (isolado) usando os nossos Templates oficiais:

1. Acesse o link correspondente à sua trilha:
   - **Trilha Frontend:** https://github.com/crrs-ai-bootcamp/techdesk-web-challenge
   - **Trilha Backend:** https://github.com/crrs-ai-bootcamp/techdesk-api-challenge
   - **Trilha QA:** https://github.com/crrs-ai-bootcamp/techdesk-qa-challenge
2. Clique no botão verde **"Use this template"** $\rightarrow$ **"Create a new repository"** (NÃO clique em *Fork*).
3. Escolha a sua conta pessoal do GitHub como *Owner*, mantenha o nome do repositório e selecione obrigatoriamente a visibilidade **Private (Privado)**.
4. No seu repositório recém-criado, vá em **Settings** $\rightarrow$ **Collaborators** $\rightarrow$ **Add people** e adicione o instrutor (**`caiorrs`**) com permissão de **Write/Admin**.
   > *Por que isso é obrigatório?* O instrutor rodará uma automação que criará as **Issues do projeto** dentro do seu repositório privado para que a sua IA possa lê-las via protocolo **MCP**!
5. Envie o link do seu repositório privado para o instrutor.

---

## Passo 2: Clonar os Repositórios Localmente

Crie uma pasta dedicada para o bootcamp e clone o seu repositório privado **e** este repositório de skills (`ai-skills`) lado a lado:

```bash
mkdir -p ~/bootcamp-ia && cd ~/bootcamp-ia

# 1. Clone o repositório corporativo de Skills e Rules
git clone https://github.com/crrs-ai-bootcamp/ai-skills.git

# 2. Clone o SEU repositório privado criado no Passo 1
git clone https://github.com/<SEU_USUARIO>/<SEU_REPO_TECHDESK>.git

# 3. Instale as dependências e teste se o projeto sobe
cd <SEU_REPO_TECHDESK>
npm install # (No caso de QA: npm run install:all)
```

---

## Passo 3: Configurar sua Chave de API do OpenRouter

Você receberá do instrutor uma chave individual do **OpenRouter** (`sk-or-v1-...`) com limite pré-configurado para os 10 dias.

- **Regra de Segurança (Prévia do Dia 1):** Jamais cole sua chave de API dentro de arquivos do projeto ou no chat da IA! Configure-a nas variáveis de ambiente do seu terminal (`~/.zshrc` ou `~/.bashrc`) ou nas configurações globais da sua ferramenta de CLI/IDE:

```bash
export OPENROUTER_API_KEY="sk-or-v1-sua-chave-aqui"
```

### Modelos Recomendados no OpenRouter durante o Bootcamp:
- **Uso Diário (Dias 1 a 7 — Rápido e Econômico):** `deepseek/deepseek-chat` (DeepSeek V3) ou `google/gemini-2.5-flash`
- **Agentes Multi-Arquivo e MCP (Dia 8 e Dia 10):** `anthropic/claude-3.5-haiku` ou `anthropic/claude-3.7-sonnet`

---

## Passo 4: Configurar o GitHub MCP Server (Model Context Protocol)

Nos Dias 2 e 8, nossa IA não receberá requisitos por "copia e cola": ela lerá diretamente as **Issues** do seu repositório no GitHub e abrirá **Pull Requests** usando o **GitHub MCP**.

1. No GitHub, acesse **Settings** $\rightarrow$ **Developer settings** $\rightarrow$ **Personal access tokens** $\rightarrow$ **Tokens (classic)** (ou Fine-grained) e gere um token com escopo `repo`.
2. Na configuração de MCP da sua ferramenta de CLI/IDE (ex: `mcp.json`, Claude Code, OpenCode, Cursor ou Cline), adicione o servidor do GitHub:

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<SEU_GITHUB_PAT_AQUI>"
      }
    }
  }
}
```

---

## ✅ Checklist Final do Dia Zero (Estou pronto para o Dia 1?)

- [ ] Criei meu repositório **Privado** usando *"Use this template"* (não fiz Fork público).
- [ ] Adicionei o usuário **`caiorrs`** como colaborador do meu repositório privado e enviei o link para ele.
- [ ] Rodei `npm install` e consegui subir o projeto localmente (`npm run dev`).
- [ ] Minha chave do OpenRouter está funcionando no meu cliente de IA (IDE/CLI).
- [ ] Meu GitHub MCP está configurado e autenticado.
