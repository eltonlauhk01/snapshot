# @cypress/snapshot

> Adds value / object / DOM element snapshot testing support to Cypress test runner

[![NPM][npm-icon] ][npm-url]

[![Build status][ci-image] ][ci-url]
[![semantic-release][semantic-image] ][semantic-url]

## Install

Requires [Node](https://nodejs.org/en/) version 6 or above.

```sh
npm install --save-dev @cypress/snapshot
```

## Use

After installing, add the following to your `cypress/support/commands.js` file

```js
require('@cypress/snapshot')()
```

This registers a new command to create new snapshot or compare value to old snapshot

```js
describe('my tests', () => {
  it('works', () => {
    cy.log('first snapshot')
    cy.wrap({ foo: 42 }).snapshot()
    cy.log('second snapshot')
    cy.wrap({ bar: 101 }).snapshot()
  })
})

describe('focused input field', () => {
  it('is empty and then typed into', () => {
    cy.visit('http://todomvc.com/examples/react/')
    cy
      .focused()
      .snapshot('initial')
      .type('eat healthy breakfast')
      .snapshot('after typing')
  })
})
```

The snapshot object can be found in file `snapshots.js`. In the above case it would look something like this

```js
module.exports = {
  "focused input field": {
    "is empty and then typed into": {
      "initial": {
        "tagName": "input",
        "attributes": {
          "class": "new-todo",
          "placeholder": "What needs to be done?",
          "value": ""
        }
      },
      "after typing": {
        "tagName": "input",
        "attributes": {
          "class": "new-todo",
          "placeholder": "What needs to be done?",
          "value": "eat healthy breakfast"
        }
      }
    }
  },
  "my tests": {
    "works": {
      "1": {
        "foo": 42
      },
      "2": {
        "bar": 101
      }
    }
  }
}
```

If you change the site values, the saved snapshot will no longer match, throwing an error

![Snapshot mismatch](img/snapshot-mismatch.png)

## Debugging

To debug this module run with environment variable `DEBUG=@cypress/snapshot`

### Small print

Author: Gleb Bahmutov &lt;gleb@cypress.io&gt; &copy; 2017

License: MIT - do anything with the code, but don't blame u if it does not work.

Support: if you find any problems with this module, email / tweet /
[open issue](https://github.com/cypress-io/snapshot/issues) on Github

## MIT License

Copyright (c) 2017 Cypress.io &lt;gleb@cypress.io&gt;

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.

[npm-icon]: https://nodei.co/npm/@cypress/snapshot.svg?downloads=true
[npm-url]: https://npmjs.org/package/@cypress/snapshot
[ci-image]: https://travis-ci.org/cypress-io/snapshot.svg?branch=master
[ci-url]: https://travis-ci.org/cypress-io/snapshot
[semantic-image]: https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg
[semantic-url]: https://github.com/semantic-release/semantic-release
