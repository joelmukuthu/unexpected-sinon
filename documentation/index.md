---
template: default.ejs
theme: dark
title: unexpected-sinon
repository: https://github.com/unexpectedjs/unexpected-sinon
---

# Unexpected-sinon

![Unexpected spy :)](unexpectedSpy.png)

This module extends the
[Unexpected](https://github.com/unexpectedjs/unexpected) assertion
library with integration for the [Sinonjs](http://sinonjs.org/)
mocking library.

```js
var obj = { spy: sinon.spy() };
obj.spy(42);
obj.spy({ foo: 'bar' }, 'baz', "qux");
expect(obj.spy, "was called twice");
expect(obj.spy, 'was called with', { foo: 'bar' }, 'baz', expect.it('to be truthy'));
expect(obj.spy, 'was always called on', obj);
```

[![NPM version](https://badge.fury.io/js/unexpected-sinon.svg)](http://badge.fury.io/js/unexpected-sinon)
[![Build Status](https://travis-ci.org/unexpectedjs/unexpected-sinon.svg?branch=master)](https://travis-ci.org/unexpectedjs/unexpected-sinon)
[![Coverage Status](https://coveralls.io/repos/unexpectedjs/unexpected-sinon/badge.svg)](https://coveralls.io/r/unexpectedjs/unexpected-sinon)
[![Dependency Status](https://david-dm.org/unexpectedjs/unexpected-sinon.svg)](https://david-dm.org/unexpectedjs/unexpected-sinon)

## How to use

### Node

Install it with NPM or add it to your `package.json`:

```
$ npm install unexpected unexpected-sinon
```

Then:

```js#evaluate:false
var expect = require('unexpected').clone();
expect.installPlugin(require('unexpected-sinon'));
```

### Browser

Include the `unexpected.js` found at the lib directory of this
repository.

```html
<script src="sinon.js"></script>
<script src="unexpected.js"></script>
<script src="unexpected-sinon.js"></script>
```

this will expose the expect function under the following namespace:

```js#evaluate:false
var expect = weknowhow.expect.clone();
expect.installPlugin(weknowhow.unexpectedSinon);
```

### RequireJS

Include the library with RequireJS the following way:

```js#evaluate:false
define(['unexpected', 'unexpected-sinon'], funtion (unexpected, unexpectedSinon) {
   var expect = unexpected.clone();
   expect.installPlugin(unexpectedSinon);
   // Your code
});
```

Because Sinon is currently not AMD compatible you will need this RequireJS configuration to make things work:

```js#evaluate:false
requirejs.config({
   paths: {
      'sinon': 'path/to/sinon'
   },
   shim: {
      'sinon': {
         deps: ['sinon'],
         exports: 'sinon'
      }
   }
});
```

## Expectations on arguments of individual calls

```js
var spy = sinon.spy();
spy({ foo: 'bar' }, 'baz');
spy('qux');
spy('quux');

expect(spy.args, 'to equal', [
    [{ foo: 'bar' }, 'baz'],
    ['qux'],
    ['quux']
]);

expect(spy.args[1], 'to equal', ['qux']);

expect(spy.args, 'to satisfy', {
    0: [
        { foo: 'bar' },
        expect.it('to be a string').and('to have length', 3)
    ],
    2: ['quux']
});
```

## Source

The source for Unexpected can be found on
[Github](https://github.com/unexpectedjs/unexpected-sinon).

## Release

### 6.0.0

* Introduced
  [to satisfy](http://unexpectedjs.github.io/assertions/any/to-satisfy/)
  samantics for
  [was called with](./assertions/spy/was-called-with/)
  and
  [threw](./assertions/spy/was-called-with/). Notice
  that matching on types by providing the type name no longer works,
  now it matches on the error message like
  [to throw](http://unexpectedjs.github.io/assertions/function/to-throw/).
* Improved the output for failing assertions a lot.

## MIT License

Copyright (c) 2013 Sune Simonsen <sune@we-knowhow.dk>

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
