Rules for Submitting API Change Proposals
=========================================

[What is the status of this document?](statuses.md)


How to propose a change to an [draft](statuses.md) API?
----------------------------------------------------------------

Every API repository has an integrated issue tracker:

 * The author of the API (and all other watchers) will be notified when you a
   submit a new issue to the tracker.

 * If you want, you can also fork the repository and attach a pull request to
   your issue. Since it's a draft, the author may merge such pull requests at
   will (he doesn't need to consult any of the partners yet).


How to propose a change to [released](statuses.md) API?
----------------------------------------------------------------

 * If you're not the API author, just do the same, as with the draft APIs
   (described above).

 * If you are the API author yourself, you can push your proposed changes to a
   separate branch (or fork), then issue yourself a pull request.

 * Only trivial changes of accepted APIs may be merged without asking for the
   approval of the other partners. All non-trivial proposals SHOULD be accepted
   before merging them.


How to get my [draft](statuses.md) or [change proposal](statuses.md)
[released](statuses.md)?
--------------------------------------------------------------------

You CANNOT assume that all partners are watching repository's issues. You
MUST contact all the partners **directly** before you can deem your proposal as
ready to be released.

 * [Breaking changes](https://en.wiktionary.org/wiki/breaking_change) to
   existing [releases](statuses.md) MUST be explicitly accepted by all
   the partners.

 * Non-breaking changes to existing releases MAY be deemed as implicitly
   accepted no sooner than **1 week** after they have been proposed (and no
   "veto" was received), but this time span SHOULD be extended if there is
   reason to suspect some partners may don't like it.

 * Upgrading [draft](statuses.md) to a [release candidate](statuses.md) MUST be
   explicitly accepted by all the partners.

 * All [change proposals](statuses.md) MUST be accompanied by a pull request.
   Partners MUST be able to review a diff of all changes, and comment on this
   diff.


How to contact the partners "directly"?
---------------------------------------

*To be decided.*
