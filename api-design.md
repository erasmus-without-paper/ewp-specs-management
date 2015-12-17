Rules for API Design, Usage and Versioning
==========================================

[What is the status of this document?](statuses.md)


Semantic Versioning
-------------------

We use **Semantic Versioning** in all our API documentation. It has enormous
advantages, when it comes to working (and reworking) API design:

 * It allows us to tag specific API versions as officially approved.

 * It allows the developers to easily determine when a breaking change occurs
   in a particular API, and adapt properly.

 * It follows [a set of quite explicit rules](http://semver.org/). Please get
   familiar with them (especially if you plan to design parts of the APIs).

 * Combined with requirement of preparing a explicit and strict API
   specifications, it allows us to easily answer the question: **if it doesn't
   work then who's fault is that?**


Permalinks
----------

Whenever you post a new release of an API somewhere, you SHOULD use a Git tag
name (or a commit ID) in the posted URL. You should avoid posting links to the
`master` branch (which can mutate, even to the point of having the link
broken).

Try pressing <kbd>y</kbd> key on GitHub site to get a permalink ([other useful
keyboard shortcuts](https://help.github.com/articles/using-keyboard-shortcuts/)).


Backward-compatibility
----------------------

As required by the rules of [semantic versioning](http://semver.org/), all
[breaking changes](https://en.wiktionary.org/wiki/breaking_change) (aka
backward-incompatible changes) SHOULD force the MAJOR API version number to be
increased.

Once a document is [released](statuses.md), such backward-incompatible
changes SHOULD be avoided (is possible).

All non-trivial changes (especially the backward-incompatible ones!) must go
through the proposal acceptance process, as described in the
[Rules for Submitting API Change Proposals](change-proposals.md) document.


Changelogs (aka Release Notes)
-------------------------------

Once an API is [released](statuses.md), every subsequent release of this API
MUST be accompanied by a *changelog*. All changes SHOULD be noted in this
changelog (and *backward-incompatible* changes should be additionally
highlighted).

Please note, that this requirement is for **released** documents only, and it
does not imply the need of having a changelog for [change proposals]
(statuses.md). Before accepting a proposal, a partner SHOULD review the full
diff of the proposed change.


XML Schemas or REST?
--------------------

It is okay for one API to use JSON and be documented in Markdown, while some
other API uses XML and is documented in XML Schema. We do not put any
restrictions on the format of the API specifications, but we do have some other
requirements:

 * We require all the API specifications to be **explicit and strict**. If any
   part of the specifications turns out to be vague, then a new version of such
   specification SHOULD be released, fixing the vague part.

 * Try to avoid changing the format of the specification after it has been
   accepted, as this will "break the diffs".

