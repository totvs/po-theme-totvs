# Code Review — AI Readiness (po-theme-totvs)

**Data:** 2026-03-25
**Repositório:** totvs/po-theme-totvs
**PR:** [#545](https://github.com/totvs/po-theme-totvs/pull/545)

---

## Sumário Executivo

| Critério | Status |
|----------|--------|
| Hierarquia de Tokens CSS | Implementado |
| Proibição de valores hard-coded | Implementado |
| Sincronização com po-style | Implementado |
| Ordem de carga CSS | Implementado |
| Engenharia e Qualidade | Implementado |

## Critérios de Aceite Verificados

### 1. Tokens CSS

- **Hierarquia documentada**: Brand Tokens → Action Colors → Feedback Colors → Component Variables
- **Categorias de tokens**: Brand, Action, Neutral, Feedback, Typography, Density, Categorical — todas documentadas
- **Proibição de valores hard-coded**: Explícita — NÃO usar `#hex`, `rgb()`, espaçamentos literais, tipografia literal
- **Estados obrigatórios**: Enable, Disable, Static, Hover, Focus, Active, Loading

### 2. Sincronização Cross-Repo

- **Espelhamento documentado**: `src/po-theme-custom.css` ↔ `src/css/themes/po-theme-default.css` do `po-ui/po-style`
- **Regra explícita**: Alterações DEVEM ser sincronizadas entre ambos os repositórios
- **Proibição de modificação unilateral**: NÃO modificar sem replicar no po-style

### 3. Ordem de Carga CSS

- **Ordem obrigatória documentada**: variables → theme → core
- **Exemplo de `angular.json`** incluído com os três arquivos na ordem correta

### 4. Engenharia e Qualidade

- **Conventional Commits**: Padrão `<type>(scope): <descrição curta>` documentado
- **CI/CD**: Canais de publicação documentados (latest, next, beta, v19-lts, v20-ng)
- **Aviso de descontinuação**: Explícito — suporte até v23.x.x

## Arquivos de AI Readiness

| Arquivo | Propósito |
|---------|-----------|
| `AGENTS.md` | Ponto de entrada com visão geral, tokens e regras |
| `.github/instructions/agents-instructions.md` | Instruções completas de desenvolvimento |
| `mcp.json` | Configuração de MCP servers (Figma) |
