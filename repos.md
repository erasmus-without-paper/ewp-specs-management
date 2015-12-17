The Structure of EWP Repositories
=================================

[What is the status of this document?](statuses.md)


Why GitHub?
-----------

We chose to use GitHub as the primary tool for working and hosting API
documentation for developers:

 * All developers are familiar with Git. Many developers are also familiar with
   GitHub.

 * GitHub allows us to easily keep track of all the changes. Having the option
   to diff the changes in the documentation (e.g. "what has changed between
   versions 1.0.0 and 1.2.7?") is a very important feature.

 * GitHub features include an integrated code review tools, issue tracker,
   change notifications, automated build tools... and many others, all useful
   in such projects (even in documentation-only projects!).


Why separate API repositories?
------------------------------

We chose to split EWP requirements into a couple of separate APIs, and host
them in separate GitHub repositories:

 * We believe that all partners should have the option to implement just
   a **subset** of all the features we have documented. This will make it
   easier for them to start off, claim that they have parts of EWP properly
   implemented, and then implement other parts later (possibly much later, with
   other teams of developers).

 * Having each API in **separate repository** has some great advantages, when
   it comes to versioning:

   - If a partner does not implement *API X*, then he also knows that he may
     ignore all the changes in *API X*'s repository.

   - If a partner have already implemented *API Y* and wants to upgrade his
     implementation to include some new changes in new API release, he may
     simply review a diff (and/or release notes) in the Git repository between
     specific tags.

   - It allows us to use [semantic versioning](http://semver.org/) separately
     on each API. This allows the partners to easily spot backward-incompatible
     changes which may break their implementations.

 * It allows the project leaders to choose separate teams for working with
   separate APIs. Each team will have its own issue tracker and will be in
   charge of assigning Git push permissions.
