---
myst:
  html_meta:
    "description lang=en": "How to set up a local nix.dev documentation environment for contributing."
    "keywords": "nix.dev, documentation, setup, contributing, development environment"
---

(setup)=

# How to set up your nix.dev environment

By the end of this guide you will have a working local preview of nix.dev running on your machine.
This lets you see your documentation changes exactly as they will appear on the published site.

## Prerequisites

Before you start, make sure you have the following.

- [Nix][nix-install] installed on your machine
- [Git](https://git-scm.com/) installed
- A [GitHub](https://github.com/) account
- A terminal you are comfortable using

Confirm that Nix is installed and check its version:

```shell-session
$ nix --version
```

If the command is not found, follow the [install Nix guide][nix-install] first.

## Install Nix

This ecosystem guide does not repeat the Nix package-manager installation steps.
If you do not have Nix yet, follow the [install Nix guide][nix-install] for your operating system.

## Set up direnv

You can load the development environment either by running `nix-shell` directly or by using [direnv][direnv-recipe] to load it automatically.
[direnv][direnv-recipe] is convenient because it reloads the environment every time you enter the repository directory.

To use direnv, install it and then allow the project's environment:

```shell-session
$ direnv allow
```

After this, the environment loads on its own whenever you `cd` into the repository.

## Fork and clone nix.dev

Fork the [nix.dev repository][nixdev-repo] on GitHub to your own account so you can push changes.
Then clone your fork and add the upstream remote so you can stay in sync:

```shell-session
$ git clone https://github.com/<your-username>/nix.dev.git
$ cd nix.dev
$ git remote add upstream https://github.com/NixOS/nix.dev.git
```

Replace `<your-username>` with your GitHub username.

## Enter the dev environment

The repository's `shell.nix` provides everything you need to work on the docs: Sphinx, MyST, npins, devmode, and vale.
Enter the development shell with:

```shell-session
$ nix-shell
```

:::{note}
If you prefer not to enter the main shell, a supplemental dev shell can provide `devmode` and `vale` without loading the full environment.
:::

## Preview your changes

Run `devmode` to start the live preview server:

```shell-session
$ devmode
```

Then open <http://localhost:8080> in your browser.
The page reloads automatically as you edit the source files.

## Lint your changes

Run vale to check your writing against the nix.dev style rules:

```shell-session
$ vale source
$ vale maintainers
```

Fix any errors or suggestions before opening a pull request.

## Build and verify

Build the site locally to verify that it compiles:

```shell-session
$ nix-build -A build
```

To include the reference manuals in the build, pass the `withManuals` argument:

```shell-session
$ nix-build -A build --arg withManuals true
```

Test redirects by serving the build output with Netlify:

```shell-session
$ netlify dev -d result
```

For a fast syntax check without a full build, run:

```shell-session
$ nix-shell --run "make dummy"
```

## Troubleshooting

:::{dropdown} Common issues

**npins is out of date**
Run `nix-shell --run update-nixpkgs-releases` and `nix-shell --run update-nix-releases` to refresh the pinned dependencies.

**direnv is not loaded**
If the environment variables or tools are missing, run `direnv allow` in the repository directory.

**Port 8080 is already in use**
Stop the process that is using port 8080, or set a different port before running `devmode`.

:::

## Next steps

Read the [authoring guide][authoring-guide] to learn how to write and structure new pages.
Then pick an open issue and start contributing your first change.

## References

- [Nix manual][nix-manual]
- [Nixpkgs manual][nixpkgs-manual]
- [NixOS manual][nixos-manual]
- [nix.dev repository][nixdev-repo]
- [direnv recipe][direnv-recipe]

[nix-install]: https://nix.dev/install-nix
[direnv-recipe]: https://nix.dev/guides/recipes/direnv.html
[nix-manual]: https://nix.dev/manual/nix/stable/
[nixpkgs-manual]: https://nixos.org/manual/nixpkgs/stable/
[nixos-manual]: https://nixos.org/manual/nixos/stable/
[nixdev-repo]: https://github.com/NixOS/nix.dev
[authoring-guide]: ./writing-a-tutorial.md
