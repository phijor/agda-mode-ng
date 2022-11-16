# `agda-mode-ng`

> Let's rethink how we interact with Agda.

This repository is meant to coordinate efforts that improve how Agda integrates with text editors and IDEs.

At _AIM XXXI_, we discussed how to coordinate efforts towards writing a Language Server.
We concluded that any _design documents_ should end up here, and that this should be the
central place to discussed _potential implementations_ before committing to a specific
design.

## Goals

* enable Agda integration in editors that are not Emacs
* explore new interaction features:
    - auto-completion for identifiers
    - type information for types outside of the context of a hole
    - ...
* __Implement an Agda Language Server__ using the [Language Server Protocol][LSP]
* ... (your improvements here)

## How to Contribute

Feel free to open pull request or issues to discuss with us,
and more importantly share this place with anyone who is
thinking about writing their own Agda editor plugin.


[LSP]: https://microsoft.github.io/language-server-protocol/
