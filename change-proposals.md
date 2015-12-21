Rules for Submitting API Change Proposals
=========================================

[What is the status of this document?](statuses.md)


How to propose a change to a [draft](statuses.md) API?
------------------------------------------------------

 * Option 1. Start a new thread in our issue tracker (TODO: the location of the
   tracker is yet to be agreed upon.) Please make sure to select a proper
   project and assign a proper category to your ticket.

   The author of the API (and all other watchers) SHOULD watch for changes in
   their projects and should be notified when you submit a new issue to the
   tracker.

 * Option 2. You can also fork the repository, change what you want changes,
   and send a GitHub pull request. Since it's a draft, the author may merge
   such pull requests at will (he doesn't need to consult any of the partners
   yet).

   If your pull request is complicated, consider creating a separate issue page
   for tracking it. Pull requests are NOT the proper place for longer
   discussions - these SHOULD be conducted within the issue tracker.


How to propose a change to [released](statuses.md) API?
-------------------------------------------------------

 * If you're not the API author, just do the same, as with the draft APIs
   (described above).

 * If you are the API author yourself, you can push your proposed changes to a
   separate branch (or fork), then issue yourself a pull request.

 * Only trivial changes of accepted APIs may be merged without asking for the
   approval of the other partners. All non-trivial proposals SHOULD be accepted
   before merging them.


How to get my `draft` or `change proposal` `released`?
------------------------------------------------------

You CANNOT assume that all partners are watching all of the issues. You
MUST contact all the partners **directly** before you can deem your proposal as
ready to be released.

 * [Breaking changes](https://en.wiktionary.org/wiki/breaking_change) to
   existing [releases](statuses.md) MUST be explicitly accepted by all
   the partners.

 * Non-breaking changes to existing releases MAY be deemed as implicitly
   accepted no sooner than **1 week** after they have been proposed (and no
   "veto" was received), but this time span SHOULD be extended if there is
   reason to suspect some partners may don't like the change.

 * Upgrading [draft](statuses.md) to a [release candidate](statuses.md) MUST be
   explicitly accepted by all the partners. Release candidates will be
   periodically upgraded to releases (and assigned version numbers) by project
   owners.

 * All [change proposals](statuses.md) MUST be accompanied by a pull request.
   Partners MUST be able to review a diff of all changes, and comment on this
   diff.


How to contact the partners "directly"?
---------------------------------------

*To be decided.*
