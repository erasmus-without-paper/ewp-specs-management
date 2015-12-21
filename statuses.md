Document statuses
=================

[What is the status of this document?](statuses.md)


Available statuses
------------------

* **DRAFT** - A designer (or a small group of designers) are still working on
  this document. It has not been approved (nor anyone was asked to approve it),
  but - since it's online - everyone may comment on it.

* **CHANGE PROPOSAL** - A document is a copy of another document with a set of
  changes applied. The partners are asked to comment on the *changed* parts of
  the document.

* **RELEASE CANDIDATE** - All partners have approved the contents of the
  document, but it has not been officially released yet (it has no version
  number assigned).

* **RELEASED** - All partners have approved the document and it has been
  assigned a version number (e.g. 1.0.0).

* **OUTDATED** - The document has been made obsolete by a newer release (and
  the newer release MAY be backward-incompatible with this document).


How to determine the status of a document?
------------------------------------------

The status of a document is determined from its **location and context**:

 * If a document has been tagged with a Git version tag (such as `v1.0.0`)
   in one of the official repositories, and there is no newer release of this
   document (no version with a greater tag name) then its status is
   **RELEASED**.

 * If a document has been tagged with a Git version tag, but there exists a
   newer tag of this document, then its status is **OUTDATED**.

 * If a document has been merged into the `stable` branch of one of the
   official repositories - then the status of this documented is **RELEASE
   CANDIDATE**.

 * If a document has not been merged into the `stable` branch yet, but there
   already exists an appropriate open pull request for its merging - then the
   status of this documented is **CHANGE PROPOSAL**.

 * In all other cases - the document is a **DRAFT**.

Official repositories are the ones owned by the **erasmus-without-paper**
GitHub organization.
