
# Introduction

LSP describes a protocol that clients and language servers
can communicate over.  Many Agda developers believe that
LSP might be sufficient to be used as a basis of the
interaction with Agda.  This document fixes our existing
assumptions and the experience we got from prototypical
implementation [alster][alster].

## Good Parts

LSP is a standard that is supported by many major editors
such as [emacs][emacs], [neovim][neovim], [visual
studio][vstudio], and many others.

The protocol defines many standard requests/responses, e.g.
the server may ask the client to show an error message, or
replace the text at the given location.

All communication happens asynchronously, and the protocol
introduces ways on enforcing synchronisation between
servers and clients.

If interaction with Agda were to fit into standard
requests/responses, then no additional work on the client is
ever needed.  This is would be a huge advantage because most
of the existing clients have to implement custom support for
Agda interaction commands.

The exact number of Agda commands that actually fit into
standard part of the LSP protocol are yet to be investigated.
There is always an option to extend LSP with custom commands.
However, those will need special treatment on the client side.

## Bad Parts

If Agda interaction requires too much custom extensions,
we would not get much benefits.  The clients will have to
handle all the custom messages locally.  We still get the
"transport layer".

If LSP were to disappear in the next few years, we would
be stuck with a deprecated protocol that may be difficult
to replace.  This is something to keep in mind when
designing the language server (e.g. try to build a thin
wrapper that would allow to replace LSP if needed).

Some discussion in  phijor/agda-mode-ng#1


# Standard Language Features

We went through the list of [Language Features][langfeat]
and listed those that we believe fit well into Agda
interaction.

   - Go to XXX:
     Where the given symbol (the type for the given symbol)
     is defined.

   - Find references:
     Where the given symbol e.g. function is being used.

   - Document (highlight/reference/link):
     Given the symbol, highlight where it appears in the
     document.  This is smarter than text search as
     it takes into account typing information.

   - Hover: Tell the type of the symbol.

   - Code lens:
     The ability to show custom information "near" the
     symbol.  This can be used to display type (C-c C-d),
     contexts, etc.

   - Folding information:
     Compute folding information in the file.  Agda can
     do this much better than any custom solution, as it
     nows exactly ranges of data/record/function definitions.

   - Selection Range:
     Given the cursor position, return a list of "interesting"
     selections around it.  For example, expression, clause,
     function-definition, where-block, etc.
     
   - Completions:
     Compute the symbols in the given file/project annotating
     their kinds, so that I can autocomplete.

   - Semantic tokens:
     Pretty much the ability to ask for custom highlighting.
     One concern is that we can't really separate it from
     typechecking, so we have to see whether we want to
     support this request in isolation.

   - Inline value:
     Not quite sure exactly what this is supposed to do,
     but it may be useful for handling normalisation requests.

   - Inlay XXX:
     A way to show additional information at the given
     location.  Maybe useful for displaying hidden parameters.

   - Error handling (diagnostics):
     We surely want this.

   - Signature help:
     Show information about function parameters/types.

   - Code action:
     Perform some kind of refactoring.  This is something
     that fits perfectly into case-split/refine/give/...

   - Code formatting:
     This would be nice to have, but thre is no standard
     implementaion yet.

   - Rename:
     Nice idea, but it can be really difficult to implement
     properly for partially-applied mixfix operations.


[neovim]: https://neovim.io/
[vstudio]: https://visualstudio.microsoft.com/
[emacs]: https://www.gnu.org/software/emacs/
[alster]: https://github.com/phijor/alster
[LSP]: https://microsoft.github.io/language-server-protocol/
[langfeat]: https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#languageFeatures
