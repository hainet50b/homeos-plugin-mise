# homeos-plugin-mise

![License](https://img.shields.io/badge/license-MIT%20OR%20Apache--2.0-blue)

A [homeos](https://github.com/hainet50b/homeos) plugin for [mise](https://github.com/jdx/mise), the polyglot tool version manager.

This plugin manages each mise-provided tool as its own homeos package. The full
`tool@version` spec is passed as a single parameter, so any backend mise
supports works — core runtimes (`node@20`), `cargo:`, `npm:`, `ubi:`, and so on.

## Usage

Add the plugin to your homeos repository:

```sh
homeos plugin add mise
```

Create a package using this plugin (depend on your `mise` package so it is
installed first):

```sh
homeos package add node --plugin mise --param tool=node@20 --depends-on mise
homeos package add ripgrep --plugin mise --param tool=cargo:ripgrep@latest --depends-on mise
```

The homeos package name is a human-friendly slug (e.g. `ripgrep`); the actual
mise spec lives in the `tool` parameter, which may contain characters not
allowed in a package name (`@`, `:`, `/`, `[]`).

## Parameters

| Parameter | Description |
|-----------|-------------|
| `tool` | Full mise tool spec, e.g. `node@20`, `cargo:ripgrep@latest`, `npm:prettier@3`. Version is optional and defaults to `@latest`. |

## Actions

| Action | Command |
|--------|---------|
| install | `mise use -g -y "{{tool}}"` |
| update | `mise upgrade -y "{{tool}}"` |
| uninstall | `mise unuse -g -y "{{tool}}"` |

`mise use` both installs the tool and records it in the global config, and
`mise unuse` both removes it from the config and prunes the on-disk install —
so install and uninstall are a clean symmetric pair. `mise upgrade` keeps the
version range from the spec (e.g. `node@20` upgrades within `20.x`); it does
not bump the recorded version, so the homeos parameter remains the source of
truth for the version.

## License

Licensed under either of

 * Apache License, Version 2.0
   ([LICENSE-APACHE](LICENSE-APACHE) or <http://www.apache.org/licenses/LICENSE-2.0>)
 * MIT license
   ([LICENSE-MIT](LICENSE-MIT) or <http://opensource.org/licenses/MIT>)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
