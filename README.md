# omarchy-dev

The development toolchain Omarchy ships, as a charly layer — the editor, language
runtimes, and git/container tooling its keybindings open.

The `omarchy-dev` candy installs the toolchain the distribution ships by default:
its Neovim configuration (`omarchy-nvim`, which seeds `/etc/skel` independently
of the editor package), the language runtimes its mise shims resolve (Ruby,
Clang/LLVM, .NET runtime, Python tooling), and the git and container TUIs its
keybindings open (`lazygit`, `lazydocker`). The Docker **packages** are installed
here, but the daemon is not enabled — a container cannot own one.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `omarchy-dev` |
| Requires | `layer-omarchy-base` (the foundation layer) |
| Installs | neovim + omarchy-nvim, tree-sitter, ruby, clang, llvm, dotnet-runtime, mise, poetry-core, lazygit, lazydocker, docker/buildx/compose, qemu-user-static-binfmt |
| Service / port | none (the docker daemon is deliberately not enabled) |

## How to use it

Compose the layer by pinning the member candy's sub-path in a box's `candy:`
list:

```yaml
my-omarchy-dev:
  candy:
    base: omarchy
    candy:
      - '@github.com/opencharly/layer-omarchy-base/candy/omarchy-base:v2026.242.0701'
      - '@github.com/opencharly/layer-omarchy-dev/candy/omarchy-dev:v2026.242.0635'
```

## Layout

- `charly.yml` — repo shape: the `discover:` rule that finds the member candy.
- `candy/omarchy-dev/charly.yml` — the candy entity (the `distro:` package arm
  and the `plan:` `check:` assertions).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Foundation: `/charly-distros:omarchy-base`.
- Nested containers: `/charly-distros:container-nesting` — the rootless nesting
  story, distinct from the Docker packages installed here.
- [`opencharly/opencharly](https://github.com/opencharly/opencharly) — the umbrella.
