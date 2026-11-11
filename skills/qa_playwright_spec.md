# Skill: Automação de QA — BDD, Page Object Model e Testes de API (`qa_playwright_spec.md`)

## Quando Usar
Use esta skill no repositório `techdesk-qa-challenge` para planejar cenários de teste (Gherkin), escrever testes de integração de API (Vitest/Supertest) e automatizar fluxos E2E (Playwright) capazes de detectar falsos positivos de interface e falhas de validação no backend.

---

## Regras de Ouro de Qualidade

1. **Seletores Resilientes e Page Object Model (POM):**
   - Priorize seletores semânticos ou atributos `data-testid` (`page.getByTestId(...)`).
   - Proibido usar seletores CSS frágeis encadeados (`div > table > tr:nth-child(2)`).
   - Encapsule os seletores e ações da página em classes Page Object (ex.: `TicketsPage.ts`).

2. **Zero `sleep()` Hardcoded:**
   - Proibido usar `waitForTimeout(5000)` ou `setTimeout`.
   - Utilize sempre Web-First Assertions do Playwright (`await expect(locator).toBeVisible()`, `await expect(locator).toHaveText(...)`).

3. **Anti Falso-Positivo de UI (Verificação de Persistência):**
   - **REGRA CRÍTICA:** Sempre que um teste E2E executar uma ação de mutação na interface (criar chamado, fechar chamado, excluir chamado), o teste **DEVE**:
     1. Validar a resposta da rede (`page.waitForResponse`) **OU**
     2. Executar `await page.reload()` e validar que o novo estado **permaneceu salvo no banco de dados** após o recarregamento da página!

4. **Cobertura de Caminho Triste e Limites (Agente do Caos):**
   - Todo endpoint de criação/atualização (`POST`, `PUT`, `PATCH`) deve ter testes cobrindo:
     - Campos vazios (`""`);
     - Campos contendo apenas espaços em branco (`"   "`);
     - Ausência de campos obrigatórios (`undefined`).
   - Todo endpoint de listagem (`GET /tickets`) deve ter testes que validem se os parâmetros `limit`, `page` e `search` realmente filtram e limitam a quantidade de itens retornados em `data`.
