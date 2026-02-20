# ⚠️ Descontinuação do Repositório

Este repositório está em processo de descontinuação.

Esses recursos passam a ser gerenciados exclusivamente em um projeto interno (repositório privado). Portanto, não haverá mais publicação de inovações e novas funcionalidades.

Para dúvidas ou orientações sobre migração, abra uma issue neste repositório.

---

# PO Theme - Totvs Default Theme

Tema padrão da Totvs para aplicações desenvolvidas com [PO UI](http://po-ui.io).

:warning: __Uso exclusivo dos produtos TOTVS e Clientes.__

### Como usar o tema

O **PO UI** possui o seu próprio tema, mas disponibilizamos um tema com os padrões da TOTVS.

Para utilizá-lo, instale o pacote `@totvs/po-theme` conforme abaixo:

```
npm i @totvs/po-theme
```

Em seguida, atualize o arquivo `angular.json` para utilizar o tema.

```json
"styles": [
  "node_modules/@totvs/po-theme/css/po-theme-default-variables.min.css",
  "node_modules/@totvs/po-theme/css/po-theme-default.min.css",
  "node_modules/@po-ui/style/css/po-theme-core.min.css",
]
```

> Leia mais sobre [como criar seu próprio tema customizado do PO UI][create-theme-customization].

[create-theme-customization]: https://po-ui.io/guides/create-theme-customization
