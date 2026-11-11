# Skill: Diretrizes de Componentes React e Hooks (`react_component_guidelines.md`)

## Quando Usar
Use esta skill ao refatorar um *God Component* (`App.tsx`) ou ao construir uma nova funcionalidade de interface no `techdesk-web-challenge` (ex.: **Módulo de Comentários do Chamado** no Dia 8).

---

## Regras Estritas de Implementação

1. **Limite de Tamanho e Coesão:**
   - Nenhum componente em `src/components/` deve ultrapassar **150 linhas**.
   - Separe componentes de apresentação (UI) da lógica de estado/rede.

2. **Tipagem 100% Estrita (`src/types/`):**
   - Proibido usar `any` ou `Record<string, any>`.
   - Tipar todas as Props com `interface <ComponentName>Props` e todos os eventos (`React.FormEvent<HTMLFormElement>`, `React.ChangeEvent<HTMLInputElement>`).

3. **Estilização Pura com TailwindCSS:**
   - Proibido usar a prop `style={{ ... }}`.
   - Use classes utilitárias do Tailwind de forma consistente para espaçamento, cores de status/prioridade, tipografia e responsividade.

4. **Isolamento de Efeitos Colaterais (`src/services/` + `src/hooks/`):**
   - Nenhuma chamada `fetch` deve ficar solta diretamente em componentes visuais.
   - Crie funções tipadas em `src/services/api.ts` utilizando `import.meta.env.VITE_API_URL`.
   - Consuma os serviços através de Custom Hooks (`useTickets`, `useTicketComments`) que exponham `{ data, isLoading, error, refetch }` e utilizem `AbortController` no cleanup do `useEffect`.
   - **Atenção às dependências do `useEffect`:** Use identificadores primitivos (ex.: `[ticketId]`) em vez de referências de objetos inteiros (`[selectedTicket]`) para evitar re-fetches acidentais ao atualizar propriedades locais.

5. **Zero Prop Drilling (> 2 níveis):**
   - Utilize `TicketContext` (`src/context/TicketContext.tsx`) ou composição (`children`) para compartilhar estado e ações com modais e subcomponentes.
