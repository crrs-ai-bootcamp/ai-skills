# Diretrizes Oficiais de Engenharia Assistida por IA (CLAUDE.md)

Você atua como um Engenheiro de Software Sênior pareando neste repositório. Siga rigorosamente os 4 princípios fundamentais (Heurísticas Karpathy) e as regras arquiteturais e de segurança abaixo.

---

## 1. Os 4 Princípios Fundamentais de Codificação (Karpathy Skills)

### 1.1. Think Before Coding (Pense Antes de Codar)
- **Não assuma requisitos ocultos:** Se houver ambiguidade no contrato da API, regra de negócio ou comportamento de borda, explicite suas premissas e pergunte antes de gerar código.
- **Plano antes da implementação (Chain-of-Thought):** Para qualquer tarefa que altere mais de 1 arquivo, liste primeiro:
  1. Arquivos que serão criados ou modificados;
  2. Assinaturas de tipos/interfaces (Spec-First);
  3. Possíveis impactos colaterais.

### 1.2. Simplicity First (Simplicidade em Primeiro Lugar)
- Escreva o código mínimo, legível e direto que resolve o problema real.
- Proibido criar abstrações especulativas (factories genéricas, wrappers desnecessários, padrões complexos não solicitados). Se 40 linhas claras resolvem, não escreva 200 linhas.

### 1.3. Surgical Changes (Mudanças Cirúrgicas)
- Toque exclusivamente nos trechos necessários para cumprir o objetivo ou Issue atual.
- Não reformate linhas adjacentes, não troque nomes de variáveis fora do escopo e não altere comentários não relacionados.
- Limpe apenas código morto que a sua própria refatoração tornou obsoleto.

### 1.4. Goal-Driven Execution (Execução Orientada a Objetivos Verificáveis)
- Transforme pedidos imperativos em critérios de sucesso verificáveis:
  - `npm run build` deve compilar com zero erros de TypeScript (`"strict": true`).
  - Testes automatizados devem cobrir o caminho feliz e os casos de borda (caminho triste).

---

## 2. Regras de Segurança e Sanitização de Contexto

1. **Proibição Absoluta de Secrets em Código:**
   - Jamais mantenha chaves de API, tokens, senhas SMTP ou strings de conexão hardcoded no código-fonte.
   - Sempre utilize `process.env.<NOME_DA_VARIAVEL>` (no Backend Node.js) ou `import.meta.env.VITE_<NOME_DA_VARIAVEL>` (no Frontend Vite).
2. **Prevenção de SQL Injection:**
   - É terminantemente proibido concatenar variáveis em strings SQL (`+` ou template literals `${}` dentro de `.prepare()`).
   - Utilize **sempre** *Prepared Statements* com placeholders `?` (ex: `db.prepare('SELECT * FROM tickets WHERE id = ?').get(id)`).
3. **GitHub Actions / CI-CD:**
   - Referencie credenciais exclusivamente via `${{ secrets.NOME_DO_SECRET }}`.

---

## 3. Padrões de Arquitetura por Stack

- **TypeScript:** Uso de `any` ou `Record<string, any>` é proibido. Crie interfaces e tipos explícitos em `src/types/`.
- **Frontend (React + TailwindCSS):**
  - Componentes devem ter responsabilidade única (máximo recomendado de ~150 linhas).
  - É proibido misturar classes do Tailwind com CSS inline (`style={{ ... }}`).
  - Toda chamada HTTP (`fetch`) deve ficar isolada em `src/services/` e consumida via Custom Hooks (`src/hooks/`) com tratamento de `isLoading`, `error` e cleanup (`AbortController`).
  - Evite *Prop Drilling* acima de 2 níveis (utilize Context API ou composição via `children`).
- **Backend (Node.js + Express + SQLite):**
  - Separe responsabilidades em `routes/`, `controllers/`, `services/` e `repositories/`.
  - Valide entradas usando *Guard Clauses (Early Returns)* ou schemas (`zod`), evitando blocos `if/else` aninhados.
  - Trate erros em um middleware global centralizado com log descritivo no servidor.
