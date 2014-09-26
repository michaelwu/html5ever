# html5ever

[![Build Status](https://travis-ci.org/kmcallister/html5ever.svg?branch=master)](https://travis-ci.org/kmcallister/html5ever)

html5ever is an HTML parser developed as part of the [Servo](https://github.com/servo/servo) project.

It can parse and serialize HTML according to the [WHATWG](https://whatwg.org/) specs (aka "HTML5").  There are some omissions at present, most of which are documented [in the bug tracker](https://github.com/kmcallister/html5ever/issues?q=is%3Aopen+is%3Aissue+label%3Aweb-compat).  html5ever passes all tokenizer tests from [html5lib-tests](https://github.com/html5lib/html5lib-tests), and most tree builder tests outside of the unimplemented features.  The goal is to pass all html5lib tests, and also provide all hooks needed by a production web browser, e.g. `document.write`.

Note that the HTML syntax is a language almost, but not quite, entirely unlike XML.  For correct parsing of XHTML, use an XML parser.  (That said, many XHTML documents in the wild are serialized in an HTML-compatible form.)

html5ever is written in [Rust](http://www.rust-lang.org/), so it avoids the most notorious security problems from C, but has performance similar to a parser written in C.  You can call html5ever as if it were a C library, without pulling in a garbage collector or other heavy runtime requirements.


## Getting started in Rust

Add html5ever as a dependency in your [`Cargo.toml`](http://crates.io/) file:

```toml
[dependencies.html5ever]
git = "https://github.com/kmcallister/html5ever"
```

Then take a look at [`examples/print-rcdom.rs`](https://github.com/kmcallister/html5ever/blob/master/examples/print-rcdom.rs) and the [API documentation online](http://www.rust-ci.org/kmcallister/html5ever/doc/html5ever/).


## Getting started in other languages

The C API is not yet complete, but it's already possible to do [tokenization](http://mainisusuallyafunction.blogspot.com/2014/08/calling-rust-library-from-c-or-anything.html).

Bindings for Python and other languages are much desired.


## Working on html5ever

To build examples and tests, do something like

```
mkdir build
cd build
../configure
make examples check bench
```

This will invoke Cargo when necessary.

Run `cargo doc` in the repository root (or `make docs` in the build directory) to build local documentation under `target/doc/`.


## Details

html5ever uses callbacks to manipulate the DOM, so it works with your choice of DOM representation.  A simple reference-counted DOM is included.

html5ever exclusively uses UTF-8 to represent strings.  In the future it will support other document encodings (and UCS-2 `document.write`) by converting input.

The code is cross-referenced with the WHATWG syntax spec, and eventually we will have a way to present code and spec side-by-side.

We will track the Rust nightly builds until Rust 1.0, at which point there will be a stable 1.0 branch (details TBD).
