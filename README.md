# Cypress dotenv-flow

Cypress plugin that enables compatability with [dotenv-flow](https://www.npmjs.com/package/dotenv-flow).  

[![Build Status](https://travis-ci.org/kamikazePT/cypress-dotenv-flow.svg?branch=master)](https://travis-ci.org/kamikazePT/cypress-dotenv-flow)
[![Maintainability](https://api.codeclimate.com/v1/badges/0d189dae8e924ada81ad/maintainability)](https://codeclimate.com/github/kamikazePT/cypress-dotenv-flow/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/0d189dae8e924ada81ad/test_coverage)](https://codeclimate.com/github/kamikazePT/cypress-dotenv-flow/test_coverage)

## What does this thing do?
It will load any [`environment variables`](https://docs.cypress.io/guides/guides/environment-variables.html#Option-2-cypress-env-json) defined in your `.env.<environment>.local` file so you can access them via `Cypress.env()` from within your tests as you would expect.

Any [Cypress config options](https://docs.cypress.io/guides/references/configuration.html) defined in your `.env` will also be applied and take precedence over what is in your `cypress.json` file. See the [Cypress docs for details on this](https://docs.cypress.io/guides/references/configuration.html#Environment-Variables)

For example, if your `.env` file has something like this:

```text
CYPRESS_HELLO=hola
GOODBYE=adios
```

You can use `Cypress.env('HELLO')` to access its value.

## Install
You will also need to install the original `dotenv-flow` package along with `cypress-dotenv-flow`
```bash
npm install --save-dev dotenv-flow cypress-dotenv-flow 
```
or
```
yarn add --dev dotenv-flow cypress-dotenv-flow
```

## Configure

Since this is a plugin, you will need to modify your file `cypress/plugins/index.js` to look something like this:

```javascript
const dotenvFlowPlugin = require('cypress-dotenv-flow');
module.exports = (on, config) => {
  config = dotenvFlowPlugin(config)
  return config
}
```

## Options
This plugin takes three paramaters. The first parameter (which is mandatory) is the Cypress config object. 

The second is an optional [dotenv-flow](https://www.npmjs.com/package/dotenv-flow#config) config object.

The third is an optional [all] boolean parameter, which is set to false by default. If set to true, it returns all available environmental variables, not limited to those prefixed with CYPRESS_.
