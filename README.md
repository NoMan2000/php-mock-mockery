# Mock PHP built-in functions with Mockery

This package integrates the function mock library
[PHP-Mock](https://github.com/php-mock/php-mock) with Mockery.

# Installation

Use [Composer](https://getcomposer.org/):

```sh
composer require php-mock/php-mock-mockery
```

# Usage

[`PHPMockery::mock()`](http://php-mock.github.io/php-mock-mockery/api/class-phpmock.mockery.PHPMockery.html#_mock)
let's you build a function mock which can be equiped
with Mockery's expectations. After your test you'll have to disable all created
function mocks by calling `Mockery::close()`.

## Example

```php
<?php

namespace foo;

use phpmock\mockery\PHPMockery;

$mock = PHPMockery::mock(__NAMESPACE__, "time")->andReturn(3);
assert (3 == time());

\Mockery::close();
```

## Restrictions

This library comes with the same restrictions as the underlying
[`php-mock`](https://github.com/php-mock/php-mock#requirements-and-restrictions):

* Only *unqualified* function calls in a namespace context can be mocked.
  E.g. a call for `time()` in the namespace `foo` is mockable,
  a call for `\time()` is not.

* The mock has to be defined before the first call to the unqualified function
  in the tested class. This is documented in [Bug #68541](https://bugs.php.net/bug.php?id=68541).
  In most cases you can ignore this restriction. But if you happen to run into
  this issue you can call [`PHPMockery::define()`](http://php-mock.github.io/php-mock-mockery/api/class-phpmock.mockery.PHPMockery.html#_define)
  before that first call. This would define a side effectless namespaced function.

# License and authors

This project is free and under the WTFPL.
Responsable for this project is Markus Malkusch markus@malkusch.de.

## Donations

If you like this project and feel generous donate a few Bitcoins here:
[1335STSwu9hST4vcMRppEPgENMHD2r1REK](bitcoin:1335STSwu9hST4vcMRppEPgENMHD2r1REK)

[![Build Status](https://travis-ci.org/php-mock/php-mock-mockery.svg?branch=master)](https://travis-ci.org/php-mock/php-mock-mockery)
