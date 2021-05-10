# @morellodev/prettier-config

A [shareable configuration](https://prettier.io/docs/en/configuration.html#sharing-configurations)
for projects using **[Prettier](https://prettier.io/)** .

## Installation

```sh
npm install --save-dev @morellodev/prettier-config
```

_This is only a shareable configuration. It does not install Prettier,
ESLint, or any other part of the tool chain._

## Usage

Reference it in `package.json` using the `prettier` property:

```json
{
  "name": "my-project-name",
  "prettier": "@morellodev/prettier-config",
  "devDependencies": {
    "@morellodev/prettier-config": "^1.0.0"
  }
}
```

If you don't want to use `package.json`, you can use any of the supported
extensions to export a string:

```jsonc
// `.prettierrc.json`
"@morellodev/prettier-config"
```

```javascript
// `prettier.config.js` or `.prettierrc.js`
module.exports = "@morellodev/prettier-config";
```

## Extending Shared Configurations

This configuration is not intended to be changed, but if you have a setup where
modification is required, it is possible. Prettier does not offer an "extends"
mechanism as you might be familiar from tools such as ESLint.

To extend a configuration you will need to:

1. Import/Require this sharable config from within your own configuration. This
   means you must be using a JavaScript version of a Prettier configuration
   file.
2. Extend your modification on top of the shared config using something like
   **[Object destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)**,
   **[Object.assign()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)**,
   or **[lodash.merge()](https://lodash.com/docs/4.17.11#merge)**
3. Export the modified configuration

> Prettier uses [cosmiconfig](https://github.com/davidtheclark/cosmiconfig) for
> configuration file support. This means you can configure prettier via:
>
> - A `.prettierrc` file, written in YAML or JSON, with optional extensions: `.yaml/.yml/.json`.
> - A `.prettierrc.toml` file, written in TOML (the `.toml` extension is _required_).
> - A `prettier.config.js` or `.prettierrc.js` file that exports an object.
> - A `"prettier"` key in your `package.json` file.

For example, if you need to change it so that semicolons are removed:

```javascript
// `prettier.config.js` or `.prettierrc.js`
const morellodevPrettierConfig = require("@morellodev/prettier-config");
const merge = require("lodash.merge");

const modifiedConfig = merge({}, morellodevPrettierConfig, {
  semi: false,
  // ... other modified settings here
});

module.exports = modifiedConfig;
```
