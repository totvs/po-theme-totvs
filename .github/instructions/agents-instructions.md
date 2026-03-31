# PO Theme TOTVS - Instruções para AI Coding Agents

## Visão Geral do Projeto

O `@totvs/po-theme` é o tema padrão da TOTVS para aplicações construídas com o framework PO UI. Estende e customiza o `@po-ui/style` com branding TOTVS (cores, tipografia, espaçamentos).

> **ATENÇÃO**: Este repositório está em processo de descontinuação. Suporte até v23.x.x. Novas funcionalidades são desenvolvidas em repositório privado interno.

## Idioma

- **Documentação**: Português formal e impessoal
- **Código fonte**: Inglês (nomes de variáveis CSS, classes, funções)

## Arquivo Principal — `src/po-theme-custom.css`

Este arquivo contém TODAS as custom properties do tema (1559+ linhas de CSS). É a única fonte de verdade para a identidade visual TOTVS.

### Sincronização com po-ui/po-style (CRÍTICO)

O arquivo `src/po-theme-custom.css` é um **espelho** do arquivo `src/css/themes/po-theme-default.css` do repositório `po-ui/po-style`. Alterações feitas em um DEVEM ser replicadas no outro. Ignorar esta regra causa divergência visual entre os temas.

## Hierarquia de Tokens CSS

```
Brand Tokens (--color-brand-01-*)
  → Action Colors (--color-action-*)
    → Feedback Colors (--color-feedback-positive-*, --color-feedback-negative-*, ...)
      → Component Variables (po-button, po-input, po-table, ...)
```

### Categorias de Tokens

1. **Brand Colors**: `--color-brand-01-lightest` até `--color-brand-01-darkest`
2. **Action Colors**: `--color-action-default`, `--color-action-hover`, `--color-action-pressed`, `--color-action-disabled`, `--color-action-focus`
3. **Neutral Colors**: `--color-neutral-light-*`, `--color-neutral-mid-*`, `--color-neutral-dark-*`
4. **Feedback Colors**: `--color-feedback-positive-*`, `--color-feedback-negative-*`, `--color-feedback-warning-*`, `--color-feedback-info-*`
5. **Tipografia**: `--font-family-theme`, `--font-family-theme-bold`, `--font-family-theme-extra-light`
6. **Density**: `--po-density-header-padding`, `--po-density-content-padding`, `--po-density-gap-spacing`
7. **Categorical**: `--color-01` até `--color-12` (para visualização de dados)

## Regras de Tokens CSS (OBRIGATÓRIO)

### PROIBIDO
- **Valores hard-coded de cor**: NÃO use `#hex`, `rgb()`, `rgba()`, `hsl()` diretamente. Use SEMPRE variáveis CSS existentes.
- **Valores hard-coded de espaçamento**: NÃO use `8px`, `16px`, `1rem` diretamente. Use tokens de densidade.
- **Valores hard-coded de tipografia**: NÃO use `font-family: 'Arial'`, `font-size: 14px`. Use tokens: `var(--font-family-theme)`.
- **Modificação unilateral**: NÃO modifique `po-theme-custom.css` sem replicar no `po-ui/po-style`.
- **Novas features**: NÃO publique novas funcionalidades — apenas correções e manutenção.

### OBRIGATÓRIO
- Todo valor visual DEVE referenciar uma CSS Variable definida no `:root` do tema.
- Componentes DEVEM cobrir os estados: Enable, Disable, Static, Hover, Focus, Active, Loading.
- Ao criar novos tokens, siga a nomenclatura: `--{categoria}-{propriedade}-{variante}`.

## Estrutura de Pastas

```
po-theme-totvs/
├── .github/
│   └── workflows/          # CI/CD publishing workflows
├── src/
│   ├── assets/fonts/       # Fontes NunitoSans (Regular, Bold, ExtraLight)
│   ├── index.css           # Entry point CSS (importa po-theme-custom.css)
│   └── po-theme-custom.css # Definição completa do tema TOTVS
├── package.json            # Configuração do pacote e scripts de build
└── README.md               # Documentação de instalação e uso
```

## Ordem de Carga CSS no angular.json (CRÍTICO)

```json
"styles": [
  "node_modules/@totvs/po-theme/css/po-theme-default-variables.min.css",
  "node_modules/@totvs/po-theme/css/po-theme-default.min.css",
  "node_modules/@po-ui/style/css/po-theme-core.min.css"
]
```

A ordem é OBRIGATÓRIA: **variables → theme → core**. Inverter causa falha na cascata CSS e tokens não serão resolvidos corretamente.

## Comandos de Desenvolvimento

```bash
# Instalar dependências
npm install

# Compilar tema (usa @po-ui/theme-cli)
npm run build

# Criar tarball para teste local
npm run pack

# Publicar em registry local (localhost:4873)
npm run publish:local
```

## Sistema de Fontes

O tema usa a família tipográfica **NunitoSans**:
- `NunitoSans-Regular.ttf` (400)
- `NunitoSans-Bold.ttf` (700)
- `NunitoSans-ExtraLight.ttf` (200)

Declaradas via `@font-face` no `po-theme-custom.css` e referenciadas por:
- `--font-family-theme`
- `--font-family-theme-bold`
- `--font-family-theme-extra-light`

## Integração MCP — Ferramentas de Design

Para conectar agentes de IA às especificações de design do Animalia DS no Figma, configure o MCP do Figma no seu ambiente de desenvolvimento.

**Configuração sugerida para `mcp.json`:**
```json
{
  "mcpServers": {
    "figma": {
      "command": "npx",
      "args": ["-y", "figma-developer-mcp", "--stdio"],
      "env": {
        "FIGMA_API_KEY": "<sua-chave-api-figma>"
      }
    }
  }
}
```

> **Nota:** A chave da API do Figma deve ser configurada como variável de ambiente, nunca embutida no código.

## Padrões de Commit (Angular conventional commits)

```
<type>(scope): <descrição curta>
```

**Types**: `feat`, `fix`, `docs`, `refactor`, `perf`, `test`, `build`  
**Scope**: Nome do componente **sem** o prefixo `po-` (ex: `feat(button)`, NÃO `feat(po-button)`)

## CI/CD — Canais de Publicação

| Canal | Trigger | npm Tag |
|-------|---------|---------|
| Latest | Manual (workflow_dispatch) | `latest` |
| Next | Manual (workflow_dispatch) | `next` |
| Beta | Push para branch `beta` | `beta` |
| Angular 19 LTS | Push para branch `19.x.x` | `v19-lts` |
| Angular 20 | Push para branch `20.x.x` | `v20-ng` |

## Migração

Para dúvidas sobre migração, abra uma issue neste repositório.
