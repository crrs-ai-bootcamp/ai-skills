# Skill: Revisão de Pull Request por IA (`pr_code_review.md`)

## Quando Usar
Use esta skill no Dia 9 e Dia 10 para auditar um Pull Request ou branch antes da aprovação final, atuando como um Tech Lead rigoroso.

---

## Checklist de Auditoria (Output Estruturado)

Analise o `git diff` da branch em relação à `master`/`main` e gere um relatório objetivo avaliando os 5 critérios abaixo (aprovando ✅ ou bloqueando ❌ cada item com citação de `arquivo:linha`):

1. **Tipagem e Contratos TypeScript:**
   - Existe algum `: any` ou `Record<string, any>` remanescente?
   - `tsconfig.json` está com `"strict": true`?
2. **Arquitetura e Simplicidade (Karpathy & Clean Code):**
   - Responsabilidades foram separadas adequadamente sem overengineering?
   - No Frontend: algum componente passou de 150 linhas ou manteve `style={{ ... }}` inline?
   - No Backend: restou lógica de negócio/SQL dentro das rotas ou `if`s aninhados profundos?
3. **Segurança (OWASP & Secrets):**
   - Todas as queries SQL usam Prepared Statements (`?`)?
   - Alguma credencial ou URL sensível ficou hardcoded fora de variáveis de ambiente?
4. **Qualidade dos Testes Automatizados:**
   - Os testes testam o comportamento real (incluindo casos de borda/erro e persistência) ou apenas testam mocks estáticos (falso positivo)?
5. **DX e CI/CD:**
   - Git hooks (`Husky` / `lint-staged`) e workflow do GitHub Actions (`.github/workflows/ci.yml`) estão configurados e íntegros?
