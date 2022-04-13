#  Accelerating the move to Meson as the SciPy build system

Proposal details:

- Title: Accelerating the move to Meson as the SciPy build system
- Author: Ralf Gommers
- Date: 4 July, 2021
- Cost: $12,000
- Time duration: 3 months
- Team members: Matthew Brett (funded), Ralf Gommers (unfunded), Gagandeep Singh (unfunded), Smit Lunagariya (funded)
- Link to public discussion: https://mail.python.org/archives/list/scipy-dev@python.org/message/4S43BYHDQIPQENNJ6EMQY5QZDZK3ZT5I/


## Context

Multiple people recently told me that our current build system and CI issues
are a pain point for working on SciPy. We have CI timeouts on our main repo,
scipy-wheels is a pain, conda-forge is also timing out on aarch64 and ppc64le
build. And I've found myself spending a whole day or weekend several times in
the past months to fix broken CI jobs due to build/packaging issues.

About 4 months ago, I wrote an RFC to move to Meson as a build system, see
https://github.com/scipy/scipy/issues/13615. Since then I have spent a lot of
time on this, and also used Quansight Labs funding to get one of my
colleagues, Gagandeep Singh, to help me move this forward faster (and he has
been super helpful). Getting a Linux + OpenBLAS dev build is close to done
(16 of 20 modules complete, all that's left is `misc`, `io`, `integrate` and
`signal` - probably those can be completed in the coming week).

Doing everything else, like adding support for Windows/aarch64/MKL/ILP64/etc.
is still a lot of work. There's a tracking issue at
https://github.com/rgommers/scipy/issues/22. Some of this stuff is pretty
specialized, e.g., building wheels, and Fortran-on-Windows. It will take a
long time to complete if it's just me spending time on the weekends.

Matthew Brett is available to help soon. He has written `multibuild` and
dealt with build/packaging topics for a long time, so I think he would be
able to make progress quickly. He wants to work on this topic as an
independent contractor (I won't add rates here, that's for the core team to
look at - but they're very reasonable).


## Goals

The overall goals of this effort are:

1. Get a (mostly) feature-complete Meson based build system in place by the
   end of October, so we can ship it in the 1.8.0 release. If all goes well,
   get rid of the `numpy.distutils` based build 1 release later.
2. Resolve all our CI timeout issues. If the build system alone isn't enough
   (it should be though), analyze the remaining issues and figure out how to
   tackle whatever is still problematic.


## Deliverables

The deliverables are, in order of priority:

1. Add capability to build release artifacts (wheels, sdist). I did some
   initial tests at the start with `mesonpep517`, but I have no idea if it
   works for SciPy and what bugs are lurking there.
2. macOS support
3. Add support for things we need to a `dev.py` interface (basically, like
   runtests.py in that it can do everything, like building docs, running
   benchmarks, etc.)
4. Contribute a few things we need, or that would make the build setup
   better, to Meson. For example, I think we'd want to be able to use
   `py3.install_sources` on generated targets. Of course I'm still new-ish to
   Meson, so it could well be that after making a proposal on the Meson issue
   tracker, another solution will be preferred.
5. Windows support
6. Improve build dependency detection and configuration - in particular
   BLAS/LAPACK flavors.
7. Clean up as many build warnings as possible, and silence the rest. The
   goal is to have a CI job that is completely silent (passes with `-Werror`).
8. Optimize build time further, including on CI (e.g., reuse build cache
   between jobs).

I'd like to use 75% of the funds to pay Matthew, and 25% of the funds to take
on a talented intern, Smit Lunagariya. He is comfortable working in Python, C
and C++, and will be able to help with deliverables 7 and 8, as well as with
testing and other tasks.

Overall I'm not certain that this amount of funds is enough to complete every
last deliverable on this list; it's hard to estimate. But we should certainly
get close, and be able to ship a Meson build in 1.8.0.


## Expected benefits

For a quick sketch of the benefits:

- On my machine the build time is currently 13 minutes with numpy.distutils
  and 90 seconds with Meson
- The build log goes from >10,000 lines (mostly noise) to ~100 lines (mostly
  configuration info).


## Why should this be a funded activity?

For two reasons:

1. Build and CI issues are probably the number one maintenance issue we have, and
2. Most people find working on build/CI boring and painful, and hence it
   doesn't happen with volunteer-only activities. Even regular maintenance of
   our CI is hard - recently jobs have been broken for 1-2 weeks at a time a
   couple of times. And the `scipy-wheels` repo is in even worse shape.

My proposal is to designate this topic as high priority, let the core team
approve the compensation levels for the funded people, and get the work
started. For reporting on progress and to have some accountability about how
we spent the funds, I propose a short report (say 1 page, giving a status
update and linking the main PRs made or issues closed) when half the funds
are spent, and another such report at the end.
