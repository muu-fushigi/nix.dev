---
myst:
  html_meta:
    "description lang=en": "How to use the nix.dev guide template: a contributor's annotated tour of guide-template.md"
    "keywords": "template, guide, how-to, contributing, nix.dev"
---

:::{note}
This template was created with generative AI (GenAI) assistance. Review and adapt it before publishing, and remove or replace this note in any guide you derive from it if you did not use GenAI to write that guide.
:::

<!-- REVIEW(tone): the AI-generated note at the top — is this label right for a meta page about the template, or should it be removed/shortened since it describes the template rather than a derived guide? -->



(using-the-template)=

# Using the template

This page is meta-commentary about [Guide template][template]. It installs nothing and names no real package. It walks the template section by section and explains, from a contributor's point of view, what each part is for and the placeholders it uses.

Read this page once to learn the shape, then keep [Guide template][template] open beside your editor while you write. For the full authoring rules (Diátaxis, linking, plain language), see [Writing a guide][write-a-guide].

<!-- REVIEW(tone): Confirm the framing here — is "companion" / "annotated tour" the right voice, or should this read as a stricter "required reading before you copy the template"? -->

The template stays generic on purpose: every concrete thing a finished guide would name is written as the literal placeholder `<component>`. Do not substitute a real package or command here — this page documents the template, it is not a filled-in example guide, and there is no worked example with real commands.

## What the template is for

The template (`guide-template.md`) is a reusable skeleton for a **new-user, installation-style HOW-TO** on nix.dev. It exists so every new guide starts from the same shape and the same conventions, instead of from a blank file.

A template-derived guide is:

- **goal-oriented** — a how-to in the Diátaxis sense: a sequence of steps toward a specific outcome, not a concept lesson.
- **new-user / installation framed** — it assumes the reader wants to get `<component>` working, not to understand how `<component>` works.
- **NixOS-declarative where it matters** — for NixOS, configuration lives in `configuration.nix` and changes are applied with `nixos-rebuild switch` (or `build-vm`), not by hand.

It is explicitly **not a tutorial**. For the underlying theory or a learning-oriented walkthrough, link to a [tutorial][tutorial] instead of explaining it inline (see [Writing a guide][write-a-guide] for why).

## Front matter

The template opens with MyST `html_meta` for `description` and `keywords`:

```yaml
---
myst:
  html_meta:
    "description lang=en": "Template: how to write a new-user installation guide for nix.dev"
    "keywords": "template, guide, installation, nix.dev"
---
```

<!-- REVIEW(scope): the front-matter guidance — should contributors copy the html_meta block verbatim and only swap the description, or also adjust the keywords per component? -->

Copy this block into your new guide and swap the `description` to match your component. Keep the `keywords` convention aligned with the other guides. These fields feed search and site previews, so they are required, not optional.

## Seed comment

Immediately after the front matter and before the title, the template carries an HTML comment beginning `<!-- Seed ... -->`. It does not render in the published docs, but it is the contract the template encodes:

- replace `<component>` throughout,
- keep pure-Nix package-manager steps out (link to the PM guides instead of documenting them),
- sequence the page `Prerequisites → Install → Configure → Verify → Troubleshooting → Next steps`,
- write headings in sentence case, one sentence per line, in plain language,
- state the outcome up front,
- for NixOS, verify the *result* of `nixos-rebuild`, not just `<component> --version`,
- in `Next steps`, chain to the next sequential guide,
- cross-check commands against the NixOS Wiki and nixos.org manuals for parity.

<!-- REVIEW(accuracy): Confirm whether a contributor should KEEP the Seed comment in the published guide or strip it. The template ships with it; this page currently tells contributors to "read it while you draft" but does not state the final disposition. -->

Read the Seed while you draft. It describes the template's intent; your finished guide should satisfy every rule it lists.

## Outcome statement

The template's first prose after the title states, in plain language, what the reader will have at the end:

> This guide shows how to install and verify `<component>` on your system. When you finish, `<component>` will be installed and ready to use.

It then links to the relevant [tutorial][tutorial] for background rather than re-teaching it. Keep this shape: state the outcome up front, then point to the tutorial for the *why*.

<!-- REVIEW(consistency): confirm the <component> placeholder convention is clear — it is a literal string to replace everywhere, including headings, prose, and code blocks (e.g. `nixpkgs.<component>`). -->

## Prerequisites

The template's `## Prerequisites` section tells the reader what they must already have before starting: a machine that can run NixOS, NixOS installation media (USB or ISO) prepared and ready to boot, the ability to boot from it, internet access for downloads, and optionally an existing `configuration.nix` to adapt. It does not document how to install NixOS itself — that belongs in the installation guides — so pure-Nix package-manager setup stays out of the template.

## Install `<component>`

