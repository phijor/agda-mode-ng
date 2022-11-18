# Improving Agda Interaction

This repository is a centralised location for
the ideas regarding interaction with Agda.  By interaction
we mean the ability to communicate with the type checker,
elaborator, etc. while developing Agda programs.

At [AIM XXXI][AIM31]
we concluded that we collect in this repository
_design documents_, links to (prototypical) _implementations_
and _design proposals_.

We are trying to improve the interaction experience,
so we do not have to stick to the old interaction backend
of Agda.  Certainly we want to reuse some parts, but we
work under the assumption that we are allowed to change
Agda.

# Problems with Existing Interaction

The existing Agda interaction mode has the following
shortcomings:

1. The interaction is very much
   [Emacs][emacs]-oriented.
   Therefore, integrating other text editors with the same
   level of feature support is difficult.

2. The interaction model has a built-in assumption that
   there is always a single file and the communication
   is synchronous.  This does not fit very well the idea
   of modern text editors which assume asynchronous
   communication.

3. When interacting with Agda, there is an inherent problem
   of figuring out when do you need to re-typecheck.
   Strictly speaking, Agda cannot answer any simplest
   requests (e.g. what is the type of this variable) without
   typechecking the entire file.  If the client made some
   edits and then sends the new request, do you need to
   re-typecheck the entire file (which can be slow), or
   it can be answered using the old server "state".
   These decisions are nowhere documented.  They are
   hard-coded and are very difficult to change.

# Links

Larger documents appear in their own file.  Here we keep
track of them and give a brief summary to simplify
navigation.

## LSP

[Language Server Protocol][LSP] is a standardised protocol
for language servers to communicate with text editors.
Language Server is an entity that can satisfy standard
requests that happen during developing programs, e.g.
what is the type of this variable, where this record
is defined, etc.

While LSP was not created to support theorem provers,
many of Agda developers agreed that this might be a valid
target to base an interaction with Agda.  The main 
argument in favour of using LSP is the number of editors
that support it.  This means that a lot of interacton
logic such as displaying error messages, changing text,
etc., does not need to be implemented on the clients.

Further details are here: [LSP design][lspdesign]


A proof-of-concept implementation is here: [Alster][alster]


## Alternative Implementations

There is a number of plugins that are current interaction
interface of Agda.

TODO

## Design

TODO

# How to Contribute

Feel free to open pull request or issues to discuss with us,
and more importantly share this place with anyone who is
thinking about writing their own Agda editor plugin.

[AIM31]: https://wiki.portal.chalmers.se/agda/pmwiki.php?n=Main.AIMXXXI
[emacs]: https://www.gnu.org/software/emacs/
[LSP]: https://microsoft.github.io/language-server-protocol/
[lspdesign]: https://github.com/phijor/agda-mode-ng/blob/main/LSP.md
[alster]: https://github.com/phijor/alster
