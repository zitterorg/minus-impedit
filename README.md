# @zitterorg/minus-impedit <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ES spec-compliant `Array.prototype.concat` shim/polyfill/replacement that works as far down as ES3.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](https://tc39.es/ecma262/#sec-@zitterorg/minus-impedit).

Because `Array.prototype.concat` depends on a receiver (the “this” value), the main export takes the array to operate on as the first argument.

## Engines where this is needed

Note: this list is not exhaustive.

  - Safari 10 - 13
  - Chrome 48+ ([v8 bug](https://bugs.chromium.org/p/v8/issues/detail?id=10381))
  - node 6+

## Example

```js
var concat = require('@zitterorg/minus-impedit');
var assert = require('assert');

var a = [1, 1, 1];
assert.deepEqual(concat(a, 1, 2), [1, 1, 1, 1, 2]);
assert.deepEqual(a, [1, 1, 1]);
```

```js
var concat = require('@zitterorg/minus-impedit');
var assert = require('assert');
/* when Array#concat is not present */
delete Array.prototype.concat;
var shimmed = concat.shim();
assert.equal(shimmed, concat.getPolyfill());
assert.equal(shimmed, Array.prototype.concat);
assert.deepEqual([1, 2, 3].concat(1, 2, 3), concat([1, 2, 3], 1, 2, 3));
```

```js
var concat = require('@zitterorg/minus-impedit');
var assert = require('assert');
/* when Array#concat is present */
var shimmed = concat.shim();
assert.equal(shimmed, Array.prototype.concat);
assert.deepEqual([1, 2, 3].concat(1, 2, 3), concat([1, 2, 3], 1, 2, 3));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@zitterorg/minus-impedit
[npm-version-svg]: https://versionbadg.es/zitterorg/minus-impedit.svg
[deps-svg]: https://david-dm.org/zitterorg/minus-impedit.svg
[deps-url]: https://david-dm.org/zitterorg/minus-impedit
[dev-deps-svg]: https://david-dm.org/zitterorg/minus-impedit/dev-status.svg
[dev-deps-url]: https://david-dm.org/zitterorg/minus-impedit#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@zitterorg/minus-impedit.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@zitterorg/minus-impedit.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@zitterorg/minus-impedit.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@zitterorg/minus-impedit
[codecov-image]: https://codecov.io/gh/zitterorg/minus-impedit/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/zitterorg/minus-impedit/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/zitterorg/minus-impedit
[actions-url]: https://github.com/zitterorg/minus-impedit/actions
