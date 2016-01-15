Working with EWP Technical Documentation
========================================

This document is our proposal on **how** to work with the technical
documentation within the EWP project (where to store it, how to submit change
proposals, etc.).

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


The Structure of EWP Repositories
---------------------------------

### How documentation is divided?

 * Each section of the documentation is stored in **separate repository**.

 * The index of all documents (along with their current statuses) can be found
   [at this URL][develhub]. This index SHOULD be frequently updated.

 * Some of these documents will probably not change much after their first
   release, while some others (like the APIs) will probably keep mutating
   (perhaps even after the project is finished - in a backward-compatible way).


### Why separate API repositories?

We chose to split EWP requirements into a couple of separate APIs, and host
them in separate GitHub repositories:

 * We believe that all partners should have the option to implement just
   a **subset** of all the features we have documented. This will make it
   easier for them to start off, claim that they have parts of EWP properly
   implemented, and then implement other parts later (possibly *much* later,
   by other team of developers).

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

 * It even allows the project leaders to choose and manage separate teams for
   working with separate APIs.


### Why GitHub?

We chose to use Git and GitHub as the primary tool for working and hosting API
documentation for developers:

 * All developers are familiar with Git. Many developers are also familiar with
   GitHub.

 * Git allows us to easily keep track of all the changes. Having the option
   to produce a set of changes between particular versions of the documentation
   (e.g. "what has changed between versions `1.0.0` and `1.2.7`?") is a very
   important feature, and it can be easily achieved with Git.

 * GitHub features include an integrated code review tools, issue trackers,
   change notifications, automated build tools - and many others, all useful in
   such projects (even in "documentation-only" projects).


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

 * It allows us to tag specific API versions as officially approved.

 * It allows the developers to easily determine when a breaking change occurs
   in a particular API, and adapt properly.

 * It follows [a set of quite explicit rules](http://semver.org/). Please get
   familiar with them (especially if you plan to design parts of the APIs).

 * Combined with the requirement of preparing an explicit and strict API
   specifications, it allows us to easily answer the question: **if it doesn't
   work then who's fault is that?**


### Use permalinks!

Whenever you post a link to a document somewhere, you SHOULD use a Git tag
name (or a commit ID) in the posted URL. You should avoid posting links to the
`master` branch (which can mutate, even to the point of having the link
broken).

Try pressing <kbd>y</kbd> key on GitHub site to get a permalink ([other useful
keyboard shortcuts](https://help.github.com/articles/using-keyboard-shortcuts/)).


### Backward-compatibility

 * As required by the rules of [semantic versioning](http://semver.org/), all
   [breaking changes](https://en.wiktionary.org/wiki/breaking_change) (aka
   backward-incompatible changes) SHOULD force the **major** API version number
   to be increased (e.g. `1.3.7` should become `2.0.0`).

 * API designers MUST take care of [backward-compatibility rules]
   [backward-compatibility-rules], to facilitate predictable workflow for all
   implementers.

 * Once a document is [released][statuses], backward-incompatible changes
   SHOULD be avoided (if possible).

 * All non-trivial changes (especially the backward-incompatible ones) must go
   through the proposal acceptance process, as described in the
   [Rules for Submitting API Change Proposals](#change-proposals) section.


### XML namespaces and branches

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

Once a document is [released][statuses], every subsequent release of such
document MUST be accompanied by a *changelog*. All changes SHOULD be noted in
this changelog (and *backward-incompatible* changes should be additionally
highlighted).

Please note, that this requirement is for **released** documents only, and it
does not imply the need of having a changelog for [change proposals]
[statuses]. Before accepting a proposal, a partner SHOULD review the full
diff of the proposed change.


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


<a name="statuses"></a>

Document statuses
-----------------

### Available statuses

* **DRAFT** - designers are still working on this document. It has not been
  approved, but everyone may comment on it.

* **CHANGE PROPOSAL** - A document is a copy of another document with a set of
  changes applied. The partners are asked to comment on the *changed* parts of
  the document (e.g. when compared to the latest release).

* **RELEASE CANDIDATE** - All partners have approved the contents of the
  document, but it has not been officially released yet (it has no version
  number assigned).

* **RELEASED** - All partners have approved the document and it has been
  assigned a version number (e.g. 1.0.0).

Additionally, RELEASED documents may also be:

* **OUTDATED** - The document has been made obsolete by a newer release (and
  the newer release MAY be backward-incompatible with this document).

* **DEPRECATED** - The document is at its latest version, but the entire API
  (described by this document) has been deprecated, and probably replaced by
  some other API. Such documents SHOULD explain (inside their contents) *why*
  they are deprecated, and which other APIs replace them.


### How to determine the status of a document?

The status of a document is determined from its **location and context**:

 * If a document has been tagged with a Git version tag (such as `v1.0.0`)
   in one of the official repositories, and there is no newer release of this
   document (no version with a greater tag name) then its status is
   **RELEASED**.

 * If a document has been tagged with a Git version tag, but there exists a
   newer release tag of its repository, then the document's status is
   **OUTDATED**.

 * The document is **DEPRECATED** only when its *latest release* explicitly
   states that its contents are deprecated. (This also means that it *is*
   possible to *undeprecate* a document.)

 * If a document has been merged into the `stable-*` branch of one of the
   official repositories - then the status of this documented is **RELEASE
   CANDIDATE**.

 * If a document has not been merged into the `stable-*` branch yet, but there
   already exists an appropriate open pull request for its merging - then the
   status of this documented is **CHANGE PROPOSAL**.

 * In all other cases - the document is a **DRAFT**.

"Official repositories" are the ones owned by the **erasmus-without-paper**
GitHub organization.


<a name='change-proposals'></a>

Rules for Submitting API Change Proposals
-----------------------------------------

### How to propose a change to a [draft][statuses] API?

 * Option 1. Start a new thread in our issue tracker (WRTODO: put a link to the
   tracker here.) Please make sure to select a proper project and assign a
   proper category to your ticket.

   The author of the API (and all other watchers) SHOULD watch for changes in
   their projects and should be notified when you submit a new issue to the
   tracker.

 * Option 2. You can also fork the repository, change what you want changed,
   and send a GitHub pull request. Since it's a draft, the author may merge
   such pull requests at will (he doesn't need to consult any of the partners
   yet).

   If your pull request is complicated, consider creating a separate issue page
   for tracking it. Pull requests are NOT the proper place for longer
   discussions - these SHOULD be conducted within the issue tracker.


### How to propose a change to [released][statuses] API?

 * If you're not the API author, just do the same, as with the draft APIs
   (described above).

 * If you are the API author yourself, you can push your proposed changes to a
   separate branch (or fork), then issue yourself a pull request.

 * Only trivial changes of accepted APIs may be merged without asking for the
   approval of the other partners. All non-trivial proposals SHOULD be accepted
   before merging them.


### How to get my draft (or change proposal) released?

You CANNOT assume that all partners are watching all of the issues. You
MUST contact all the partners and attempt to get their approval before you can
deem your proposal as ready to be released.

 * [Breaking changes](https://en.wiktionary.org/wiki/breaking_change) to
   existing [releases][statuses] MUST be explicitly accepted by all
   the partners.

 * Non-breaking changes to existing releases MAY be deemed as implicitly
   accepted no sooner than **1 week** after they have been proposed (and no
   "veto" was received), but this time span SHOULD be extended if there is
   reason to suspect some partners may don't like the change.

 * Upgrading [draft][statuses] to a [release candidate][statuses] MUST be
   explicitly accepted by all the partners.

 * Release candidates will be periodically upgraded to releases (and assigned
   version numbers) by project managers.

 * All [change proposals][statuses] SHOULD be accompanied by a pull request.
   Partners MUST be able to review a diff of all changes, and comment on this
   diff.


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
