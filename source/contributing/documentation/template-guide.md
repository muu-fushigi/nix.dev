---
myst:
  html_meta:
    "description lang=en": "Template: how to write a new-user installation guide for nix.dev"
    "keywords": "template, guide, installation, nix.dev"
---

:::{note}
AI-generated template. This page was authored with AI assistance; review and adapt it before publishing.
:::

(template-guide)=

# How to install <component>

<!-- Seed for a new-user/installation HOW-TO (NixOS). Rewrite/refresh existing
     docs from this skeleton — act on the existing indebted structure, don't
     invent from scratch. Keep pure Nix package-manager steps out: link to the
     PM guides/tutorials instead of documenting them here. Replace <component>
     throughout. Headings in sentence case; one sentence per line.
     In Next steps, chain to the next sequential guide, e.g.
     [editing your configuration.nix](./edit-configuration.md). Cross-check
     commands against the NixOS Wiki and nixos.org manuals for parity.
     For full authoring rules see [how to write a guide](./write-a-guide.md). -->

This guide shows how to install and verify <component> on your system.
For background on why this matters, see the [relevant tutorial][tutorial].

## Prerequisites

State what the reader must already have before starting.
For example, list the supported operating systems and any required accounts.

If the Nix package manager itself is not installed, link to the [install Nix guide][nix-install] rather than documenting the daemon install here.

```shell-session
# Confirm Nix is installed and on a supported system
$ nix --version
```

## Install <component>

Use a `tab-set` when the steps differ per operating system.
Describe what each command does before showing it.

For NixOS, install the system via the installer ISO / `nixos-rebuild`, not `nix-env`.
Reserve `nix-env -iA` (below) for the pure-Nix package-manager path and link to PM guides instead of expanding it here.

:::::{tab-set}

::::{tab-item} Linux

Install <component> with your package manager.

```shell-session
$ nix-env -iA nixpkgs.<component>
```

::::

::::{tab-item} macOS

Install <component> on macOS with the same derivation.

```shell-session
$ nix-env -iA nixpkgs.<component>
```

::::

:::::

## Configure <component>

Show the minimal configuration needed to use <component>.
Explain each option you set so readers do not copy commands blindly.

```shell-session
$ <component> config set example enabled
```

:::{note}
Replace `example` with the actual option name for your setup.
:::

## Verify the installation

Confirm the install succeeded so readers can catch mistakes early.
Show the expected output of the check command.

```shell-session
$ <component> --version
<component> 1.0.0
```

:::{tip}
Open a new terminal first if the command is not found, so shell caches are refreshed.
:::

## Troubleshooting

List the most common failure and its fix.
Use a `dropdown` for deeper detail that would distract from the main flow.

If `<component>` is not found, make sure your `PATH` includes the Nix profile.

:::{dropdown} Why this happens

Nix installs packages into a profile directory that must be on `PATH`.
:::

## Next steps

Point readers to the next guide in the sequence, plus related tutorials and reference material.

- See the [installation tutorial][tutorial] for background.
- Read the [Nix manual][nix-manual] for the full list of options.

## References

Link to the official sources you cited.
Prefer [permanent links](https://en.wikipedia.org/wiki/Permalink) (a specific commit or tag) when citing source code.

- [Nix manual][nix-manual]
- [Nixpkgs manual][nixpkgs-manual]
- [<component> project][component-repo]

<!-- Replace the <component> placeholders and point [tutorial] at the specific
     component tutorial. Use permalinks (commits/tags) when citing source code. -->
[nix-install]: https://nix.dev/install-nix
[tutorial]: https://nix.dev/tutorials
[nix-manual]: https://nix.dev/manual/nix/stable/
[nixpkgs-manual]: https://nixos.org/manual/nixpkgs/stable/
[component-repo]: https://github.com/<owner>/<component>
