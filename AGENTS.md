# AGENTS.md — PO Theme TOTVS

> **ATENÇÃO**: Este repositório está em processo de descontinuação.
> Suporte até v23.x.x. Após essa versão, o pacote deixará de ser mantido.
> Novas funcionalidades são desenvolvidas em repositório privado interno.

## Instruções Detalhadas

Consulte o arquivo principal de instruções:
- **[.github/instructions/agents-instructions.md](.github/instructions/agents-instructions.md)** — Instruções completas para desenvolvimento

## Visão Geral

Tema padrão da TOTVS para aplicações PO UI. Pacote: `@totvs/po-theme`.
Estende o `@po-ui/style` com branding TOTVS (cores, tipografia, espaçamentos).

## Arquivo Principal

`src/po-theme-custom.css` — Contém TODAS as custom properties do tema (1559+ linhas).
Este arquivo é um **espelho** de `src/css/themes/po-theme-default.css` do repositório `po-ui/po-style`.
Alterações DEVEM ser sincronizadas entre ambos os repositórios.

## Hierarquia de Tokens CSS

```
Brand Tokens (--color-brand-01-*)
  → Action Colors (--color-action-*)
    → Component Variables (po-button, po-input, ...)
```

### PROIBIDO
- **NÃO** adicione valores hard-coded (hex, rgb). Use SEMPRE variáveis CSS existentes.
- **NÃO** modifique `po-theme-custom.css` sem replicar a alteração no `po-ui/po-style`.
- **NÃO** publique novas features — apenas correções e manutenção.

## Estrutura

```
src/
├── assets/
│   └── fonts/              # Fontes NunitoSans (Regular, Bold, ExtraLight)
├── index.css               # Entry point CSS (importa po-theme-custom.css)
└── po-theme-custom.css     # Definição completa do tema TOTVS
```

## Ordem de Carga CSS no angular.json (CRÍTICO)

```json
"styles": [
  "node_modules/@totvs/po-theme/css/po-theme-default-variables.min.css",
  "node_modules/@totvs/po-theme/css/po-theme-default.min.css",
  "node_modules/@po-ui/style/css/po-theme-core.min.css"
]
```

A ordem é OBRIGATÓRIA: variables → theme → core. Inverter causa falha na cascata CSS.

## Comandos Essenciais

```bash
npm install                    # Instalar dependências
npm run build                  # Compilar tema (usa @po-ui/theme-cli)
npm run pack                   # Criar tarball
npm run publish:local          # Publicar em localhost:4873
```

## Padrões de Commit (Angular conventional commits)

```
<type>(scope): <descrição curta>
```

**Types**: `feat`, `fix`, `docs`, `refactor`, `perf`, `test`, `build`

## Migração

Para dúvidas sobre migração, abra uma issue neste repositório.
