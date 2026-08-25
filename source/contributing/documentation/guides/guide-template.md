---
myst:
  html_meta:
    "description lang=en": "Template: how to write a new-user installation guide for nix.dev"
    "keywords": "template, guide, installation, nix.dev"
---

:::{note}
This template was created with generative AI (GenAI) assistance. Review and adapt it before publishing, and remove or replace this note in any guide you derive from it if you did not use GenAI to write that guide.
:::

(guide-template)=

# Guide template

<!-- Seed for a new-user/installation HOW-TO (NixOS). Rewrite/refresh existing
     docs from this skeleton — act on the existing indebted structure, don't
     invent from scratch. Do NOT document Nix package-manager (PM) internals:
     contributors should link out to the PM guides/tutorials instead of writing
     them here (this keeps one voice and avoids duplicated, drifting
     instructions). Replace <component> throughout. Headings in sentence case;
     one sentence per line.
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

This guide shows how to install and verify <component> on your NixOS system.
When you finish, <component> will be installed and ready to use.
For background on why this matters, see the [relevant tutorial][tutorial].

## Prerequisites

You need a few things in place before you start:

- A machine that can run NixOS (most commodity PCs do).
- NixOS installation media (a USB drive or ISO) prepared and ready to boot from.
- The ability to boot that machine from the installation media.
- Internet access, so the installer can download what it needs.
- Optionally, an existing `configuration.nix` you want to adapt.

You are ready to begin once you have booted into the NixOS live environment, or have your existing `configuration.nix` open to edit.

## Install <component>

<!-- REVIEW(scope): The Install section leads newcomers with environment.systemPackages + nixos-rebuild switch (the canonical declarative NixOS path). Confirm this is the right gentle on-ramp for new users, or whether nix profile install (simpler, no rebuild) is the better "feet wet" first step before introducing declarative config. -->

On NixOS you declare what you want in `configuration.nix`, then apply it.
`configuration.nix` is your system's description: it lists the packages and settings NixOS should build.
You do not install packages by hand — you add them to the description and let `nixos-rebuild switch` build and activate the new system for you.

Add <component> to the `environment.systemPackages` list in your `configuration.nix`:

```nix
environment.systemPackages = [ pkgs.<component> ];
```

Then apply the change:

```shell-session
$ sudo nixos-rebuild switch
building the system...
activating the configuration...
setting up /etc...
reloading systemd...
```

The rebuild ends without errors once <component> is part of your system.

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

After `nixos-rebuild switch` finishes, confirm the change actually took effect.
A successful rebuild that ends without errors means <component> is now part of your system.

Open a new terminal and run the component to confirm it works:

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

If `<component>` is not found after the rebuild, open a new terminal so your `PATH` picks up the newly installed package, and confirm `nixos-rebuild switch` completed without errors.

:::{dropdown} Why this happens

NixOS adds system packages to your `PATH` when the configuration is activated, so a stale terminal session may not see the new command until you reopen it.
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
[tutorial]: https://nix.dev/tutorials
[nix-manual]: https://nix.dev/manual/nix/stable/
[nixpkgs-manual]: https://nixos.org/manual/nixpkgs/stable/
[component-repo]: https://github.com/<owner>/<component>
