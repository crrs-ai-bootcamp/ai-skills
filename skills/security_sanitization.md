# Skill: Sanitização de Contexto e Segurança de Dados (`security_sanitization.md`)

## Quando Usar
Use esta skill antes de refatorar arquivos legados com credenciais expostas (Dia 4) e ao gerar pipelines de CI/CD no GitHub Actions (Dia 9).

---

## Protocolo de Sanitização

1. **Verificação da Cerca Virtual (`.aiexclude` / `.cursorignore`):**
   - Confirme que `.env`, `.env.*` e a pasta `secrets/` estão listados no `.aiexclude` e no `.gitignore`.

2. **Substituição por `<PLACEHOLDERS>`:**
   - Ao encontrar constantes com chaves reais ou URLs internas sensíveis no código legado, substitua os valores literais por variáveis de ambiente:
     - Backend Node.js: `process.env.SMTP_CONNECTION_URI`, `process.env.MASTER_API_SECRET`, `process.env.WEBHOOK_NOTIFICATION_URL`.
     - Frontend Vite: `import.meta.env.VITE_API_BASE_URL`, `import.meta.env.VITE_SENTRY_DSN`.
   - Gere um arquivo `.env.example` documentando apenas os nomes das chaves com valores fictícios (`<SUA_CHAVE_AQUI>`).

3. **Auditoria de Injeção SQL (OWASP A03):**
   - Inspecione todas as ocorrências de `db.prepare(` ou `.exec(` no projeto.
   - Qualquer concatenação de string (`+` ou `${}`) com dados vindos de `req.query`, `req.params` ou `req.body` deve ser convertida imediatamente para parâmetros posicionais `?`.

4. **Segurança em Pipelines (`.github/workflows/*.yml`):**
   - Nenhuma chave de API ou token deve aparecer em texto plano no YAML.
   - Utilize estritamente `${{ secrets.<NOME_DO_SECRET> }}` e defina permissões mínimas (`permissions: contents: read`).
