[https://github.com/yassinedoghri/astro-i18next#-getting-started](https://github.com/yassinedoghri/astro-i18next#-getting-started)

## 🚀 Getting started
### 1. Install
```bash
yarn add astro-i18next


```
### 2. Configure

1. Add astro-i18next to your astro.config.mjs:
```bash
import { defineConfig } from "astro/config";
import astroI18next from "astro-i18next";

export default defineConfig({
  integrations: [astroI18next()],
});
```

2. Configure astro-i18next in your astro-i18next.config.mjs file:
```bash
/** @type {import('astro-i18next').AstroI18nextConfig} */
export default {
  defaultLocale: "en",
  locales: ["en", "fr"],
};
```

3. By default, astro-i18next expects your translations to be organized inside your [astro'spublicDir](https://docs.astro.build/en/reference/configuration-reference/#publicdir), in a locales folder:
```bash
  public
  └── locales  # create this folder to store your translation strings
      ├── en
      |   └── translation.json
      └── fr
          └── translation.json
```
### 3. Start translating


## 高频使用
### npx astro-i18next generate / 生成页面
使用之后，需要`yarn dev`重新启动
```bash
npx astro-i18next generate
```

### Trans component / 文段传递
```bash
---
import { Trans } from "astro-i18next/components";
---

<Trans i18nKey="superCoolKey">
  An <a href="https://astro.build" title="Astro website">astro</a> integration of
  <a href="https://www.i18next.com/" title="i18next website">i18next</a> and utility
  components to help you translate your astro websites!
</Trans>
```
```bash
// fr.json
{
  "superCoolKey": "Une intégration <0>astro</0> d'<1>i18next</1> + quelques composants utilitaires pour vous aider à traduire vos sites astro !"
}
```
#### Trans Props
| Prop name | Type (default) | Description |
| --- | --- | --- |
| i18nKey | ?string (undefined) | Internationalization key to interpolate to. Can contain the namespace by prepending it in the form 'ns:key' (depending on i18next.options.nsSeparator). If omitted, a key is automatically generated using the content of the element. |
| ns | ?string (undefined) | Namespace to use. May also be embedded in i18nKey but not recommended when used in combination with natural language keys. |


### LanguageSelector component / 语言切换
```
---
import { LanguageSelector } from "astro-i18next/components";
---

<LanguageSelector showFlag={true} class="my-select-class" />
<!-- LanguageSelector with custom language naming -->
<LanguageSelector
  showFlag={true}
  languageMapping={{ en: "English" }}
  class="my-select-class"
/>
```
#### anguageSelector Props
| Prop name | Type (default) | Description |
| --- | --- | --- |
| showFlag | ?boolean (false) | Choose to display the language emoji before language name |
| languageMapping | ?object (undefined) | Rewrite language names by setting the locale as key and the wording of your choice as value |

### localizePath function / 内部 URL 
```bash
---
import { localizePath } from "astro-i18next";
import i18next from "i18next";

i18next.changeLanguage("fr");
---

<a href={localizePath("/about")}>...</a>
<!-- renders: <a href="/fr/about">...</a> -->
```
