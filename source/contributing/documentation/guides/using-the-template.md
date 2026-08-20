---
myst:
  html_meta:
    "description lang=en": "How to use the nix.dev guide template: a contributor's annotated tour of guide-template.md"
    "keywords": "template, guide, how-to, contributing, nix.dev"
---

:::{note}
AI-generated companion page. This page was authored with AI assistance; review and adapt it before publishing.
:::

(using-the-template)=

# How to use this template

This page is a companion to [the guide template][template]. It installs nothing and contains no example component. Instead it walks the template section by section and explains, from a contributor's point of view, how the template is shaped and how to fill it in.

Read this page once to learn the shape, then keep [`guide-template.md`][template] open beside your editor while you write. For the full authoring rules (Diátaxis, linking, plain language), see [how to write a guide][write-a-guide].

<!-- REVIEW(tone): Confirm the framing here — is "companion" / "annotated tour" the right voice, or should this read as a stricter "required reading before you copy the template"? -->

## What the template is for

The template (`guide-template.md`) is a reusable skeleton for a **new-user, installation-style HOW-TO** on nix.dev. It exists so every new guide starts from the same shape and the same conventions, instead of from a blank file.

A template-derived guide is:

- **goal-oriented** — a how-to in the Diátaxis sense: a sequence of steps toward a specific outcome, not a concept lesson.
- **new-user / installation framed** — it assumes the reader wants to get `<component>` working, not to understand how `<component>` works.
- **NixOS-declarative where it matters** — for NixOS, configuration lives in `configuration.nix` and changes are applied with `nixos-rebuild switch` (or `build-vm`), not by hand.

It is explicitly **not a tutorial**. For the underlying theory or a learning-oriented walkthrough, link to a [tutorial][tutorial] instead of explaining it inline (see [write a guide][write-a-guide] for why).

## The seed comment

Near the top of `guide-template.md` is an HTML comment beginning `<!-- Seed ... -->`. It does not render in the published docs, but it carries the rules the template encodes:

- replace `<component>` throughout,
- keep pure-Nix package-manager steps out (link to the PM guides instead of documenting them),
- sequence the page `Prerequisites → Install → Configure → Verify → Troubleshooting → Next steps`,
- write headings in sentence case, one sentence per line, in plain language,
- state the outcome up front,
- for NixOS, verify the *result* of `nixos-rebuild`, not just `<component> --version`,
- in `Next steps`, chain to the next sequential guide,
- cross-check commands against the NixOS Wiki and nixos.org manuals for parity.

Read the Seed while you draft. It is the contract between the template and your finished guide.

<!-- REVIEW(accuracy): Confirm whether a contributor should KEEP the Seed comment in the published guide or strip it. The template ships with it; this page currently tells contributors to "read it while you draft" but does not state the final disposition. -->

## Section-by-section walkthrough

### Front matter

The page opens with MyST `html_meta` for `description` and `keywords`. Keep these: they feed search and site previews. Copy the template's block and swap the description to match your component.

### Outcome statement

(lines ~35-37 of the template)

The first prose after the title states, in plain language, what the reader will have at the end:

> This guide shows how to install and verify `<component>` on your system. When you finish, `<component>` will be installed and ready to use.

State the outcome up front. Then link to the relevant tutorial for background rather than re-teaching it.

### Prerequisites

State what the reader must already have (supported OS, required accounts). Critically, **do not document the Nix daemon install here** — if Nix itself is not installed, link to the [install Nix guide][nix-install] instead.

### Install `<component>`

Use a `tab-set` when the steps differ per operating system. For NixOS, install via the installer ISO / `nixos-rebuild`, not `nix-env`. Reserve the pure-Nix `nix-env -iA` path for the package-manager guides and link to them rather than expanding it inline.

### Configure `<component>`

Show the minimal configuration needed to use the component, and explain each option you set so readers do not copy commands blindly. For NixOS this means editing `configuration.nix`.

### Verify the installation

Confirm the install succeeded so readers catch mistakes early, and show the expected output. For NixOS, verify the *result* of the rebuild, not just a version string.

