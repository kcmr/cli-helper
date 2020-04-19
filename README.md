<!--
[![Build Status](https://travis-ci.com/kcmr/cli-helper.svg?branch=master)](https://travis-ci.com/kcmr/cli-helper)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![codecov](https://codecov.io/gh/kcmr/cli-helper/branch/master/graph/badge.svg)](https://codecov.io/gh/kcmr/cli-helper)
![Dependency status](https://img.shields.io/david/kcmr/cli-helper.svg)

[![NPM](https://nodei.co/npm/cli-helper.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/cli-helper/)
-->

# CliHelper

> A multicommand CLI helper that uses yargs and inquirer.

## Install

```bash
npm i @kuscamara/cli-helper
```

## Usage

`CliHelper` creates CLIs from the specified commands object and uses [yargs](https://www.npmjs.com/package/yargs) for command options and [inquirer](https://www.npmjs.com/package/inquirer) to prompt for missing params not passed as flags / options.

```js
const CliHelper = require('@kuscamara/cli-helper');
const cli = new CliHelper({ options });
```

### Options

- `description` (`string`): Main command description.
- `defaultCommandMessage` (`string`): Prompt message of the default command. Default "Choose a command". 
- `commands` (`object`): CLI commands. Accepts an `action` key (`function`) for each command that will receive the executed command and the command options as `options` object. The `params` property uses the same options that inquirer questions.

**Full example**

```js
const CliHelper = require('@kuscamara/cli-helper');

const cli = new CliHelper({
  description: 'My awesome CLI',
  commands: {
    'print': {
      desc: 'Prints something',
      params: {
        color: {
          message: 'Use colors in output',
          type: 'boolean'
        }
      },
      action: ({ command, options }) => {
        console.log(`${command} executed with ${options.color}`);
      }
    },
    'greet': {
      desc: 'Says hello',
      params: {
        name: {
          message: 'Name',
          type: 'string'
        }
      },
      action: ({ options }) => {
        console.log(`Hello ${options.name}!`);
      }
    }
  }
});

cli.run();
```

### Registering custom prompt types

```js
const CliHelper = require('@kuscamara/cli-helper');
const { PathPrompt } = require('inquirer-path');

CliHelper.registerPrompt('path', PathPrompt);

const cli = new CliHelper(options);

cli.run();
```

## License

This project is licensed under the [MIT License](LICENSE).
