---
myst:
  html_meta:
    "description lang=en": "How to write a new-user or installation HOW-TO guide for nix.dev"
    "keywords": "guide, how-to, documentation, contributing, nix.dev"
---

:::{note}
This template was created with generative AI (GenAI) assistance. Review and adapt it before publishing, and remove or replace this note in any guide you derive from it if you did not use GenAI to write that guide.
:::

<!-- REVIEW(consistency): The GenAI disclosure here ("AI-generated content. This page was authored with AI assistance") differs from guide-template.md ("created with generative AI (GenAI) assistance ... remove or replace this note ... if you did not use GenAI"). Align the disclosure phrasing across all three guide docs so contributors see one canonical note. -->

<!-- REVIEW(consistency): HUMAN UPDATE: aligned all GenAI notes to the one used in guide-template.md; this is due to it being more descriptive for newer contributors and removes ambiguity. -->

(writing-a-guide)=

# Writing a guide

This guide shows how to author a new-user or installation HOW-TO for nix.dev, starting from the existing template.
When you finish, you will have a complete, build-passing guide that follows the project's conventions.

## Before you start

Read the documents this guide depends on so your new page matches the project's conventions.

- Copy the [Guide template][template] as the seed for your page.
- Skim the [documentation style guide][style-guide] for voice, links, and one-sentence-per-line rules.
- Read the [Diátaxis overview][diataxis] so you keep your page in the right category.

