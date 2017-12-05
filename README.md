# HueStatusModule

[![Build Status](https://travis-ci.org/APCOvernight/huestatusmodule.svg?branch=master)](https://travis-ci.org/APCOvernight/huestatusmodule) [![Coverage Status](https://coveralls.io/repos/github/APCOvernight/huestatusmodule/badge.svg?branch=master)](https://coveralls.io/github/APCOvernight/huestatusmodule?branch=master) [![Maintainability](	https://img.shields.io/codeclimate/maintainability/APCOvernight/huestatusmodule.svg)](https://codeclimate.com/github/APCOvernight/huestatusmodule/maintainability) 
[![Dependencies](https://img.shields.io/david/APCOvernight/huestatusmodule.svg)](https://david-dm.org/APCOvernight/huestatusmodule) [![Greenkeeper badge](https://badges.greenkeeper.io/APCOvernight/huestatusmodule.svg)](https://greenkeeper.io/)

Template [HueStatus](https://github.com/APCOvernight/huestatus/) module

## Get Started

- Clone or Fork this Repo
- Add your desired module name, version, git repo, author etc to package.json
- Run `npm install` to install dependencies
- Make sure [HueStatus](https://github.com/APCOvernight/huestatus/) is installed globally `npm install -g huestatus`

## Building your module

The entry point for this module is index.js. It must export a class that extends the [BaseModule class from HueStatus](https://github.com/APCOvernight/huestatus/blob/master/src/Module.js).

Your module class must have a start method, this is called when the module is loaded and HueStatus is ready to start updating.

Your module class can optionally have a generateInstanceName method, that generates a unique instanceName for use in debugging. If this method is omitted a uuid will be generated instead.

The BaseModule constructor adds the module config object to `this.config`. It also creates an event emitter at `this.emitter` but you shouldn't have to access this directly. You should use the change method (see below).

### this.change(status, message) ⇒ <code>async function</code>
The BaseModule change method is used to update the status (by emitting an event to the huestatus module).

**Returns**: <code>Promise</code>

| Param | Type | Description |
| --- | --- | --- |
| status | <code>String</code> | The status to send to the Hue Light - One of '*ok*', '*alert*', '*warning*', '*building*' |
| message | <code>String</code> | Message to send to the debug log. (Why is the status changing?) |

**Example**
```js
if (someConditionIsMet) {
  await this.change('ok', 'everything is ok')
}
```

## Testing

The default codestyle in this repository is APC-style, run `npm run lint` to lint the all js files in your project.

Unit tests are included in test, run these with `npm run test`. Test coverage will be calculated by [nyc](https://github.com/istanbuljs/nyc).

[Stryker](https://stryker-mutator.github.io/) mutation tests can be run with `npm run stryker`

### Running in your local environment

Run `npm link` ([docs](https://docs.npmjs.com/cli/link)) from the project directory, to make it available to node globally. Then you can register it in your .huerc and run `huestatus` to test it manually.

## Integrations

A .travis.yml file is included for simple [Continuous Integration in Travis](https://travis-ci.org). You will need to add your repo to travis to set up automated builds.

The npm coverage script is set up to send coverage to [Coveralls](https://coveralls.io/) and [Code Climate](https://codeclimate.com/) upon build. You will need to create an account and add you repositories there for this to work.

## Publishing

Make sure to write your own README, and make sure all references in package.json are to your new module name. 

You should include a `.huerc-example` file with an example of all the possible module config variables.

When you are ready, publish to NPM with `npm publish`.
