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
   are aware that most of our repositories will be hosting documentation
   only, but we do find all these tools useful even in documentation-only
   projects.


Issue tracker
-------------

GitHub offers built-in issue tracking which should be entirely sufficient for
purposes of developing the software and its documentation.

Every GitHub project may have its own separate issue tracker, and we have
chosen to stick to this design decision. In other words, we will use **multiple
issue trackers**. When you're reading documentation on GitHub and you find a
bug, simply scroll to the top of the page, and click the *Issues* tab.

Pros:

 * We keep project's issues along with the project's code.
 * The *Issues* tab is always around.

Cons:

 * Issue numbers will not be unique within the entire EWP Project. When
   cross-referencing issues between sub-projects, absolute issue URLs will need
   to be used. However, since WP6 will also use a separate issue tracker (and
   we were [unable to share it]
   (https://github.com/erasmus-without-paper/general-issues/issues/1)), the
   issue numbers would not be unique *in either case*.


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

We are inclined to use XML as our primary data exchange format. We might be
persuaded towards JSON however. Further inquiry will be conducted and decisions
will be released in future versions of this document.

Regardless of what we choose, it is possible for some APIs to use some other
data formats than the "primary" ones (especially if the format is a
well-established one, for exchanging some particular type of data).


### Preferred Documentation Format

We have decided to use Markdown for text documentation. We will also use schema
languages (such as XML Schema or JSON Schema) for describing data formats in
detail.

 * **Markdown** - because it is very easy to understand even when displayed
   *raw*. This makes it a very good language to be reviewed in Git diffs.

 * **XML Schema** - because it is a well-established documentation format for
   XML, and makes it easier for developers to confirm that their documents meet
   the requirements. Schema validators are already built into many programming
   languages.

 * **JSON Schema** - not (yet?) so popular, but there are multiple validators
   on the web, available for many programming languages.


### Preferred Documentation Style

We require all API specifications to be **explicit and strict** - with lots
of "MUSTs" and "MUST NOTs" (as defined in [RFC 2119]
(https://www.ietf.org/rfc/rfc2119.txt)) and detailed explanations for all
the enumerations used). If any part of the specifications turns out to be
vague, then a new version of such specification SHOULD be released, fixing the
vague part.


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

Rules for Accepting API Change Proposals
-----------------------------------------

### How to propose a change to a document?

 * **Option 1.** Start a new thread in the issue tracker associated with this
   document (search for the *Issues* tab on the top of the GitHub page).

   The authors and maintainers of the APIs SHOULD subscribe for GitHub's issue
   notifications, and should be notified when you submit a new issue to their
   tracker.

 * **Option 2.** You MAY also [fork](https://guides.github.com/activities/forking/)
   the repository, change what you want changed, and send a pull request.

   If your pull request is complicated, consider creating a separate issue page
   for tracking it. Pull requests are NOT the proper place for longer
   discussions - such discussions SHOULD be conducted within the issue tracker.


### How to get my draft (or change proposal) released?

These rules apply to developers with write-permissions to official EWP
repositories. Developers MUST follow these rules whenever they want to release
a new version of a document.

 * All [change proposals][statuses] SHOULD be accompanied by a [pull request]
   (https://help.github.com/articles/using-pull-requests/). Partners MUST be
   able to review a diff of all changes, and be allowed to comment on this diff
   somewhere.

   * This is also true when releasing [drafts][statuses] - e.g. if the draft is
     present in the `master` branch, then you should issue yourself a pull
     request to the `stable-*` branch.

 * Only trivial changes of already implemented APIs may be released without
   previously asking for the review of the other partners.

 * You CANNOT assume that all partners are watching all GitHub issues and/or
   pull requests. Whenever you mean to contact the partners, you MUST do so
   either directly, or via the technical@erasmuswithoutpaper.eu mailing list.

 * Whenever you contact the partners and ask for their review, you MAY give
   them a **deadline** for such review. After such deadline is reached, it MAY
   be assumed that all the partners who did not respond gave you their
   approval.

   * Deadlines should vary on the nature of the change. E.g. A one-week
     deadline might be enough for non-breaking changes, but
     [breaking changes](https://en.wiktionary.org/wiki/breaking_change) to
     [already released][statuses] documents may need a longer deadline.

   * If there is a strong reason to suspect that some partners may don't like
     the change (e.g. you know the implementation has already started), you
     SHOULD attempt to contact them directly and get their *explicit* approval.


[develhub]: http://developers.erasmuswithoutpaper.eu/
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management/blob/stable-v1/README.md#statuses
[backward-compatibility-rules]: https://github.com/erasmus-without-paper/ewp-specs-architecture/blob/stable-v1/README.md#backward-compatibility-rules
