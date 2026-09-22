#JavaScript #TypeScript #markdown 

v2 (v3 since late 2023: MDX v3 — bare `{` / `<` in markdown are parse errors; TS-first template `docusaurus.config.ts` / `sidebars.ts`; React 18+)

[[CSS]]

### Components

Codeblock → fence info string `jsx title="src/file.js" showLineNumbers`

Highlight line `// highlight-next-line`, `// highlight-start` / `// highlight-end`

Tab `import Tabs from '@theme/Tabs'` + `import TabItem from '@theme/TabItem'` → `<Tabs><TabItem value="a" label="A">`

Callout `:::note` / `:::tip` / `:::warning` / `:::danger` … `:::`

<br>

`baseUrl: '/docs/'`
![[docs-mainpage.png]]


<br>

### Enable Doc-only

1.  Diable Blog @`docusaurus.config.js`
2.  add at the document index page
    ```markdown
    ---
    slug: /
    ---
    ```
3.  Remove `src/pages/index.js`    
4.  `routeBasePath: '/'`

<br>

### Hide file

Simple way: ignore the file → add `_` before the doc / folder (default exclude of plugin-content-docs)

<br>

### Theme Config

[Theme configuration](https://docusaurus.io/docs/api/themes/configuration)

<br>

### MDX

[MDX and React](https://docusaurus.io/docs/markdown-features/react#exporting-components)

1.  Write in the same mdx
2.  Write in separated js/tsx

<br>

### Multiple docs

[Multiple Docs - Stack Overflow](https://stackoverflow.com/questions/60783595/is-there-a-way-to-have-two-docs-in-docusaurus-2)

1.  Download the plugin: [plugin-content-docs](https://docusaurus.io/docs/api/plugins/@docusaurus/plugin-content-docs)
2.  Add to `docusaurus.config.js` Plugin section

```jsx
[
    '@docusaurus/plugin-content-docs',
    {
      id: 'docs-api',
      path: 'docs-api', // file path
      routeBasePath: 'docs-api', // route path can not start with / 
      sidebarPath: require.resolve('./sidebars.js'),
    }, 
],
```

1.  Add to `docusaurus.config.js` navbar section

```jsx
{
    to: '/docs-api/Intro',    // openpage -> routeBasePath + doc
    label: 'API', // label
    position: 'left',
    activeBaseRegex: `/docs-api/`, // unknow
},
```

<br>

### Versioning

```shell
npm run docusaurus docs:version 1.0.0 # snapshot current docs
```
→ `versioned_docs/` + `versions.json`
`lastVersion` / `onlyIncludeVersions` options @`docusaurus.config.js`

### Swizzling
https://docusaurus.io/docs/swizzling

Ejecting -> can complete replace the original component via React Component, e.g. footer
Wrapping


### i18n

Translation [https://docusaurus.io/docs/cli#docusaurus-write-translations-sitedir](https://docusaurus.io/docs/cli#docusaurus-write-translations-sitedir)

```JavaScript
// docusaurus.config
i18n: {
    defaultLocale: 'zh',
    locales: ['zh', 'en']
},
```

```shell
# create a i18n folder
npm run write-translations

# with specific locale
npm run write-translations -- --locale en
# i18n/en/code.json

```

```shell
npm run start -- --locale en # works, dev server only serves one locale at a time
npm run build -- --locale en # will should locale as /
```

##### locale dropdown
[https://docusaurus.io/docs/i18n/tutorial#theme-configuration](https://docusaurus.io/docs/i18n/tutorial#theme-configuration)

<br>

### Search Plugin
Support Chinese
[https://github.com/easyops-cn/docusaurus-search-local](https://github.com/easyops-cn/docusaurus-search-local)

<br>

### `docusaurus.config.js`

Plugin
Webpack setting
```jsx
configureWebpack()
```

##### ssrTemplate → ejs
```jsx
<% let lang = 'en' %>
<% console.log(lang) %>
```