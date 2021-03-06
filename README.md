es6-mixin
=========

Minimalist mixin helper designed to be used with ES6 (ES2015) classes. Less than
1 kB minified and gzipped.

[![Latest Stable Version](https://img.shields.io/npm/v/es6-mixin.svg)](https://www.npmjs.com/package/es6-mixin)
[![License](https://img.shields.io/npm/l/es6-mixin.svg)](https://www.npmjs.com/package/es6-mixin)
[![Build Status](https://img.shields.io/travis/amercier/es6-mixin/master.svg)](https://travis-ci.org/amercier/es6-mixin)

[![NPM Downloads](https://img.shields.io/npm/dm/es6-mixin.svg)](https://www.npmjs.com/package/es6-mixin)
[![Test Coverage](https://img.shields.io/codecov/c/github/amercier/es6-mixin/master.svg)](https://codecov.io/github/amercier/es6-mixin?branch=master)
[![API Documentation](https://doc.esdoc.org/github.com/amercier/es6-mixin/badge.svg)](https://doc.esdoc.org/github.com/amercier/es6-mixin/index.html)

Installation
------------

``` shell
npm install --save es6-mixin
```

Usage
-----

### `mix(SuperClass, Mixin1, Mixin2, ...)`

``` javascript
import { mix } from 'es6-mixin';

class Super {
  foo() {
    return 'foo';
  }
}

class Mixin1 {
  bar () {
    return 'bar';
  }
}

class Mixin2 {
  baz () {
    return 'baz';
  }
}

class Sub extends mix(Super, Mixin1, Mixin2) {
}

new Sub().foo(); // => 'foo'
new Sub().bar(); // => 'bar'
new Sub().baz(); // => 'baz'
new Sub() instanceof Super; // => true
new Sub() instanceof Mixin1; // => false
new Sub() instanceof Mixin2; // => false
```

### `mixin(target, Mixin [, arg1, arg2, ...])`

#### Basic usage

``` javascript
import { mixin } from 'es6-mixin';

class Foo {
  foo() {
    return 'foo';
  }
}

class Bar {
  constructor() {
    mixin(this, Foo);
  }
}

new Bar().foo(); // => 'foo'
```

#### Pass parameters to a constructor

``` javascript
import { mixin } from 'es6-mixin';

class Foo {
  constructor(a, b, c) { ... }

  foo() {
    return 'foo';
  }
}

class Bar {
  constructor() {
    mixin(this, Foo, 1, 2, 3); // 1, 2, 3 are passed to Foo's constructor
  }
}

new Bar().foo(); // => 'foo'
```

#### Use with ES5-style prototypes

``` javascript
import { mixin } from 'es6-mixin';

function Foo() {
}

Foo.prototype.foo = function() {
  return 'foo';
};

class Bar {
  constructor() {
    mixin(this, Foo);
  }
}

new Bar().foo(); // => 'foo'
```

### `class extends Mixin { ... }`

``` javascript
import { Mixin } from 'es6-mixin';

class Foo extends Mixin {
  foo() {
    return 'foo';
  }
}

class Bar {
  constructor() {
    Foo.mixin(this);
  }
}

new Bar().foo(); // => 'foo'
```
