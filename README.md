# testron
CI your client side tests with Electron

[![build status](https://secure.travis-ci.org/shama/testron.svg)](https://travis-ci.org/shama/testron)
[![NPM version](https://badge.fury.io/js/testron.svg)](https://badge.fury.io/js/testron)
[![experimental](http://hughsk.github.io/stability-badges/dist/experimental.svg)](http://github.com/hughsk/stability-badges)

# about
This uses [Electron](https://github.com/atom/electron) to run tests in
[Chromium](http://www.chromium.org/).

# usage

* Install to your project: `npm install testron --save-dev`
* Install Electron: `npm install electron-prebuilt --save-dev`
* Add a `test` script to your `package.json`:  
    ```json
    {
      "name": "my-project",
      "scripts": {
        "test": "testron test/client.js"
      },
    }
    ```
* Run `npm test` to run the test script in Electron

## Writing tests
Currently this only supports TAP. Here is an example test written using [tape](https://www.npmjs.com/package/tape):

```js
// Let tape know we are running in a browser
process.browser = true
var test = require('tape')

test('test this', function (t) {
  t.plan(1)
  var ul = document.createElement('ul')
  var li = document.createElement('li')
  ul.appendChild(li)
  li.textContent = 'it works'
  t.equal(ul.outerHTML, '<ul><li>it works</li></ul>', 'client-test should have worked')
  t.end()
})
```

## API
There is also an API:

```js
var testron = require('testron')
var tests = testron('test/client.js')
tests.stdout.on('data', function (data) {
  console.log('line: ' + data.toString())
})
tests.on('exit', function () {
  console.log('Tests are done!')
})
```

# license
(c) 2015 Kyle Robinson Young. MIT License
