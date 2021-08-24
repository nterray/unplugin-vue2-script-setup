# unplugin-vue2-script-setup

[![NPM version](https://img.shields.io/npm/v/unplugin-vue2-script-setup?color=a1b858&label=)](https://www.npmjs.com/package/unplugin-vue2-script-setup)

Bring [`<script setup>`](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to Vue 2.

## Install

```bash
npm i -D unplugin-vue2-script-setup
npm i @vue/composition-api
```

Install [`@vue/composition-api`](https://github.com/vuejs/composition-api) in your App's entry (it enables the `setup()` hook):

```ts
import Vue from 'vue'
import VueCompositionAPI from '@vue/composition-api'

Vue.use(VueCompositionAPI)
```

<details>
<summary>Vite</summary><br>

```ts
// vite.config.ts
import { defineConfig } from 'vite'
import { createVuePlugin as Vue2 } from 'vite-plugin-vue2'
import ScriptSetup from 'unplugin-vue2-script-setup/vite'

export default defineConfig({
  plugins: [
    Vue2(),
    ScriptSetup(),
  ],
})
```

Example: [`playground/`](./playground/)

<br></details>

<details>
<summary>Nuxt</summary><br>

```bash
npm i @nuxtjs/composition-api
```

```ts
// nuxt.config.js
export default {
  buildModules: [
    '@nuxtjs/composition-api/module',
    'unplugin-vue2-script-setup/nuxt',
  ],
}
```

> This module works for both Nuxt 2 and [Nuxt Vite](https://github.com/nuxt/vite)

Example: [`examples/nuxt`](./examples/nuxt)

###### TypeScript

To use TypeScript with Nuxt, install the [`@nuxtjs/typescript-module`](https://typescript.nuxtjs.org/) but disable the type check:

```bash
npm i -D @nuxt/typescript-build vue-tsc
```

```ts
// nuxt.config.js
export default {
  buildModules: [
    ['@nuxt/typescript-build', { typeCheck: false }],
    '@nuxtjs/composition-api/module',
    'unplugin-vue2-script-setup/nuxt',
  ],
}
```

And then use [`vue-tsc`](https://github.com/johnsoncodehk/volar) to do the type check at build time:

```jsonc
// package.json
{
  "scripts": {
    "dev": "nuxt",
    "build": "vue-tsc --noEmit && nuxt build"
  }
}
```

<br></details>

<details>
<summary>Vue CLI</summary><br>

```ts
// vue.config.js

module.exports = {
  configureWebpack: {
    plugins: [
      require('unplugin-vue2-script-setup/webpack')(),
    ],
  },
}
```

Example: [`examples/vue-cli`](./examples/vue-cli)

###### TypeScript

To use TypeScript with Vue CLI, install `@vue/cli-plugin-typescript` but disable the type check:

```bash
npm i -D @vue/cli-plugin-typescript vue-tsc
```

```ts
module.exports = {
  configureWebpack: {
    plugins: [
      require('unplugin-vue2-script-setup/webpack')(),
    ],
  },
  chainWebpack(config) {
    // disable type check and let `vue-tsc` handles it
    config.plugins.delete('fork-ts-checker')
  },
}
```

And then use [`vue-tsc`](https://github.com/johnsoncodehk/volar) to do the type check at build time:

```jsonc
// package.json
{
  "scripts": {
    "dev": "vue-cli-service serve",
    "build": "vue-tsc --noEmit && vue-cli-service build"
  }
}
```

<br></details>

<details>
<summary>Webpack</summary><br>

```ts
// webpack.config.js
module.exports = {
  /* ... */
  plugins: [
    require('unplugin-vue2-script-setup/webpack')()
  ]
}
```

<br></details>

<details>
<summary>JavaScript API</summary><br>

```ts
import { transform } from 'unplugin-vue2-script-setup'

const Vue2SFC = transform(`
<template>
  <!-- ... -->
</template>

<script setup>
  // ...
</script>
`)
```

<br></details>

## IDE

We recommend using [VS Code](https://code.visualstudio.com/) with [Volar](https://github.com/johnsoncodehk/volar) to get the best experience (You might want to disable Vetur if you have it).

When using Volar, you will need to install `@vue/runtime-dom` as devDependencies to make it work on Vue 2.

```bash
npm i -D @vue/runtime-dom
```

[Learn more](https://github.com/johnsoncodehk/volar#using)

###### Global Types

If the global types are missing for your IDE, update your `tsconfig.json` with:

```jsonc
{
  "compilerOptions": {
    "types": [
      "unplugin-vue2-script-setup/types"
    ]
  }
}
```

###### ESLint

If you are using ESLint, you might get `@typescript-eslint/no-unused-vars` warning with `<script setup>`. You can disable it and add `noUnusedLocals: true` in your `tsconfig.json`, Volar will infer the real missing locals correctly for you. 

## Recommendations

If you enjoy using `<script setup>`, you might also want to try [`vue-global-api`](https://github.com/antfu/vue-global-api) to improve the DX even further. 

## Progress

- [x] PoC
- [x] Components registration
- [x] Compile time macros `defineProps` `defineEmits` `withDefaults`
- [x] Global types
- [x] Merge with normal scripts
- [x] Vite plugin
- [x] Webpack plugin
- [x] Nuxt module
- [ ] ~~Top-level await~~ (not supported)

## How?

<details>
  <summary>
    👀
  </summary>

![image](https://user-images.githubusercontent.com/11247099/130307245-20f9342e-377b-4565-b55d-1b91741b5c0f.png)

It's made possible by transforming the `<script setup>` syntax back to normal `<script>` and let the Vue 2 SFC compiler handle the rest.

<br></details>

## Sponsors

<p align="center">
  <a href="https://cdn.jsdelivr.net/gh/antfu/static/sponsors.svg">
    <img src='https://cdn.jsdelivr.net/gh/antfu/static/sponsors.svg'/>
  </a>
</p>

## License

[MIT](./LICENSE) License © 2021 [Anthony Fu](https://github.com/antfu)
