Working with EWP Technical Documentation
========================================

This document is our proposal on **how** to work with the technical
documentation within the EWP project (where to store it, how to submit change
proposals, etc.).

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


The Structure of EWP Repositories
---------------------------------

### How documentation is to be divided?

 * Separate sections of the documentation SHOULD be stored in **separate
   Git repositories**.

 * The index of all documents (along with their current statuses) SHOULD be
   kept [at this URL][develhub]. If SHOULD be frequently updated.

Some of these repositories will probably not change much after their first
release, while some others (like the APIs) will probably keep mutating perhaps
even after the project is finished (though, in a backward-compatible way).


### Why separate API repositories?

We chose to split EWP requirements into a couple of separate APIs, and host
them in separate GitHub repositories:

 * We believe that partners (this includes all the **future** partners) should
   have the option to implement just a **subset** of all the features we have
   documented. This will make it easier for them to start off, claim that they
   have parts of EWP properly implemented, and then implement other parts later
   (possibly *much* later, with other teams of developers).

 * Having each API in **separate repository** has some great advantages, when
   it comes to versioning:

   - If a partner does not implement *API X*, then he also knows that he may
     ignore all the changes in *API X*'s repository.

   - If a partner has already implemented *API Y* and wants to upgrade his
     implementation to include some new changes in new API release, he may
     simply review a diff (and/or release notes) in the Git repository between
     specific tags.

   - It allows us to use [semantic versioning](http://semver.org/) separately
     for each API. This allows the partners to easily spot
     backward-incompatible changes which may break their implementations.

 * It allows the project leaders to choose and manage separate teams for
   working with separate APIs.


### Why GitHub?

We chose to use Git and GitHub as the primary tool for working and hosting
*documentation for developers*:

 * All developers are familiar with Git. Many developers are also familiar with
   GitHub. **We will require developers to review and accept documentation
   often** throughout the project. We believe that these tools will help them
   with this task.

 * Git allows us to easily keep track of all the changes. Having the option
   to produce a set of changes between particular versions of the documentation
   (e.g. "what has changed between versions `1.0.0` and `1.2.7`?") is a very
   important feature, and it can be easily achieved with Git.

 * GitHub features include an integrated code review tools, issue trackers,
   change notifications, automated build tools - and many other features. We
   are aware that our most of the repositories will be hosting documentation
   only, but we do find all these tools useful even in documentation-only
   projects.


Issue tracker
-------------

*WRTODO: The location of the issue tracker is yet to be agreed upon.*

GitHub offers built-in issue tracking which would be entirely sufficient for
purposes of developing the software and its documentation. However:

 * There are also other (external) issue trackers which would also suffice for
   this particular purpose.

 * If GitHub turns out to be NOT sufficient for other parts of the EWP project
   (and developers are not the only ones who need issue tracking) - then we
   SHOULD try to find a common solution which would play out well for everyone.

 * We SHOULD have only one issue tracker. Having multiple issue trackers might
   lead to confusion. E.g. a term "issue #123" might become ambiguous.

 * Some WPs declared that they will be using Redmine for their own purposes.
   We believe it would in everyone's best interest if we at least tried to use
   the same Redmine instance for tracking our issues too.


Rules for API Design and Versioning
-----------------------------------

### Semantic Versioning

We will use **Semantic Versioning** for releases of EWP technical
documentation. It has enormous advantages, when it comes to working (and
reworking) API design:

 * We will assign documents their version numbers only after they are
   officially approved.

 * Semantic versioning scheme allows developers to easily determine when a
   breaking change occurs in a particular API.

 * It follows [a set of quite explicit rules](http://semver.org/). Please get
   familiar with them (especially if you plan to design parts of the APIs).

 * Having a single, official latest version of the document, combined with the
   requirement of preparing an explicit and strict API specifications, allows us
   to easily answer the question: **if it doesn't work then who's fault is
   that?**


### Backward-compatibility

 * As required by the rules of [semantic versioning](http://semver.org/), all
   [breaking changes](https://en.wiktionary.org/wiki/breaking_change) (aka
   backward-incompatible changes) SHOULD force the **major** API version number
   to be increased (e.g. `1.3.7` should become `2.0.0`).

 * API designers MUST take care of [backward-compatibility rules]
   [backward-compatibility-rules], to facilitate predictable workflow for all
   implementers.

 * Once a document is [released][statuses], backward-incompatible changes
   SHOULD be avoided. Once first implementations are deployed on production
   servers, backward-incompatible changes MUST NOT occur, unless they cannot be
   avoided.

 * All non-trivial changes (especially the backward-incompatible ones) must go
   through the proposal acceptance process, as described in the
   [Rules for Submitting API Change Proposals](#change-proposals) section.


### Git branches (and XML namespaces)

 * All released specifications MUST be merged to a `stable-v<N>` branch, where
   *N* is the major version number of the specification (ideally, *N* will
   stay equal to `1` for the majority of all specifications).

 * XML namespaces used throughout the project SHOULD "self-describe"
   themselves. Namespace values SHOULD be valid GitHub URLs, pointing to
   `stable-*` GitHub branches. Every XML document SHOULD conform to the
   specification described in the `stable-*` branch given in its XML namespace.

 * Major changes in API versions SHOULD lead to a new `stable-*` (e.g.
   `stable-v2`) branch being created. If there is any XML namespace associated
   with API, then this also means that a new XML namespace will be created (and
   newer versions of XML documents will be required to use this namespace).

 * Unreleased (draft) APIs also SHOULD use valid GitHub URLs for theirs XML
   namespaces (most probably, URLs referring to the `master` branch).


### Changelogs (aka Release Notes)

 * Once a document is [released][statuses], every subsequent release of such
   document MUST be accompanied by a *changelog*. All changes SHOULD be noted
   in this changelog (and *backward-incompatible* changes should be
   additionally highlighted).

Please note, that this requirement is for **released** documents only, and it
does not imply the need of having a detailed changelog made for every [change
proposal][statuses] (although many change proposals MAY be accompanied by such
change logs).


### Preferred Data Formats

*WRTODO: The preferred data format is yet to be decided upon.*

 * XML? (our current pick)
 * JSON?


### Preferred Documentation Format

*WRTODO: The preferred documentation format is yet to be decided upon.*

 * Markdown? (our current pick)
 * reStructuredText?
 * JSON Schema?
 * XML Schema? (our current pick)

Regardless of what we choose, we do have some requirements on the documentation
itself:

 * We require all API specifications to be **explicit and strict** (with lots
   of "MUSTs" and "MUST NOTs" and detailed explanations for all the
   enumerations used). If any part of the specifications turns out to be vague,
   then a new version of such specification SHOULD be released, fixing the
   vague part.

 * Let's try to avoid changing the format of the specification after it has
   been first released (as this would "break the diffs").


### Use permalinks!

Whenever you post a link to a specific version of a document somewhere, you
SHOULD use a Git tag name (or a commit ID) in the posted URL. You should avoid
posting links to the `master` branch (which can mutate, even to the point of
having the link broken).

*Hint:* Try pressing <kbd>y</kbd> key on GitHub site to get a permalink ([other
useful keyboard shortcuts](https://help.github.com/articles/using-keyboard-shortcuts/)).


<a name="statuses"></a>

Document statuses
-----------------

Before you read any EWP document on GitHub, make sure you know the status of
this document. An index of official documents and drafts is kept [here]
[develhub]. You can also attempt determine the status yourself based the
document's **location and context**.

Common document statuses include (but are not limited to):

 * **RELEASED** - All partners have approved the document and it has been
   assigned a version number (e.g. `1.0.0`) in one of the official project
   repositories.

   * If there is no newer release of this document (no version with a greater
     tag name) then it is a **Latest release**.

   * If there exists a newer release of this document, then its status is
     **OUTDATED**. The latest release MAY be backward-incompatible with this
     document.

   * It is also possible for a document to be at its latest release, but the
     entire API (described by this document) has been **DEPRECATED**, and
     probably replaced by some other API. Such documents MUST explain (inside
     their contents) *why* they are deprecated, and which other APIs replace
     them. (Note, that this definition does not prohibit to *undeprecate* a
     document.)

 * **CHANGE PROPOSAL** - A document is a copy of another document with a set of
   changes applied. The partners are asked to comment on the *changed* parts of
   the document (e.g. when compared to the latest release).

   Change proposals may appear outside of the official repositories (i.e. in
   forks). They are often accompanied by open pull requests for merging them to
   official `stable-*` branches.

 * **DRAFT** - designers are still working on this document. It has not been
   approved, but everyone may comment on it. After being reviewed and accepted,
   drafts become releases.

"Official repositories" are the ones owned by the **erasmus-without-paper**
GitHub organization.


<a name='change-proposals'></a>

Rules for Submitting API Change Proposals
-----------------------------------------

### How to propose a change to a document?

 * **Option 1.** Start a new thread in our issue tracker (WRTODO: put a link to
   the tracker here.) Please make sure to select a proper project and assign a
   proper category to your ticket.

   The authors and maintainers of the APIs MUST subscribe for GitHub
   notifications for their projects, and should be notified when you submit a
   new issue to the tracker.

 * **Option 2.** You MAY also fork the repository, change what you want
   changed, and send a GitHub pull request.

   If your pull request is complicated, consider creating a separate issue page
   for tracking it. Pull requests are NOT the proper place for longer
   discussions - such discussions SHOULD be conducted within the issue tracker.


### How to get my draft (or change proposal) released?

You CANNOT assume that all partners are watching all of the issues. You
MUST contact all the partners and attempt to get their approval before you can
deem your proposal as ready to be released.

 * Only trivial changes of already implemented APIs may be merged without
   asking for the approval of the other partners.

 * [Breaking changes](https://en.wiktionary.org/wiki/breaking_change) to
   existing [releases][statuses] MUST be explicitly accepted by all
   the partners.

 * Non-breaking changes to existing releases MAY be deemed as implicitly
   accepted no sooner than **1 week** after they have been proposed (and no
   "veto" was received), but this time span SHOULD be extended if there is
   reason to suspect some partners may don't like the change.

 * Upgrading [draft][statuses] to a [release candidate][statuses] SHOULD be
   explicitly accepted by all the partners.

 * All [change proposals][statuses] SHOULD be accompanied by a pull request.
   Partners MUST be able to review a diff of all changes, and be allowed to
   comment on this diff somewhere.


EWP Partner Developers
----------------------

This is the list of developers who are allowed to accept the API change
proposals in the name of a partner:

* **Poland**:

  * Wojciech Rygielski - rygielski@mimuw.edu.pl
  * Michał Kurzydłowski - michalk@mimuw.edu.pl

* *(WRTODO: full list of the partners)*


Relevant external documents
---------------------------

 * [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) - strict definitions of
   keywords such as "MUST" and "SHOULD" (which we will use throughout all the
   documents).


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management/blob/master/README.md#statuses
[backward-compatibility-rules]: https://github.com/erasmus-without-paper/ewp-specs-architecture/blob/master/README.md#backward-compatibility-rules
