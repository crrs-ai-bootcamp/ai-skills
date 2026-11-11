# 🧭 Mapa de Estudos Contínuos Pós-Bootcamp (8 Semanas)

Parabéns por concluir os **10 dias intensivos do Bootcamp de Engenharia Assistida por IA**!
Durante o treinamento, saímos do *"Copy-Paste no Browser"* (Nível 1) para a **Engenharia Assistida por Contexto, Skills e Agentes via MCP** (Nível 3).

Este guia define o seu **caminho de evolução autônoma nas próximas 8 semanas** e prepara você para os nossos encontros quinzenais de **Prompt Show & Tell**.

---

## 🎤 Como Funcionam os Encontros Quinzenais ("Prompt Show & Tell")

A cada 15 dias faremos uma sessão rápida de 30–45 minutos focada em **prática real**:
1. **O Melhor Prompt / Skill da Quinzena (5 min):** Um Dev ou QA compartilha na tela uma tarefa complexa que resolveu com IA, mostrando o contexto/skill utilizado. As melhores soluções viram PRs oficiais neste repositório (`ai-skills`).
2. **A Maior Alucinação da Quinzena (5 min):** Um Dev ou QA mostra um caso onde a IA errou feio (inventou biblioteca, quebrou regra de negócio, entrou em loop) e **como ajustou o contexto/prompt** para resolver.

---

## 📚 Trilha de Estudo Autônomo (Semana a Semana)

### Semanas 1 e 2 — Psicologia de LLMs, Economia de Tokens e Modelos de Raciocínio
- **O que estudar:**
  - **Modelos Fast/Chat vs. Modelos Reasoning (Thinking):** Quando usar modelos rápidos (DeepSeek V3, Gemini Flash, Claude Haiku) vs. modelos de raciocínio profundo (DeepSeek R1, Claude Extended Thinking, OpenAI o3-mini).
  - **Degradação de Janela de Contexto ("Lost in the Middle"):** Por que conversas longas degradam a precisão do código gerado e quando usar `/compact` ou iniciar uma nova sessão limpa após fechar o plano (*Spec-First*).
- **Leituras Obrigatórias:**
  - [Andrej Karpathy Skills (`multica-ai/andrej-karpathy-skills`)](https://github.com/multica-ai/andrej-karpathy-skills) — Releia as 4 heurísticas (*Think Before Coding, Simplicity First, Surgical Changes, Goal-Driven Execution*).
  - [Prompting Guide — Advanced Techniques](https://www.promptingguide.ai/techniques) (*ReAct*, *Self-Consistency*, *Tree of Thoughts*).

---

### Semanas 3 e 4 — Domínio do Protocolo MCP e Ecossistema de Skills
- **O que estudar:**
  - Arquitetura do **Model Context Protocol (MCP)**: como funcionam *Tools*, *Resources* e *Prompts* locais e remotos.
  - Servidores MCP que aceleram o desenvolvimento diário:
    - **Atlassian / Jira & Confluence MCP:** Ler histórias de usuário e critérios de aceite reais sem sair do terminal.
    - **Playwright / Browser DevTools MCP:** Permitir que o agente inspecione o DOM, console logs e requisições de rede ao vivo no navegador.
    - **Database MCP (SQLite / Postgres):** Permitir que a IA consulte o schema real do banco antes de escrever queries ou migrations.
- **Leituras e Repositórios de Referência:**
  - [AgentSkills.io](https://agentskills.io/home) — Padrão aberto para criação de skills portáveis entre agentes.
  - [Skills.sh](https://www.skills.sh/) — Diretório de skills de linha de comando para agentes.
  - [AI Hero (`aihero.dev/skills`)](https://www.aihero.dev/skills) — Padrões avançados de orquestração de agentes e TypeScript.

---

### Semanas 5 e 6 — Aprofundamento por Especialidade (Front, Back e QA)

#### 🎨 Trilha Frontend
- **Tópicos para explorar:**
  - Auditoria automatizada de **Acessibilidade (WCAG / ARIA)** e **Performance de Renderização React** assistida por IA.
  - Geração de **Design Systems / Tokens** e documentação viva (Storybook + MSW) guiada por contratos TypeScript.
  - Fluxo *Screenshot/Figma-to-Code* combinando visão multimodal com as regras do `react_component_guidelines.md`.

#### ⚙️ Trilha Backend
- **Tópicos para explorar:**
  - Aplicação de **Clean Architecture, DDD (Domain-Driven Design) e Ports & Adapters** com IA sem cair em overengineering ([Referência: Formação IA — Rodrigo Branas](https://www.branas.io/formacoes/inteligencia-artificial)).
  - Uso de IA para análise de planos de execução de queries (`EXPLAIN QUERY PLAN`), criação de índices e detecção de *N+1 queries*.
  - Geração de scripts de **Teste de Carga e Stress** (k6 / Artillery) a partir da especificação OpenAPI.

#### 🧪 Trilha QA & Automação
- **Tópicos para explorar:**
  - **Testes Mutantes (Mutation Testing — ex: StrykerJS):** Como avaliar se os testes gerados pela IA realmente falham quando uma regra de negócio é alterada no código.
  - **Contract Testing & Schema Validation:** Garantir automaticamente que o Frontend e o Backend nunca quebrem contratos JSON entre sprints.
  - **E2E Auto-Healing e Visual Regression:** Estratégias para manter suítes Playwright rápidas, determinísticas (zero flakiness) e integradas ao CI.

---

### Semanas 7 e 8 — Automação de Esteira (CI/CD), Custom CLI Commands e Multi-Agentes
- **O que estudar:**
  - Como criar **Scripts e Hooks de Diagnóstico Automatizado** (ex.: ler o log de erro de um job que falhou no GitHub Actions via `gh run view --log-failed` e já injetar na CLI da IA com o diff do último commit).
  - Orquestração de **Subagentes / Swarms** (um agente focado em implementar a feature e um segundo agente com contexto limpo atuando exclusivamente como revisor hostil de segurança e qualidade antes de abrir o PR).
  - Contribuição contínua para o repositório corporativo `ai-skills`.
