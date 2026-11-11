# 🧠 Repositório Corporativo de AI Skills & Rules (`ai-skills`)

Biblioteca central de **Regras de Sistema (`CLAUDE.md`, `.cursorrules`, `.aiexclude`)** e **Skills Reutilizáveis** para Engenharia Assistida por IA no ecossistema **TechDesk**.

---

## 📂 Estrutura do Repositório

```text
ai-skills/
├── 00-onboarding-dia-zero.md         # Guia obrigatório de preparação antes do Dia 1 (Template, OpenRouter, MCP)
├── 01-roadmap-pos-bootcamp.md        # Trilha de 8 semanas de estudos autônomos + Prompt Show & Tell
├── rules/
│   ├── CLAUDE.md                     # Regras base (Heurísticas Karpathy + Clean Arch + Segurança)
│   ├── .cursorrules                  # Âncoras de contexto para Cursor / IDEs compatíveis
│   └── .aiexclude                    # Cerca Virtual padrão para bloquear leitura de secrets/.env
└── skills/
    ├── generate_crud.md              # Skill Backend: Criação de CRUD em 3 camadas + SQLite seguro
    ├── react_component_guidelines.md # Skill Frontend: Componentes modulares, Hooks e Tailwind puro
    ├── qa_playwright_spec.md         # Skill QA: BDD/Gherkin, Page Object Model e Testes de API/E2E
    ├── security_sanitization.md      # Skill Segurança: Placeholders, auditoria SQLi e CI/CD seguro
    └── pr_code_review.md             # Skill Tech Lead: Checklist de revisão automatizada de PRs
```

---

## 🚀 Como Utilizar no Dia a Dia (IDE e Agentes de CLI)

### 1. Configurando a "Cerca Virtual" e Regras Base (Dia 1)
Copie os arquivos da pasta `rules/` para a raiz do seu projeto:
```bash
cp ../ai-skills/rules/.aiexclude ./.aiexclude
cp ../ai-skills/rules/.aiexclude ./.cursorignore
cp ../ai-skills/rules/CLAUDE.md ./CLAUDE.md
cp ../ai-skills/rules/.cursorrules ./.cursorrules
```

### 2. Invocando Skills com Agentes de Terminal / IDE (Dia 8)
Ao executar tarefas complexas ou criar novas features (como a **Issue #3 — Comentários no Chamado**), referencie a skill correspondente junto com o **GitHub MCP**:

- **No Backend (`techdesk-api-challenge`):**
  > *"Use o MCP para ler a Issue #3 do repositório. Em seguida, aplique a skill `@ai-skills/skills/generate_crud.md` para implementar o CRUD de Comentários nos Tickets. Rode os testes, faça commit e abra um Pull Request fechando a Issue #3."*

- **No Frontend (`techdesk-web-challenge`):**
  > *"Use o MCP para ler a Issue #3 do repositório. Aplique a skill `@ai-skills/skills/react_component_guidelines.md` para construir o módulo de Comentários no Chamado com estados de loading/error e tipagem estrita."*

- **No QA (`techdesk-qa-challenge`):**
  > *"Use o MCP para ler a Issue #3 do repositório. Aplique a skill `@ai-skills/skills/qa_playwright_spec.md` para criar os cenários BDD, Page Objects e testes automatizados."*
