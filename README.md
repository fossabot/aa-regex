# aa-regex

[![Lifecycle: experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fjeanmanguy%2Faa-regex.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fjeanmanguy%2Faa-regex?ref=badge_shield)


[![Rust](https://github.com/jeanmanguy/aa-regex/workflows/Rust/badge.svg?branch=master)](https://github.com/jeanmanguy/aa-regex/actions?query=workflow%3ARust)
[![Rust Documentation](https://img.shields.io/badge/api-rustdoc-blue.svg)](https://docs.rs/aa_regex)
[![Crates.io version](https://img.shields.io/crates/v/aa_regex)](https://crates.io/crates/aa-regex/)
[![Crates.io license](https://img.shields.io/crates/l/aa_regex)](https://github.com/jeanmanguy/aa-regex/blob/master/LICENSE)

Utility macros to build regular expression matching protein sequences.

**Warning**: Work in progress, very experimental library, this is my very first crate.

## Motivation

 We can use regular expressions to match motifs on peptidic sequences, but writing them is a bit tedious. Some can become very complicated to read and understand. This crate tries to provide macros to help writing regular expressions at compile time. It uses procedural macros to generate strings that can be concatenated and used as regular expressions using the reduced alphabet of 20 amino acids. Any residue can now be limited to any valid amino acid instead of `.` (which would macth any valid unicode character) or manually writing the 20 amino acids and brackets. Does it make the regular expression search faster? I don't know.

## Setup

Add this to your `Cargo.toml`:

```toml
[dependencies]
aa-regex = "0.3"
```


## Usage

### Any

```rust
use aa_regex::any;

let any = any!(); // => let any = "[ARNDCEQGHILKMFPSTWYV]";
assert_eq!(any, "[ARNDCEQGHILKMFPSTWYV]");
```

### Any of

```rust
use aa_regex::any_of;

let any_aromatics = any_of!(W, F, Y); // => let any_aromatics = "[WFY]";
assert_eq!(any_aromatics, "[WFY]");
```

### Except

```rust
use aa_regex::except;

let no_proline = except!(P); // => let no_proline = "[ARNDCEQGHILKMFSTWYV]";
assert_eq!(no_proline, "[ARNDCEQGHILKMFSTWYV]");
```

### Aliases

TODO

- `any_aromatics!()`
- `except_aromatics!()`
- `except_proline!()`
- `any_charged!()`
- ...

### Concatenation

You can use the `std::concat!` macro to assemble the regular expression.

```rust
let motif = concat!(any_of!(R, H, K), except!(P)); // => let motif = "[RHK][ARNDCEQGHILKMFSTWYV]";
assert_eq!(motif, "[RHK][ARNDCEQGHILKMFSTWYV]")
```

## Ideas & bugs

Please create a new issue on the [project repository](https://github.com/jeanmanguy/aa-regex/issues).

## License

Aa-regex is distributed under the terms of the Apache License (Version 2.0). See [LICENSE](./LICENSE) for details.


[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fjeanmanguy%2Faa-regex.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fjeanmanguy%2Faa-regex?ref=badge_large)