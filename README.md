# agking-theme

Shopify storefront theme. This file is a source map for finding the Liquid, JavaScript, styles, and theme configuration that make up the storefront.

## Render path

1. Shopify selects a page template from `templates/`.
2. JSON templates compose sections by their `type`; for example, the product template uses `sections/product-information.liquid`.
3. Sections render reusable snippets and expose editor-configurable blocks from `blocks/`.
4. `layout/theme.liquid` wraps the page, renders the header and footer groups, and includes shared drawers and modals.
5. The layout loads global styles through `snippets/stylesheets.liquid` and JavaScript modules through `snippets/scripts.liquid`.

## Source map

| Path | Contents |
| --- | --- |
| `assets/` | Storefront JavaScript modules, CSS, fonts, and icons. `base.css` is the global stylesheet; `package.json` only declares JavaScript module mode. |
| `blocks/` | Reusable theme-editor blocks, including product, collection, blog, and content blocks. |
| `config/settings_schema.json` | Definitions for global theme-editor settings. |
| `config/settings_data.json` | Current theme setting values; Shopify-managed data. |
| `layout/` | Outer document layouts: `theme.liquid` and the password layout. |
| `locales/` | Storefront translations and translation schema files. |
| `sections/` | Page sections and section groups, including header and footer groups. |
| `snippets/` | Shared Liquid fragments, styles, and global asset loaders. |
| `templates/` | Page-to-section compositions for home, product, collection, cart, search, blog, and other routes. |

## Finding the implementation

- To change a page composition, start with its file in `templates/`, then follow each section `type` into `sections/`.
- To change section settings or block support, inspect the section's schema and the matching files in `blocks/`.
- To find shared markup or global asset loading, search `snippets/`; for browser behavior and styling, search `assets/`.
- To change global theme-editor controls, update `config/settings_schema.json`. Treat `settings_data.json` and editor-generated JSON templates as Shopify-managed; changes made in the Theme Editor may rewrite them.
- The global runtime entry points are `layout/theme.liquid`, `snippets/stylesheets.liquid`, and `snippets/scripts.liquid`. Feature scripts are loaded there or imported by other modules.

## Validation

There is no root package manifest or declared test/build script. `assets/package.json` only sets `"type": "module"`. Run Shopify Theme Check or Theme CLI validation when those tools are available in the development environment.
