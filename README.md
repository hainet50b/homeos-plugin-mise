# homeos-plugin-mise

![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)

A [homeos](https://github.com/hainet50b/homeos) plugin for [mise](https://github.com/jdx/mise), the polyglot tool version manager.

## Usage

Add the plugin to your homeos repository:

```sh
homeos plugin add mise
```

Create a package using this plugin (depend on your `mise` package so it is installed first):

```sh
homeos package add java-temurin25 --plugin mise --param tool=java@temurin-25 --depends-on mise
homeos package add ripgrep --plugin mise --param tool=cargo:ripgrep@latest --depends-on mise
```

The homeos package name is a human-friendly slug you choose (e.g. `java-temurin25`); the full mise spec — including characters like `@` and `:` — goes in the `tool` parameter.

## Parameters

| Parameter | Description |
|-----------|-------------|
| `tool` | Full mise tool spec (e.g. `java@temurin-25`, `cargo:ripgrep@latest`) |

## Actions

| Action | Command |
|--------|---------|
| install | `mise use -g -y "{{tool}}"` |
| update | `mise upgrade -y "{{tool}}"` |
| uninstall | `mise unuse -g -y "{{tool}}"` |

## License

Licensed under either of

 * Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without any additional terms or conditions.
