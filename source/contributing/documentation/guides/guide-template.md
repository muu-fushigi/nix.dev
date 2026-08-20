---
myst:
  html_meta:
    "description lang=en": "Template: how to write a new-user installation guide for nix.dev"
    "keywords": "template, guide, installation, nix.dev"
---

:::{note}
This template was created with generative AI (GenAI) assistance. Review and adapt it before publishing, and remove or replace this note in any guide you derive from it if you did not use GenAI to write that guide.
:::

<!-- REVIEW(consistency): The GenAI disclosure wording here ("created with generative AI (GenAI) assistance ... remove or replace this note ... if you did not use GenAI") differs from writing-a-guide.md ("AI-generated content. This page was authored with AI assistance"). Align the disclosure phrasing across all three guide docs so contributors see one canonical note. -->

(guide-template)=

# Guide template

<!-- Seed for a new-user/installation HOW-TO (NixOS). Rewrite/refresh existing
     docs from this skeleton — act on the existing indebted structure, don't
     invent from scratch. Keep pure Nix package-manager steps out: link to the
     PM guides/tutorials instead of documenting them here (this also keeps one
     voice and avoids duplicated, drifting instructions). Replace <component>
     throughout. Headings in sentence case; one sentence per line.
     Use plain language and state the outcome up front (short sentences, no
     jargon; tell the reader what they will have at the end).
     Lead with the minimal working steps — examples first, progressive
     disclosure: introduce a concept only when the reader needs it to act, not
     up front. Keep one voice across every guide: friendly, direct, and
     competent; address the reader as 'you'. Be humane: if a step needs
     justification, link to the relevant tutorial for the why rather than
     explaining it here; only add a one-line note when it prevents a concrete
     mistake. Present optional steps as recommendations with an escape
     hatch (e.g. 'if you don't have X, skip this'); keep troubleshooting neutral
     and non-blaming (state the symptom and the fix, never 'you did it wrong').
     Sequence the page: Prerequisites -> Install/Do -> Configure -> Verify ->
     Troubleshooting -> Next steps. For NixOS, configuration is declarative: edit
     configuration.nix and run `nixos-rebuild switch` (or build-vm); verify the
     result rather than just `<component> --version`. In Next steps, chain to the
     next sequential guide, e.g. [editing your configuration.nix](./edit-configuration.md).
     Cross-check commands against the NixOS Wiki and nixos.org manuals for parity.
     For NixOS guides also cite the NixOS manual: https://nixos.org/manual/nixos/stable/.
     For ordered procedures use numbered steps (1. 2. 3.) for actions that must
     run in order. This page is a how-to GUIDE (goal-oriented,
     sequenced actions, just-in-time explanation), not a tutorial — keep it that way.
      For full authoring rules see [Writing a guide](./writing-a-guide.md). -->
<!-- REVIEW(consistency): This seed comment and the body cross-link to ./edit-configuration.md, ./writing-a-guide.md, and the style guide. After the restructure (guide contributor files moved into guides/, titles aligned to filenames, link labels normalised to page titles), verify each cross-reference target still exists and that its link label matches the target page title. -->

This guide shows how to install and verify <component> on your system.
When you finish, <component> will be installed and ready to use.
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

<!-- REVIEW(scope): The Linux and macOS tab-items below both show the identical `nix-env -iA nixpkgs.<component>` command. Confirm whether the steps genuinely differ per OS; if they don't, the tab-set is misleading and should collapse to a single block, or the macOS path should show its real divergence. -->

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

<!-- REVIEW(accuracy): The seed comment (lines ~37) instructs contributors to "verify the result rather than just `<component> --version`", but this Verify section only shows `<component> --version` and its expected output. For NixOS declarative guides the verification must check the actual applied result (e.g. service is running / config took effect), not merely the binary version. Reconcile the template body with the seed instruction. -->

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
