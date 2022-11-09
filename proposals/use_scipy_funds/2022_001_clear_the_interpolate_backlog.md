#  Clearing up the `scipy.interpolate` backlog

Proposal details:

- Title: Clearing up the `scipy.interpolate` backlog
- Author: Evgeni Burovski, Ralf Gommers
- Date: Apr 25, 2022
- Cost: $10,000
- Time duration: Two months: 16 May 2022 - 17 July 2022
- Team members: Evgeni Burovski, Matt Haberland
- Link to public discussion: https://mail.python.org/archives/list/scipy-dev@python.org/thread/V5ADHAFNZIRTQXZL5DHGXA7NDT5DELRS/


## Context

As a community-driven project, SciPy primarily relies on volunteers. This includes
proposing and implementing new functionality, reporting and fixing
issues in existing code, and reviewing pull requests. While generally our
overall approach works great, relying on ''nights and weekends'' effort has two limitations.
First, volunteers naturally tend to concentrate on "fun" parts of the work,
mostly related to writing new code. Second, volunteer time budget is limited
*and quantized*. This, in turn, severely limits the scope of topics volunteers
can work on. Large features---and large review efforts---which require a
concentrated work of more than a couple of hours, tend to slide into the backlog.

Our backlog is currently more then 300 open PRs and more then a thousand issues 
and keeps growing. While the backlog is not a problem per se, issues and PRs
which just keep lingering for years are. Some of these long-standing issues
are just too localized and/or low-prio. Some, however, are different. There are
two kinds of problems:

 - Long-lived issues which require more than a typical volunteer time quantum.
   These issues often involve decades-old Fortran 77 code, handwritten C API glue,
   or other obscure issues, and often involve non-trivial backwards compatibility
   considerations. The sheer amount of triaging and debugging required to fix
   these sorts of issues often exceeds a volunteer time budget, and issues just
   keep sitting in the backlog and are being regularly pinged on by users who
   run into them---for years on end. 

 - Large PRs, which bring good, wanted functionality. Small maintenance
   PRs are typically reviewed and merged quickly. OTOH, large PRs with large
   amounts of algorithmic code tend to require non-trivial review effort---which
   exceeds the volunteer maintainer time budget, and PRs linger, also for years
   on end. After a while a frustrated PR author simply leaves, and a PR requires
   even more work to review and finish up. And we lose a potential contributor and
   possibly even a good future maintainer candidate.

These kinds of items---thorny bugs in obscure code and large algorithmic PRs---
are difficult to tackle within purely self-organized volunteer effort, and
we propose to supplement our business as usual with a more structured and
concentrated approach with work allocations earmarked per scipy subpackage.
We acknowledge that many such issues do get addressed, and SciPy is and will
likely remain a primarily volunteer-driven project. There are gaps however, and
now that SciPy has a sustainable (if modest) income stream, we propose to
address those gaps where we can for submodules that are widely used.
A public discussion of a big picture, including the topic of this proposal,
can be found in the email thread discussion at [1].

In this proposal we start with `scipy.interpolate`, because it's a widely used
module and has no active maintainer with domain expertise *and* enough bandwidth
at the moment.

[1] https://mail.python.org/archives/list/scipy-dev@python.org/thread/V5ADHAFNZIRTQXZL5DHGXA7NDT5DELRS/
[2] https://docs.scipy.org/doc/scipy/dev/roadmap-detailed.html


## Goals

The overall goals of this effort are to analyze the backlog of
`scipy.interpolate`, identify issues and PRs which are difficult to fix/review
by the self-organized volunteer effort, and fix/review them. We expect that
this brings the subpackage backlog down significantly.
For other issues, add triage comments as needed, for example regarding the
solution direction, whether it's an issue a new contributor may be able to
tackle, or about its relative importance.

The following are non-goals:
  - bring the open issue count to zero. This is neither realistic not necessary.
  - undertake large R&D efforts for new functionality (e.g. ''replace FITPACK
    with a better alternative'', https://github.com/scipy/scipy/issues/2579).
    While these enhancements are definitely wanted and are hard for a
    volunteer-only effort, such new large features are out of scope for this
    project.


## Deliverables

The deliverables are, in order of priority:

1. Review, finalize and merge or reject all open PRs for `scipy.interpolate`
   subpackage. There are 11 in total, the oldest ones dating back to 2014 and 2017.
   Some of these PRs require work to finish up, and the original authors are not
   always available.
2. Analyze open issues in `scipy.interpolate`, select the ones which are difficult
   to fix by the self-organized volunteer effort, and fix them. We expect this
   to bring the subpackage backlog down significantly.
3. Review ongoing work in `scipy.interpolate` (there is at least one pull
   request in progress to bring the GCV splines reimplementation; the work
   itself is not a part of this project; reviewing the PR if it arrives is).
4. Update the detailed roadmap for `scipy.interpolate` to reflect the results of
   this project.
5. Contact fortran-lang organization and other interested parties on possible
   maintenance of FITPACK and other Fortran components.
6. Clean up `interpolate` usage in other subpackages, primarily in `signal`.
   Possibly remove/deprecate duplicated functionality, per SciPy detailed
   roadmap [2]. This, in particular, includes b-splines in `scipy.signal`
   (the roadmap item is "B-splines: ... Move the good stuff to interpolate (with
   appropriate API changes to match how things are done in interpolate), and
   eliminate any duplication.")


## Expected benefits

- Fix long-standing issues in `scipy.interpolate`, some of which have been
  open for years.
- Review, finish up and merge long-standing pull requests, some of which have
  been open for years.


## Why should this be a funded activity?

For two reasons:

1. Long-open pull requests simply are not being reviewed with purely volunteer
   effort, and
2. Long-open issues simply do not get fixed with purely volunteer effort.

In general, it's not easy to find the expertise and availability for doing this
work. Currently Evgeni Burovski is available, and he has the right combination
of domain expertise and familiarity with SciPy internals.