### Troubleshooting

List the most common failure and its fix. Use a `dropdown` for deeper detail that would distract from the main flow.

### Next steps

Point readers to the next guide in the sequence, plus related tutorials and reference material. This is how readers flow from one task to the next.

### References

Link to the official sources you cited, using reference-style links defined at the bottom of the file. Prefer [permanent links](https://en.wikipedia.org/wiki/Permalink) (a specific commit or tag) when citing source code so citations do not rot.

<!-- REVIEW(accuracy): The template's References section links [component-repo] to github.com/<owner>/<component>. Confirm the exact placeholder shape contributors should expect, and whether a "References" section is always required or optional for short guides. -->

## Conventions to keep

These come straight from the Seed and from [write a guide][write-a-guide]:

- **Sentence case** headings (e.g. `## Install <component>`, not `## Install the Component`).
- **One sentence per line** — MyST/Markdown treats one sentence per line as a soft wrap; it keeps diffs clean and reviews easy.
- **Numbered steps** (`1.` `2.` `3.`) for procedures that must run in order.
- **Plain language, imperative voice, short sentences**, no jargon; state the outcome before the first procedure.
- **One voice** — friendly, direct, competent; address the reader as "you". This serves nix.dev's onboarding goal of not making new users feel inexperienced.
- **Humane tone** — link to a tutorial for the *why*; keep the guide step-focused (only a one-line mistake-preventing note inline); optional steps are recommendations with an escape hatch; troubleshooting is neutral and non-blaming.
- **Examples first / progressive disclosure** — lead with the working steps; explain a concept only when the reader needs it to act.

## Filling it in: the workflow

1. Copy `guide-template.md` to your new guide's file.
2. Read the `<!-- Seed -->` comment at the top.
3. Replace `<component>` throughout the file.
4. Fill each section following the Seed's rules, not from memory.
5. Wire the new page into the relevant `toctree` / index.
6. Run the local build (see [contributor setup][setup] and [write a guide → Pass the automated checks][write-a-guide]) and fix every failure before opening your PR.

<!-- REVIEW(tone): Step 5 says "wire into the relevant toctree / index" — is that precise enough, or should it name the exact index file contributors must edit? -->

## Automated checks you must pass

The docs have CI checks that fail the build on warnings. From a template-user's perspective:

- `extractable_code_block` only runs blocks explicitly marked to run; template placeholder blocks are safe as examples.
- `vale` runs at `MinAlertLevel = suggestion`, so it reports warnings and suggestions, not just errors.
- `editorconfig` requires Unix line endings (`lf`), a final newline, and no trailing whitespace.
- The Sphinx build uses `-W`, which turns warnings into errors. It **fails on missing documentation cross-references**, so a broken internal `.md` link breaks the build.

Never link to a `.md` file that does not exist in the repository. Link only to existing docs, or use full `https://` URLs for external resources.

<!-- REVIEW(accuracy): These check descriptions are copied from writing-a-guide.md. Confirm they still match the current CI configuration before publishing this page. -->

## Next steps

- Read [how to write a guide][write-a-guide] for the full authoring rules.
- Set up a local build environment with the [nix.dev contributor documentation][nix-dev-contributor-guide] so you can run `vale` and the Sphinx build yourself.
- Copy [the template][template] and start your guide.

## References

- [Nix manual][nix-manual]
- [Nixpkgs manual][nixpkgs-manual]
- [NixOS manual][nixos-manual]
- [nix.dev contributor guide][nix-dev-contributor-guide]

[template]: ./guide-template.md
[write-a-guide]: ./writing-a-guide.md
[style-guide]: ../style-guide.md
[diataxis]: ../diataxis.md
[setup]: ../setup.md
[tutorial]: https://nix.dev/tutorials
[nix-install]: https://nix.dev/install-nix
[nix-manual]: https://nix.dev/manual/nix/stable/
[nixpkgs-manual]: https://nixos.org/manual/nixpkgs/stable/
[nixos-manual]: https://nixos.org/manual/nixos/stable/
[nix-dev-contributor-guide]: https://nix.dev/contributing/documentation/
