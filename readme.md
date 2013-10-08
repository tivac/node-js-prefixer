JS Prefixer
==========

Prefix relative URLs in JavaScript & JSON code with a cdn URL.

Turns `var a = "/fooga.js";` into `var a = "http://woogabooga.com/fooga.js"`;


[![Build Status](https://travis-ci.org/tivac/node-js-prefixer.png?branch=master)](https://travis-ci.org/tivac/node-js-prefixer)
[![NPM version](https://badge.fury.io/js/js-prefixer.png)](http://badge.fury.io/js/js-prefixer)
[![Dependency Status](https://gemnasium.com/tivac/node-js-prefixer.png)](https://gemnasium.com/tivac/node-js-prefixer)

## Usage ##

```javascript
var prefixer = require("js-prefixer"),
	code     = "var fooga = \"/googa/nooga.txt\";";

prefixr(code, { prefix : "//abcdefg123.cloudfront.net" }, function(err, src) {
    if(err) {
        throw new Error(err);
    }
    
    console.log(src); // writes out: var fooga = "//abcdefg123.cloudfront.net/googa/nooga.txt";
});
```

## API ##

### prefixer(code, [options], cb)

* `code` _{String}_ JS code string
* `options` _{Object}_
* `cb` _{Function}_
  * `err` _{Error | null}_
  * `src` _{String}_ Code with cdn-prefixed URLs

#### Options

* `prefix` _{String}_ URL used to prefix elements.
* `codegen` _{Object}_ escodegen options (see `./codegen.json` for defaults & [escodegen docs](https://github.com/Constellation/escodegen/wiki/API#options) for descriptions)

## Caveats ##

Support for JSON is enabled within esprima by attempting to `JSON.parse` incoming code, then modifying it by prepending `var ___jsprefixer___ = ` to it so it parses as valid JavaScript. This may have unintended side-effects and hasn't been thoroughly tested against real-world JSON.

## A Note on Versioning ##

This project's version number currently has a "0.x" prefix, indicating that it's a new
project under heavy development. **As long as the version number starts with
"0.x", minor revisions may introduce breaking changes.** You've been warned!

Once it reaches version 1.0.0, it will adhere strictly to
[SemVer 2.0](http://semver.org/spec/v2.0.0.html).
