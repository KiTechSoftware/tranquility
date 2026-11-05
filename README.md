# Tranquility

Tranquility (`tquil`) is a command-line tool, written in Rust, for setting up and managing a development machine. It handles:

- **Applications**: install and uninstall apps from a built-in catalog or your own applications file
- **Nerd Fonts**: list, install, update and uninstall fonts, downloaded from the latest upstream release
- **VPS profiles**: save SSH profiles, then connect, ping, run scripts, copy files, and import/export them
- **Config**: validate, override and reset the `config`, `applications` and `vps` files (TOML, YAML or JSON)
- **Diagnostics**: `info`, `doctor` and `logs` for system status and troubleshooting

## Build and run

```sh
cd workspace && cargo build
./target/debug/tquil --help
```

Or use the Makefile (a `justfile` and `taskfile.yml` expose the same targets):

| Target | Purpose |
| --- | --- |
| `make build` / `make run` | Build or run `tquil` |
| `make test` | Run the tests |
| `make test-coverage` | Run the tests with coverage |
| `make lint` / `make fmt` | Lint or format the code |
| `make check-license` | Check license headers |
| `make ci-check` | Run the full CI check |
| `make docs-serve` / `make docs-build` | Serve or build the docs (MkDocs) |
| `make image-run` | Run in a container image |
| `make setup` / `make dev-setup` / `make update` | Set up or update the environment |

## Quick start

```sh
tquil info
tquil app list
tquil font install --name FiraCode,Hack
tquil vps add --host example.com myserver
tquil vps connect --id myserver
```

Sample config files are in [`example/`](example/README.md). Check one with:

```sh
tquil config validate config --file example/config.toml
```

See the [command reference](docs/pages/commands.md) for every command and flag.

## Project layout

| Path | Contents |
| --- | --- |
| `workspace/` | The Rust crate (`tquil`): `cli`, `core`, `engine`, `infra` |
| `docs/` | MkDocs site and the command reference |
| `example/` | Sample config, applications and VPS files |
| `scripts/` | Build, test, lint, install and release scripts |
| `docker/` | Container image files |

## Contributing

Commits follow the rules in [`.cwizard.toml`](.cwizard.toml). See the [commit-wizard guide](https://commit-wizard.kitechsoftware.com/guides/getting-started/).

### Version management

The project ships a custom `cargo version` subcommand in `.cargo/bin/cargo-version`. It keeps `Cargo.toml` (the source of truth) and the root `VERSION` file in sync.

```sh
export PATH="$PWD/.cargo/bin:$PATH"   # once per shell, or add to your rc file
cargo version                         # print the current version
cargo version --set 1.2.3             # set a version (v1.2.3 also accepted)
cargo version --bump patch            # or minor / major
```

## License

Apache License, Version 2.0 (SPDX: `Apache-2.0`). The full text is in [`LICENSE`](LICENSE).
