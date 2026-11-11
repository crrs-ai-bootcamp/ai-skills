# Skill: Geração e Refatoração de CRUD Backend (`generate_crud.md`)

## Quando Usar
Use esta skill para quebrar monolitos Express/SQLite ou criar um novo recurso RESTful completo (ex.: **Comentários do Ticket** no Dia 8) seguindo Arquitetura em Camadas e segurança contra SQL Injection.

---

## Passo a Passo Obrigatório (Workflow do Agente)

### Etapa 1 — Spec-First (Contratos e Schema)
1. Defina as interfaces e DTOs em `src/types/<resource>.ts` (sem usar `any`).
2. Defina a criação da tabela SQLite em `src/config/database.ts` (ou `src/database/connection.ts`) com chaves estrangeiras e `created_at` padrão.

### Etapa 2 — Camada de Acesso a Dados (`src/repositories/<resource>Repository.ts`)
1. Implemente os métodos de acesso ao `better-sqlite3`.
2. **REGRA CRÍTICA:** Todas as queries (`SELECT`, `INSERT`, `UPDATE`, `DELETE`) devem usar **exclusivamente Prepared Statements (`?`)**. Nenhuma variável pode ser concatenada na string SQL.

### Etapa 3 — Camada de Regra de Negócio (`src/services/<resource>Service.ts`)
1. Valide os dados de entrada usando **Guard Clauses (Early Returns)** no topo do método (máximo 1 nível de indentação `if`).
2. Lance uma instância de `AppError(message, statusCode)` para erros de domínio (`400 Bad Request`, `404 Not Found`, `409 Conflict`).

### Etapa 4 — Camada HTTP (`src/controllers/` e `src/routes/`)
1. O Controller apenas extrai `req.params`, `req.query` e `req.body`, chama o Service e retorna o `res.status(...).json(...)` (`200 OK`, `201 Created` ou `204 No Content`).
2. Erros são repassados para o middleware global de erro (`next(err)`).

### Etapa 5 — Verificação (Goal-Driven)
1. Atualize o arquivo `requests.http` com exemplos das novas rotas.
2. Crie ou atualize os testes unitários/integração do Service cobrindo o caminho feliz e pelo menos 2 casos de erro (`400` e `404`).
3. Execute `npm run build` e a suíte de testes antes de concluir.
