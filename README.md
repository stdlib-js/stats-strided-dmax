<!--

@license Apache-2.0

Copyright (c) 2020 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# dmax

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Calculate the maximum value of a double-precision floating-point strided array.

<section class="intro">

</section>

<!-- /.intro -->

<section class="installation">

## Installation

```bash
npm install @stdlib/stats-strided-dmax
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

## Usage

```javascript
var dmax = require( '@stdlib/stats-strided-dmax' );
```

#### dmax( N, x, strideX )

Computes the maximum value of a double-precision floating-point strided array `x`.

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var x = new Float64Array( [ 1.0, -2.0, 2.0 ] );

var v = dmax( x.length, x, 1 );
// returns 2.0
```

The function has the following parameters:

-   **N**: number of indexed elements.
-   **x**: input [`Float64Array`][@stdlib/array/float64].
-   **strideX**: stride length for `x`.

The `N` and stride parameters determine which elements in the strided array are accessed at runtime. For example, to compute the maximum value of every other element in `x`,

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var x = new Float64Array( [ 1.0, 2.0, 2.0, -7.0, -2.0, 3.0, 4.0, 2.0 ] );

var v = dmax( 4, x, 2 );
// returns 4.0
```

Note that indexing is relative to the first index. To introduce an offset, use [`typed array`][mdn-typed-array] views.

<!-- eslint-disable stdlib/capitalized-comments -->

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var x0 = new Float64Array( [ 2.0, 1.0, 2.0, -2.0, -2.0, 2.0, 3.0, 4.0 ] );
var x1 = new Float64Array( x0.buffer, x0.BYTES_PER_ELEMENT*1 ); // start at 2nd element

var v = dmax( 4, x1, 2 );
// returns 4.0
```

#### dmax.ndarray( N, x, strideX, offsetX )

Computes the maximum value of a double-precision floating-point strided array using alternative indexing semantics.

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var x = new Float64Array( [ 1.0, -2.0, 2.0 ] );
var N = x.length;

var v = dmax.ndarray( N, x, 1, 0 );
// returns 2.0
```

The function has the following additional parameters:

-   **offsetX**: starting index for `x`.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameter supports indexing semantics based on a starting index. For example, to calculate the maximum value for every other value in `x` starting from the second value

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var x = new Float64Array( [ 2.0, 1.0, 2.0, -2.0, -2.0, 2.0, 3.0, 4.0 ] );

var v = dmax.ndarray( 4, x, 2, 1 );
// returns 4.0
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   If `N <= 0`, both functions return `NaN`.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var discreteUniform = require( '@stdlib/random-array-discrete-uniform' );
var dmax = require( '@stdlib/stats-strided-dmax' );

var x = discreteUniform( 10, -50, 50, {
    'dtype': 'float64'
});
console.log( x );

var v = dmax( x.length, x, 1 );
console.log( v );
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->

* * *

<section class="c">

## C APIs

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- C usage documentation. -->

<section class="usage">

### Usage

```c
#include "stdlib/stats/strided/dmax.h"
```

#### stdlib_strided_dmax( N, \*X, strideX )

Computes the maximum value of a double-precision floating-point strided array.

```c
const double x[] = { 1.0, -2.0, 3.0, -4.0 };

double v = stdlib_strided_dmax( 4, x, 1 );
// returns 3.0
```

The function accepts the following arguments:

-   **N**: `[in] CBLAS_INT` number of indexed elements.
-   **X**: `[in] double*` input array.
-   **strideX**: `[in] CBLAS_INT` stride length for `X`.

```c
double stdlib_strided_dmax( const CBLAS_INT N, const double *X, const CBLAS_INT strideX );
```

#### stdlib_strided_dmax_ndarray( N, \*X, strideX, offsetX )

Computes the maximum value of a double-precision floating-point strided array using alternative indexing semantics.

```c
const double x[] = { 1.0, -2.0, 3.0, -4.0 };

double v = stdlib_strided_dmax_ndarray( 4, x, 1, 0 );
// returns 3.0
```

The function accepts the following arguments:

-   **N**: `[in] CBLAS_INT` number of indexed elements.
-   **X**: `[in] double*` input array.
-   **strideX**: `[in] CBLAS_INT` stride length for `X`.
-   **offsetX**: `[in] CBLAS_INT` starting index for `X`.

```c
double stdlib_strided_dmax_ndarray( const CBLAS_INT N, const double *X, const CBLAS_INT strideX, const CBLAS_INT offsetX );
```

</section>

<!-- /.usage -->

<!-- C API usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- C API usage examples. -->

<section class="examples">

### Examples

```c
#include "stdlib/stats/strided/dmax.h"
#include <stdio.h>

int main( void ) {
    // Create a strided array:
    const double x[] = { 1.0, -2.0, 3.0, -4.0, 5.0, -6.0, 7.0, -8.0 };

    // Specify the number of indexed elements:
    const int N = 8;

    // Specify a stride:
    const int strideX = 1;

    // Compute the maximum value:
    double v = stdlib_strided_dmax( N, x, strideX );

    // Print the result:
    printf( "max: %lf\n", v );
}
```

</section>

<!-- /.examples -->

</section>

<!-- /.c -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

* * *

## See Also

-   <span class="package-name">[`@stdlib/stats-strided/dmin`][@stdlib/stats/strided/dmin]</span><span class="delimiter">: </span><span class="description">calculate the minimum value of a double-precision floating-point strided array.</span>
-   <span class="package-name">[`@stdlib/stats-strided/dnanmax`][@stdlib/stats/strided/dnanmax]</span><span class="delimiter">: </span><span class="description">calculate the maximum value of a double-precision floating-point strided array, ignoring NaN values.</span>
-   <span class="package-name">[`@stdlib/stats-strided/max`][@stdlib/stats/strided/max]</span><span class="delimiter">: </span><span class="description">calculate the maximum value of a strided array.</span>
-   <span class="package-name">[`@stdlib/stats-strided/smax`][@stdlib/stats/strided/smax]</span><span class="delimiter">: </span><span class="description">calculate the maximum value of a single-precision floating-point strided array.</span>

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2025. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/stats-strided-dmax.svg
[npm-url]: https://npmjs.org/package/@stdlib/stats-strided-dmax

[test-image]: https://github.com/stdlib-js/stats-strided-dmax/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/stats-strided-dmax/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/stats-strided-dmax/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/stats-strided-dmax?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/stats-strided-dmax.svg
[dependencies-url]: https://david-dm.org/stdlib-js/stats-strided-dmax/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/stats-strided-dmax/tree/deno
[deno-readme]: https://github.com/stdlib-js/stats-strided-dmax/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/stats-strided-dmax/tree/umd
[umd-readme]: https://github.com/stdlib-js/stats-strided-dmax/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/stats-strided-dmax/tree/esm
[esm-readme]: https://github.com/stdlib-js/stats-strided-dmax/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/stats-strided-dmax/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/stats-strided-dmax/main/LICENSE

[@stdlib/array/float64]: https://github.com/stdlib-js/array-float64

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

<!-- <related-links> -->

[@stdlib/stats/strided/dmin]: https://github.com/stdlib-js/stats-strided-dmin

[@stdlib/stats/strided/dnanmax]: https://github.com/stdlib-js/stats-strided-dnanmax

[@stdlib/stats/strided/max]: https://github.com/stdlib-js/stats-strided-max

[@stdlib/stats/strided/smax]: https://github.com/stdlib-js/stats-strided-smax

<!-- </related-links> -->

</section>

<!-- /.links -->
