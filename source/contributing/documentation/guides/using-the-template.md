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

# Using the template

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

The template encodes nix.dev's authoring conventions in its Seed, and [how to write a guide][write-a-guide] explains them in full — sentence case, one sentence per line, numbered steps, plain language, one voice, a humane tone, and examples-first. Read that page for the rationale; in practice, follow the Seed and the style guide and you will meet them.

## Filling it in: the workflow

1. Copy `guide-template.md` to your new guide's file.
2. Read the `<!-- Seed -->` comment at the top.
3. Replace `<component>` throughout the file.
4. Fill each section following the Seed's rules, not from memory.
5. Wire the new page into the relevant `toctree` / index.
6. Run the local build (see [contributor setup][setup] and [write a guide → Pass the automated checks][write-a-guide]) and fix every failure before opening your PR.

<!-- REVIEW(tone): Step 5 says "wire into the relevant toctree / index" — is that precise enough, or should it name the exact index file contributors must edit? -->

## Automated checks you must pass

The docs enforce CI checks that fail the build on warnings. [how to write a guide][write-a-guide] describes them and the current configuration in full (section "Pass the automated checks").

The one rule that most often breaks a template-derived guide: **never link to a `.md` file that does not exist in the repository.** The Sphinx build runs with `-W`, so a broken internal link fails the build. Link only to existing docs, or use full `https://` URLs for external resources.

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
