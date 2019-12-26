# Nuxt Validate

**This is a fork of [lewyuburi/nuxt-validate](https://github.com/lewyuburi/nuxt-validate).**  
If you use VeeValidate 2, can you consider to use [nuxt-validate](https://github.com/lewyuburi/nuxt-validate/tree/c0879facf4abf461a0fbdbd3afe3fd9247be56ec).

[![Downloads](https://badgen.net/npm/dm/@mole-inc/nuxt-validate)](https://www.npmjs.com/package/@mole-inc/nuxt-validate)
[![Version](https://badgen.net/npm/v/@mole-inc/nuxt-validate)](https://www.npmjs.com/package/@mole-inc/nuxt-validate)
[![License](https://badgen.net/npm/license/@mole-inc/nuxt-validate)](https://www.npmjs.com/package/@mole-inc/nuxt-validate)
[![codecov](https://codecov.io/gh/mole-inc/nuxt-validate/branch/master/graph/badge.svg)](https://codecov.io/gh/mole-inc/nuxt-validate)

Nuxt.js module for validations using [VeeValidate](https://github.com/logaretm/vee-validate) 3

## Install

Use npm

```sh
npm i vee-validate -S
npm i @mole-inc/nuxt-validate -D
```

or yarn

```sh
yarn add vee-validate
yarn add @mole-inc/nuxt-validate --dev
```

## Usage

Add `@mole-inc/nuxt-validate` to `buildModules`.

`nuxt.config.js`

```js
module.exports = {
  buildModules: [
    ...
    ['@mole-inc/nuxt-validate', {
      lang: 'es',
      nuxti18n: {
        locale: {
          'zh-CN': 'zh_CN'
        }
      }
      ...
      // regular vee-validate options
      // https://github.com/logaretm/vee-validate/blob/master/docs/configuration.md
    }]
  ]
}
```

### Using top level options

```js
module.exports = {
  buildModules: [
    '@mole-inc/nuxt-validate'
  ],
  nuxtValidate: {
    rules: ['required']
    nuxti18n: {
      locale: {
        'zh-CN': 'zh_CN'
      }
    }
  }
}
```

### Configuration

#### `lang`

- Default: `undefined`

The `lang` option accepts the name file placed on the [locale dir](https://github.com/logaretm/vee-validate/tree/master/locale) of Vee-Validate repository without the extension.

#### `rules`

- Default: `undefined`

If `undefined`, importing all rules.
When listed from [validation-rules](https://logaretm.github.io/vee-validate/api/rules.html#validation-rules), importing it.

```js
rules: ['alpha_dash', 'min']
```

#### `nuxti18n`

- Default: `undefined`

When `nuxti18n` option is set as a `true`, Vee-Validate's locale changes with nuxt-i18n's locale.  
If nuxt-i18n's locale and Vee-Validate's [locale](https://github.com/logaretm/vee-validate/tree/master/locale) are different, set `locale` object to convert locale code.

```js
nuxti18n: {
  locale: {
    // nuxt-i18n's locale: Vee-Validate's locale
    'zh-cn': 'zh_CN',
    'zh-tw': 'zh_TW'
  }
}
```

:warning: **notice:** If you use nuxt-i18n module, declare the nuxt-validate module at before it.

## Documentation

Read the [official Vee-Validate documentation and demos](https://logaretm.github.io/vee-validate/).

## FAQ

### How to add custom validation methods?

We recommend using plugins.

`nuxt.config.js`

```js
module.exports = {
  plugins: ["~plugins/validate.js"],
}
```

`plugins/validate.js`

```js
import { extend } from "vee-validate";

extend("my-validation", {
  message: "This {_field_} is invalid.",
  validate: value => {
    // ...
    return true;
  }
});
```