You need a local checkout of the repository and the ability to run the documentation build (see [Next steps](#next-steps)).

## Write a how-to, not a tutorial

A guide is a goal-oriented list of steps that helps a reader reach a specific outcome.
It assumes the reader already understands the background and does not teach concepts.

For the underlying theory or a learning-oriented walkthrough, link to a [tutorial][tutorial] instead of explaining it inline.
For example, if your guide installs a tool, point readers to the relevant tutorial for *why* the tool matters rather than re-teaching it.

## Start from the template

Always begin from the [Guide template][template] rather than a blank file.
The template encodes the required shape: a short outcome statement, `Prerequisites`, the task sections, `Troubleshooting`, `Next steps`, and `References`.

Keep these conventions from the template:

- Write headings in [sentence case][style-guide].
- Write one sentence per line.
- State the outcome up front in plain language.
- Use numbered steps (`1.` `2.` `3.`) for procedures that must run in order.

## Plan your upstream links

Link to the canonical upstream sources so readers can go deeper, and so nix.dev stays a network of documentation.
Use [reference-style links][style-guide] defined at the end of the file.

Point readers to these sources:

- The [Nix manual][nix-manual] for the Nix package manager.
- The [Nixpkgs manual][nixpkgs-manual] for packages and derivations.
- The [NixOS manual][nixos-manual] for system configuration.
- Source repositories such as `github.com/NixOS/<repo>`, [permalinked to a commit or tag][nixpkgs-repo] when you cite code.

Prefer [permanent links](https://en.wikipedia.org/wiki/Permalink) (a commit or release tag) over branch URLs so citations do not rot.

## Keep Nix and NixOS scope separate

Pure Nix package-manager topics belong in package-manager guides, not in NixOS guides.
If your page would otherwise document installing the Nix daemon, link to the [install Nix guide][nix-install] instead of repeating those steps.

NixOS guides should cover `configuration.nix` and declarative system changes, and must not duplicate the package-manager install steps.
This keeps each page focused, maintains one voice across the manuals, and avoids divergent, conflicting instructions.

## Chain the next steps in sequence

Each guide should link to the next guide in its sequence from its `Next steps` section.
This lets readers flow from one task to the next without hunting through the navigation.

For example, an installation guide might end by pointing to a follow-up guide that configures the installed component.

## Check for parity with other docs

Cross-reference the [NixOS Wiki][nixos-wiki] and the [nixos.org manuals][nixos-manual] when you write or update commands.
Confirm that the commands and options you document match the current upstream behavior.

Flag any gaps you find: if upstream documents a step that nix.dev misses, note it in your pull request so the gap gets closed.

## Write in plain language

Use the imperative voice and short sentences, and avoid jargon.
State the outcome the reader will have at the end of the page before the first procedure.

Use numbered steps for ordered procedures.

1. Describe what the reader will do.
2. Show the command or configuration.
3. Show how to verify the result.

<!-- REVIEW(accuracy): For NixOS declarative guides the "verify the result" step must confirm the applied configuration took effect (e.g. after `nixos-rebuild switch`, check the running service / actual state), not just run `<component> --version`. Consider stating this explicitly so contributors don't ship a version-only check. -->

## Write with one voice and a humane tone

nix.dev exists to ease onboarding, so every guide should sound like the same friendly, competent helper. Address the reader directly as "you", avoid baby-talk, and never make the reader feel inexperienced.

- Keep the guide step-focused. For the *why* behind a step (concepts, rationale), link to the relevant [tutorial][tutorial] rather than explaining it inline — a how-to teaches actions, not theory. Add only a one-line note when it prevents a concrete mistake.
- Present optional steps as recommendations and give an escape hatch, for example "if you don't have a mobile number, skip this step". Never phrase them as demands.
- Keep troubleshooting neutral and non-blaming: state the symptom and the fix factually. Do not write "you did it wrong".

## Lead with examples (progressive disclosure)

Start with the minimal working steps so the reader reaches a result quickly, then explain only what they need to act. Introduce concepts just in time, not up front. This matches the project's onboarding goals and keeps guides approachable.

## Use the authoring scaffolds

The project's MyST setup supports several scaffolds.
Use them to keep pages consistent and readable.

<!-- REVIEW(scope): The tab-set example below shows the identical `nix-env -iA nixpkgs.example` command for both Linux and macOS. Confirm whether the steps genuinely differ per OS; if they don't, the tab-set is misleading and should collapse, or the macOS step should show its real divergence (e.g. nix-darwin path). -->

Use a `tab-set` when steps differ per operating system.

````markdown
::::{tab-set}

:::{tab-item} Linux

Install the package with your package manager.

```shell-session
$ nix-env -iA nixpkgs.example
```

:::

:::{tab-item} macOS

Use the same derivation on macOS.

```shell-session
$ nix-env -iA nixpkgs.example
```

:::
::::

````

Use admonitions to highlight non-linear content.

````markdown
:::{note}
Replace `example` with the actual option name for your setup.
:::

:::{tip}
Open a new terminal first if the command is not found.
:::

:::{important}
Back up your configuration before rebuilding.
:::

:::{warning}
This command removes the old profile; make sure you have a rollback.
:::

:::{dropdown} Why this happens
Nix installs packages into a profile directory that must be on `PATH`.
:::
````

Use `shell-session` for terminal output so copy-button and prompts render correctly.

<!-- REVIEW(accuracy): The example output `nix (Nix) 2.11.0` is a fixed version claim. Confirm it still matches a current/relevant Nix release, or replace with a placeholder like `<version>` so the example doesn't go stale. -->

```shell-session
$ nix --version
nix (Nix) 2.11.0
```

<!-- REVIEW(consistency): This exact `(pass-the-automated-checks)=` anchor is deep-linked from using-the-template.md via `[write-a-guide-checks]: ./writing-a-guide.md#pass-the-automated-checks`. If this heading or anchor is renamed, that deep link breaks the Sphinx `-W` build. Keep the anchor name locked or update the source link in lockstep. -->

(pass-the-automated-checks)=
## Pass the automated checks

The documentation has several automated checks that run in CI.
Knowing them prevents surprise build failures.

- `extractable_code_block` only executes code blocks that are explicitly marked to run.
  Placeholder or template shell blocks are not executed, so they are safe to leave as examples.
- `vale` runs at `MinAlertLevel = suggestion`, so it reports warnings and suggestions, not just errors.
- `editorconfig` requires Unix line endings (`lf`), a final newline, and no trailing whitespace.
- The Sphinx build uses `-W`, which turns warnings into errors.
  It **fails** on missing documentation cross-references, so broken links break the build.

Never include a Markdown link to a `.md` file that does not exist in the repository.
For example, linking to `./does-not-exist.md` triggers `myst.xref_missing` and fails the build under `-W`.
Only link to existing docs, or use full `https://` URLs for external resources.

## Next steps

- Copy and adapt the [Guide template][template] for your new guide.
- Set up a local build environment using the [nix.dev contributor documentation][nix-dev-contributor-guide] so you can run `vale` and the Sphinx build yourself.

## References

- [Nix manual][nix-manual]
- [Nixpkgs manual][nixpkgs-manual]
- [NixOS manual][nixos-manual]
- [nix.dev contributor guide][nix-dev-contributor-guide]

[template]: ./guide-template.md
[style-guide]: ../style-guide.md
[diataxis]: ../diataxis.md
[tutorial]: https://nix.dev/tutorials
[nix-install]: https://nix.dev/install-nix
[nix-manual]: https://nix.dev/manual/nix/stable/
[nixpkgs-manual]: https://nixos.org/manual/nixpkgs/stable/
[nixos-manual]: https://nixos.org/manual/nixos/stable/
[nixos-wiki]: https://wiki.nixos.org/
[nixpkgs-repo]: https://github.com/NixOS/nixpkgs/tree/24.11
[nix-dev-contributor-guide]: https://nix.dev/contributing/documentation/