The template's `## Install <component>` section shows the NixOS install path: add `<component>` to `environment.systemPackages` in your `configuration.nix`, then run `sudo nixos-rebuild switch` to apply the change. It does not use `nix-env` or document package-manager internals — those stay in the PM guides.



The `<component>` placeholder appears in the heading, in the `environment.systemPackages` list as `pkgs.<component>`, and in the verify command, so replacing it propagates to each.

## Configure `<component>`

The template's `## Configure <component>` section shows the minimal configuration needed to use `<component>` and explains each option so readers do not copy commands blindly. For NixOS this means editing `configuration.nix`. The example command uses the placeholder directly:

```shell-session
$ <component> config set example enabled
```

with a note telling the reader to replace `example` with the real option name.

## Verify the installation

The template's `## Verify the installation` section confirms the install succeeded and shows expected output, using `<component> --version` as the placeholder check.

<!-- REVIEW(accuracy): for NixOS the template says verify the result of nixos-rebuild switch rather than <component> --version; confirm the exact verify approach (rebuild result vs version string) contributors should follow. -->

For NixOS, the Seed instructs you to verify the *result* of the rebuild, not just a version string. The placeholder lets you decide the right check for your component.

## Troubleshooting

The template's `## Troubleshooting` section lists the most common failure and its fix, and uses a `dropdown` for deeper detail that would distract from the main flow. It references `<component>` in the symptom (`<component>` not found) so the placeholder stays consistent.

## Next steps

The template's `## Next steps` section points readers to the next guide in the sequence plus related tutorials and reference material. The Seed tells you to chain to the next sequential guide (for example, editing `configuration.nix`) so readers flow from one task to the next.

## References

The template's `## References` section links to the official sources it cited, using reference-style links defined at the bottom of the file, and prefers [permanent links](https://en.wikipedia.org/wiki/Permalink) (a specific commit or tag) when citing source code. It lists `[Nix manual]`, `[Nixpkgs manual]`, and `[<component> project][component-repo]`.

<!-- REVIEW(accuracy): The template's References section links [component-repo] to github.com/<owner>/<component>. Confirm the exact placeholder shape contributors should expect, and whether a "References" section is always required or optional for short guides. -->

## Conventions to keep

The template encodes nix.dev's authoring conventions in its Seed, and [Writing a guide][write-a-guide] explains them in full — sentence case, one sentence per line, numbered steps, plain language, one voice, a humane tone, and examples-first. Read that page for the rationale; in practice, follow the Seed and the [documentation style guide][style-guide] and you will meet them.

<!-- REVIEW(consistency): confirm the cross-links to [Writing a guide][write-a-guide] and the deep link [Writing a guide: Pass the automated checks][write-a-guide-checks] are the right anchors/keys to reference from this meta page. -->

## Filling it in: the workflow

1. Copy `guide-template.md` to your new guide's file.
2. Read the `<!-- Seed -->` comment at the top.
3. Replace `<component>` throughout the file.
4. Fill each section following the Seed's rules, not from memory.
5. Wire the new page into the relevant `toctree` / index.
6. Run the local build (see the [nix.dev contributor documentation][nix-dev-contributor-guide] and [Writing a guide: Pass the automated checks][write-a-guide-checks]) and fix every failure before opening your PR.

<!-- REVIEW(tone): Step 5 says "wire into the relevant toctree / index" — is that precise enough, or should it name the exact index file contributors must edit? -->

## Automated checks you must pass

The docs enforce CI checks that fail the build on warnings. [Writing a guide: Pass the automated checks][write-a-guide-checks] describes them and the current configuration in full.

The one rule that most often breaks a template-derived guide: **never link to a `.md` file that does not exist in the repository.** The Sphinx build runs with `-W`, so a broken internal link fails the build. Link only to existing docs, or use full `https://` URLs for external resources.

## Next steps

- Read [Writing a guide][write-a-guide] for the full authoring rules.
- Set up a local build environment with the [nix.dev contributor documentation][nix-dev-contributor-guide] so you can run `vale` and the Sphinx build yourself.
- Copy [Guide template][template] and start your guide.

## References

- [Nix manual][nix-manual]
- [Nixpkgs manual][nixpkgs-manual]
- [NixOS manual][nixos-manual]
- [nix.dev contributor guide][nix-dev-contributor-guide]

[template]: ./guide-template.md
[write-a-guide]: ./writing-a-guide.md
[write-a-guide-checks]: ./writing-a-guide.md#pass-the-automated-checks
[style-guide]: ../style-guide.md
[diataxis]: ../diataxis.md
[setup]: ../setup.md
[tutorial]: https://nix.dev/tutorials
[nix-install]: https://nix.dev/install-nix
[nix-manual]: https://nix.dev/manual/nix/stable/
[nixpkgs-manual]: https://nixos.org/manual/nixpkgs/stable/
[nixos-manual]: https://nixos.org/manual/nixos/stable/
[nix-dev-contributor-guide]: https://nix.dev/contributing/documentation/
