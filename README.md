# Quori v1 Documentation

This repository is a work in progress for the complete documentation for the [Quori Robot v1](http://www.quori.org/).

The documentation is written in Markdown and built with [mdBook](https://rust-lang.github.io/mdBook/) and published with [github pages](https://pages.github.com/).

See the current state of the project here: https://semio-ai.github.io/quori-doc/introduction.html


## Building

To make and view changes, the repository can be cloned and built locally with mdBook,
with extra tools to for testing it, like `mdbook-linkcheck`.

```bash
cargo install mdbook mdbook-linkcheck
mdbook watch -o # Builds it, serves it, open it in a browser and auto-rebuilds on changes.
```

See the official instructions:
- [installing mdBook](https://rust-lang.github.io/mdBook/guide/installation.html).
- [serving](https://rust-lang.github.io/mdBook/guide/creating.html).
- [`mdbook-linkcheck`](https://crates.io/crates/mdbook-linkcheck).
