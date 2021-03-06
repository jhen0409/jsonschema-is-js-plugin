# jsonschema-is-js [![Build Status](https://travis-ci.org/jhen0409/jsonschema-is-js.svg)](https://travis-ci.org/jhen0409/jsonschema-is-js) [![NPM version](http://img.shields.io/npm/v/jsonschema-is-js.svg?style=flat)](https://www.npmjs.com/package/jsonschema-is-js)

The [jsonschema](https://github.com/tdegrunt/jsonschema) validator property included [is.js](https://github.com/arasatasaygin/is.js) functions for JavaScript.

## Install

```
$ npm i --save jsonschema jsonschema-is-js
```

## Usage

```js
var Validator = require('jsonschema').Validator;
var isPlugin = require('jsonschema-is-js');
var v = new Validator();

v.attributes.is = isPlugin();

var schema = {
  type: 'object',
  properties: {
    emails: { type: 'array', is: 'all.email' },  // <- use attribute
    text: { type: 'string', is: 'include:some' } // <- method:value, result: is.include(text, 'some')
  }
};

var result1 = v.validate({
  emails: [ 'a@test.cc', 'b@test.cc', 123, 'test' ]
}, schema);
var result2 = v.validate({
  emails: [ 'a@test.cc', 'b@test.cc', 'test@ggg.gg' ],
  text: 'some text...'
}, schema);

console.log(result1.errors);  // error
console.log(result2.errors);  // not error
```

Or use is.js of override regex:
```js
var is = require('is_js')
is.setRegexp(/quack/, 'url');
v.attributes.is = isPlugin(is);
```

## License

[MIT](LICENSE)
