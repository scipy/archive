---
tags: SciPy, meeting
---

# 2023 SciPy Community Meeting

- Next meeting: **December 13th, 2023 (Wednesday) @2pm UTC**
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.
- Meeting notes archive at https://github.com/scipy/archive/tree/main/community_meetings

### Code of Conduct

We want to take a moment to remind you that this meeting, like all project spaces is meant to be open, welcoming, diverse, inclusive, and it's important for us to have a healthy community. Like all SciPy spaces, and everyone participating in them, this meeting will follow our [code of conduct](http://scipy.github.io/devdocs/dev/conduct/code_of_conduct.html). If you haven't read it yet, please take some time to do so later on as it already applies to you. For now, in short, please be kind and generous towards one another.

## Agenda for December 27th, 2023

**Present:** Melissa (@melissawm), Jake (@j-bowhay), Lucas (@lucascolley)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Lucas] M1 Mac + `venv` build issues
    - I reproduced issues that someone was running into during the PyLadies sprint by following the `venv` build instructions.

- [name=Lucas] `-pie being ignored` build warnings
    - Any idea where they're coming from?
    - https://github.com/scipy/scipy/issues/19736

- [name=Lucas] Directing to `development` version of the contributor docs from other versions
    - +1 from Pamphile and Ralf, but how to go about it?
    - https://github.com/scipy/scipy/issues/19699

- [name=Lucas] Incorrect test in `cluster`
    - Looks like a typo, although errors are introduced on fixing it.
    - https://github.com/scipy/scipy/issues/19683

- [name=Lucas] DX PR: `requirements/*.txt` files
    - Ralf gave initial review, ready for another look.
    - Based on the script used in skimage and numpydoc. 
    - https://github.com/scipy/scipy/pull/19750

- [name=Jake] https://github.com/scipy/scipy/issues/19223 


## Agenda for December 13th, 2023

**Present:** Lucas (@lucascolley), Evgeni (@ev-br)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Lucas] My PRs/Issues
    - Incorrect test in `cluster` - seems to fail after correction: https://github.com/scipy/scipy/issues/19683
    - Improving array API test skip decorators (sort of blocked on the above): https://github.com/scipy/scipy/pull/19682
    - `linalg` array API - waiting for Ralf or Ilhan: https://github.com/scipy/scipy/pull/19260

- [name=]

## Agenda for November 29th, 2023

**Present:** Melissa Mendonça (@melissawm), Lucas Colley (@lucascolley), Aditya Mohan (@amohan826), Tyler

- [name=Lucas] Sprint Prep
    - Triage plan/strategy?
    - I added some implementation options to https://github.com/scipy/scipy/issues/19181
    - Benchmarks issue https://github.com/scipy/scipy/issues/19596
    - https://hackmd.io/@melissawm/scipy-sprint
    - Announce on the mailing list

- [name=Lucas] My PRs
    - Closing the 'private but present' deprecation issue - waiting for an opinion from Axel (https://github.com/scipy/scipy/pull/19585)
    - `linalg` array API - ready for a look from Ralf or Ilhan (https://github.com/scipy/scipy/pull/19260)
    - Restricting input dtypes to subdtypes of `np.number` and `np.bool_` (https://github.com/scipy/scipy/pull/19606)

- [name=Lucas] Anything need help for 1.12?
    - Branching Dec 6, still a few things open

- [name=] Add your item here!

## Agenda for November 15th, 2023

**Present:** Melissa Mendonca, Lucas Colley, Ralf Gommers

- [name=Melissa, Kai] SciPy sprint with PyLadies Berlin :tada:
    - https://www.meetup.com/pyladies-berlin/events/297275969/?isFirstPublish=true
    - Kai, Melissa and Lucas will mentor folks during the sprint
    - [name=Lucas] could try to work out some actionable options on https://github.com/scipy/scipy/issues/19181? Also line length stuff as below

- [name=Lucas] A few PRs to draw attention to if anyone's interested :)
    - Adding a `[lint only]` skip tag for CI - is there a way to do it without all of the new 'get commit message' jobs? https://github.com/scipy/scipy/pull/19497
        - Might be possible to re-use logic to add a [docs only] skip tag later.
    - Enabling `PyUpgrade` rules in the linter (Stefan's idea) - will do a full pass for formatting  https://github.com/scipy/scipy/pull/19516
    - We are now enabling the line length check in CI submodule-by-submodule (thanks Jake and Matt!!) - perhaps make a tracker issue once PRs are in for`fft` and `constants` (might be useful for sprint)? Or leave in background if it's been too much of a STY overload recently 😅 https://github.com/scipy/scipy/issues/19479
        - Might be simpler to group things together and put in few PRs to sort out groups of submodules at a time.

- [name=Lucas] Array API - Charlie (ruff maintainer) is happy in principle with a ruff rule for migrating from `np` to `xp` (array-agnostic) https://github.com/astral-sh/ruff/issues/8615. Would be  helpful for SciPy and even more so for other projects. Won't be done before https://github.com/numpy/numpy/issues/25076 and likely for long after. (Scope to expand beyond NumPy too).

## Agenda for November 1st, 2023

**Present:** Ralf (@rgommers), Lucas (@lucascolley), Tyler, Melissa (@melissawm), Jake (@j-bowhay)

- [name=Ralf] Update on BLAS/LAPACK support
    - Lots of complaints on NumPy, not so many on SciPy
    - Might be able to get all fixes in meson before the next SciPy release, but not sure.
- [name=Ralf] Wheels for new Accelerate - 8 MB smaller
- [name=Tyler] Do we wait for NumPy 2.0 for next release?
    - Might do a 1.12 around December and 1.13 when NumPy 2.0 comes out
- [name=Jake] Optional dependencies, how to track how many people use them?
    - Bug reports mostly
    - Related to https://github.com/ashvardanian/simsimd
- [name=Lucas] Line length follow-up


## Agenda for October 18th, 2023

**Present:** Melissa (@melissawm), Daniel (@dschmitz89)

- [name=Melissa] Docs build times
- [name=Daniel] Interactive docs 

## Agenda for October 4th, 2023

**Present:** Melissa (@melissawm), Lucas (@lucascolley), Tyler (@tylerjereddy)

- [name=Melissa] https://github.com/scipy/scipy/pull/16660
    - New version of pydata-sphinx-theme still doesn't resolve the performance issue, but there may be improvement. Melissa will also run tests
- [name=Tyler] Python 3.12 is out, but things seem to be smooth
- [name=Lucas] After the [ruff rules for NumPy 2.0](https://github.com/astral-sh/ruff/pull/7702), there has been discussion (on the Scientific Python discord) about rules for array API

## Agenda for September 20th, 2023

**Present:** Jake (@j-bowhay), Lucas (@lucascolley), Daniel (@dschmitz89)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Lucas] Return dtype consistency/testing
    - Better documentation for expected return dtype?
    - Test multiple dtypes
- [name=Daniel] Interactive documentation
    - https://discuss.scientific-python.org/t/making-docstring-examples-interactive/812
- [name=Lucas] Array API: FFT merged, linalg in progress
    - Blog post to explain process coming soon


## Agenda for September 6th, 2023

**Present:** Lucas (@lucascolley), Melissa (@melissawm), Tyler (@tylerjereddy)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Melissa] NumFOCUS Summit: any special topics?
- [name=Melissa] New Contributors Meeting September 15 at 12pm UTC - who can host?
- [name=Lucas] Update on array API work
    - A few small PRs with help from the group
    - https://github.com/scipy/scipy/pull/19186
        - Pending on decision/consensus
    - https://github.com/scipy/scipy/pull/19187
        - Close to merge
    - https://github.com/scipy/scipy/pull/19005
        - Could use another look
    - https://github.com/scipy/scipy/pull/19194
    - `scipy.linalg`: restrict to smaller scope + tests to make review easier. PR coming soon
    - `lazywhere`: ready to merge
- [name=Lucas] Will write a blog post on array API work for SciPy
    - Might be helpful for others working on implementing array API for other submodules

## Agenda for August 23, 2023

**Present:** Lucas (@lucascolley), Melissa (@melissawm), Ralf (@rgommers), Jake (@j-bowhay)

- [name=Kai] Sprint at EuroSciPy
    - A few issues with building and developer docs. Will try to share later.
    - In particular, https://github.com/scipy/scipy/issues/19085
- [name=Melissa] New time for this meeting: 2pm UTC
- [name=Lucas] https://github.com/scipy/scipy/issues/19068
    - SciPy functions which work with NumPy arrays will still be there, but new functions will be added.
    - What happens if a contributor wants to add new functions?
    - The new functionality is hidden behind a flag, so it shouldn't impact any PRs in progress. As long as NumPy-compatible best-practices are followed, nothing should change.
    - If this feature is to become the default, we should make sure it is easy for contributors to use it.
- [name=Melissa] Benchmarking (new contributor request): any pointers on what to work on?
    - https://github.com/scipy/scipy/pull/19052 should fix CI
    - Benchmarks for optimize can be tricky, because they take a long time to run (especially global optimizers)
    - May be useful to look at
        - https://github.com/scipy/scipy/issues/18566
        - https://github.com/scipy/scipy/pull/19060 -> benchmarks for this might be useful

## Agenda for August 9, 2023

**Present:** Tyler (@tylerjereddy), Lucas (@lucascolley), Jake Bowhay (@j-bowhay), Anirudh Dagar

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Melissa] Community meeting time/poll
    - http://whenisgood.net/kfd94pw
- [name=Tyler] SciPy release `1.11.2` planning
    - Python `3.12` shims?
    - NumPy "silent deprecation" backports?
    - musl/alpine wheel support backports? 
- Discussion of `fft` array API by Lucas

* * *

## Agenda for July 26, 2023

**Present:** Melissa (@melissawm), Pamphile (@tupui), Ralf (@rgommers), Kai (@kai-striega), Christian (@lorentzenchr), Jonathan, Evgeni (@ev-br)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Ralf] Editable installs in `dev.py`, and if so then as an option or as the default?
    - Previously we had a combination of `python setup.py` and `runtests.py`, as a convenience tool
    - When switching to Meson, `dev.py` is the replacement for `runtests.py`. Editable builds were not possible before with Meson, but they are now.
    - Proposal is to use editable installs as the default (or as an option) for `dev.py`. This could create issues for advanced use-cases, but they are avoidable issues.
    - Pamphile mentions an outstanding issue with npz files (referencing the wrong location.) This may be a fundamental limitation of editable builds, and one should avoid using `__file__` and `__path__` in that case.
    - Evgeni mentions it might be better to have editable installs and regular builds separate (i.e. not include editable installs machinery to `dev.py`)
    - [`spin`](https://github.com/scientific-python/spin) could be an option for the future, as long as functionality is intact
    - Adding as an option to `dev.py` sounds reasonable for now.

- [name=Christian] Isotonic regression [PR #17722](https://github.com/scipy/scipy/pull/17722). Anything left to do? Continue to make it univariate curve fitting, i.e. iso.fit(x, y)?
    - Pamphile mentions Matt may be interested in univariate curve fitting because of cdf fitting
    - Evgeni has been the lead reviewer and mentions the univariate curve fitting could be reasonable for scipy.interpolate
    - Andrew, Dan, Matt are the most active folks in optimize so they may want to take a look at #17722 before merging.
    - The univariate curve fitting is already implemented in scikit-learn and would stay there. The question is whether we *also* want this on SciPy (as an improved version of the implementation)

- [name=Melissa] Can we make the community meetings more effective/attractive?
    - Could we have thematic meetings? Release party? PR party? Triage meetings?
    - We could make the meetings shorter (30 mins) as they happen often enough.
    - Having an agenda beforehand would be helpful to have more focused agendas.
    - We could also have presentations on recently added methods/projects.
    - Use polls for meeting times/day.

- [name=Pamphile] [SPECS](https://github.com/scientific-python/specs), https://scientific-python.org/specs/
    - We are endorsing SPECs 0, 1 and 4
    - Open to feedback on endorsement and what this means (improvements to text are in the works)

* * *

## Agenda for June 28, 2023

**Present:** Kai Striega (@kai-striega), Pamphile Roy (@tupui), Ralf Gommers (@rgommers), Alvaro Valdes, Dhanusshya Raghu, 

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Melissa] [Licensing issue](https://github.com/scipy/scipy/issues/18765)
    - Top prio is removing GPL-licensed code
    - Should be pointed to new maintainers
    - Should we introduce SPDX headers in all files? Using https://reuse.software/
        - Pamphile to open an issue
- [name=Pamphile] Release is ok, a few regressions but taken care of.
    - Pending: https://github.com/scipy/scipy/pull/18644
    - [name=Ralf] Related: scipy.sparse needs a more defined roadmap and plan for updates
- [name=Pamphile] Array API close to be a thing: [PR 18668](https://github.com/scipy/scipy/pull/18668)
    - Still need to document the transition and plan. Then send a final email to the list for merge.
- [name=Melissa] We will cancel the next meeting (July 12) as a lot of people will be at [SciPy Conf](https://www.scipy2023.scipy.org/)
    - Melissa will send a note to the mailing list and cancel meeting on the calendar.

* * *

## Agenda for June 14, 2023

**Present:** Melissa (@melissawm), Ralf (@rgommers), Tyler 
(@tylerjereddy), Pamphile (@tupui), Matt (@mdhaber), Gideon (@ggkogan)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Pamphile] Array API support: [PR 18668](https://github.com/scipy/scipy/pull/18668) 
    - Requesting feedback and comments
    - Docs update is needed
- [name=Gideon] How are PRs/new features prioritized?
    - Specifically: https://github.com/scipy/scipy/issues/14783
    - Reviewers are hard to find, and things fall through the cracks. 
    - Related: https://github.com/scipy/scipy/pull/15519
    - Needs review, comments, feedback.
- [name=Pamphile] NumFOCUS summit: 2 spots, who wants to go?
    - Pamphile to send an email to the core mailing list and see who is interested
- [name=Pamphile] New place for nightly (weekly) wheels https://anaconda.org/scientific-python-nightly-wheels/scipy
    - Restricts access to those who can upload (related to [SPEC 4](https://scientific-python.org/specs/spec-0004/))
- [name=Ralf] Last call for removal of Docker images: https://github.com/scipy/scipy/issues/18623
- [name=Ralf] OpenBLAS on CI
    - There are no explicit tests for OpenBLAS on CI
    - Should we build from source on CI to make sure we capture any regressions early?
    - There is some bandwidth/funding for that currently through a Sovereign Tech Fund grant
    - This would be run from the pre release job




* * * 


## Agenda for May 31, 2023

**Present:** Melissa (@melissawm), Ralf (@rgommers), Evgeni (@ev-br), Jake (@j-bowhay), Dhanusshya Raghu

- [name=Melissa] AUTOSOL https://github.com/scipy/scipy/pull/12755
    - any path forward?
    - there is a separate package on pypi (that requires old scipy) but works.
- [name=Melissa] ndimage: https://github.com/scipy/scipy/pull/18170
    - Who can we ping for a review?
    - Ralf can review, but we can ping Greg Lee
- [name=Tyler] Any last-minute concerns about the RC1 release scheduled for May 31?
    - all good!
- [name=Jake] Using None to trigger deprecation warnings
    - Needs deprecation docs update
- [name=Evgeni] Why is the MyPy CI check not coupled with linting?
    - Probably because the MyPy check is slow, and linting blocks other checks from running
    - Currently it is attached to another (unrelated) job, could be moved to its standalone job or to the linting check.
- [name=Evgeni] testing notebooks
    - Melissa to check for latest tool to test notebook output
    - Evgeni suggests putting that in refguide check
- [name=Melissa] *Add your items here*


## Agenda for May 17, 2023

**Present:** Melissa Mendonça (@melissawm), Tyler Reddy (@tylerjereddy), Ralf Gommers (@rgommers), Stéfan van der Walt (@stefanv), Jake Bowhay (@j-bowhay)


- [name=Ralf] Policy on (no) new Fortran additions?
    - New components are sometimes proposed (e.g., optimizers in https://github.com/scipy/scipy/issues/18118), but based on recent experience, should be require translating to C/C++/Cython (or Python of course, if possible)? 
    - What about existing Fortran code?
    - Fortran version doesn't really matter (new versions are harder to wrap with f2py, but it may be nicer to maintain)
    - There is existing effort to rewrite some Fortran code into cython/pure Python.
    - LFortran might be a solution in the future, but right now it is still in development.
    - Follow up at a later meeting.
- [name=Tyler] 1.10.2 Release
    - 1.11 will branch in a few weeks
    - No blockers for either
    - Keeping setup.py for 1.11, and probably delete later as soon as conda-forge on windows is figured out
    - Ralf working on BLAS/LAPACK build
    - Cython memoryviews/LAPACK PR reverted, some const changes left. Should not be an issue as long as there is nothing left on pxd files.
- [name=Stéfan] Scientific Python Developer Summit next week :tada: 
    - Next week we may see some work on sparse
    - Goal is deprecating matrices
    - Discussion on the status of the C++ code: switching around matrix and array data structures, and then eventually deprecating `*_matrix` should work. Note that the code isn't very featureful, and compared to PyData/Sparse, PyTorch, TACO and MLIR, it's not a good base to build on - so "maintenance mode with at best a couple added features" is probably the right way to treat it.



## Agenda for May 3, 2023

**Present:** Melissa Mendonça (@melissawm), Pamphile Roy (@tupui), Ralf Gommers (@rgommers), Evgeni Burovski (@ev-br), Jake Bowhay (@j-bowhay)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Melissa/Pamphile] Unclear what is happening with the parallel doc build, it's a Sphinx race condition apparently. Not top priority.
- [name=Pamphile] Outstanding items for 1.11?
    - No blockers for branching end of May
- [name=Evgeni] We need to activate intersphinx for the notebooks
    - Melissa will work on it
- [name=Evgeni] dev.py interface
    - Who owns it? -> same as many other parts of SciPy without a dedicated maintainer
    - https://github.com/scipy/scipy/issues/16452
    - We should plan for maintenance
    - There is also `spin`, from the scientific python folks, but it's still in development.


## Agenda for April 19, 2023

**Present:** Pamphile Roy (@tupui), Ralf Gommers (@rgommers), Anirudh Dagar, Evgeni Burovski (@ev-br), Tyler Reddy (@tylerjereddy), Praveer Nidamaluri, Steven Gough-Kelly (@steventgk), Leo Mensah (@leomensah)

- [name=Ralf] Discussion restructure of "building from source" docs (see [gh-18239](https://github.com/scipy/scipy/issues/18239#issuecomment-1507743084))
- [name=Pamphile] Moving jobs from Azure to GH actions ([gh-15814](https://github.com/scipy/scipy/issues/15814))
    - Rethink skips: newcomers are usually not aware of CI an skipping it. Things are better now due to all jobs related to docs are in CircleCI.
- [name=Ralf] RFC for multiple array types support ([gh-18286](https://github.com/scipy/scipy/issues/18286))
    - Change in our code: np.asarray changed to use the new validation function
    - Responsibility on the array-api-compat library
    - Not the PR from Ivan, make a new one
    - Demo on some SciPy code https://quansight-labs.github.io/array-api-demo/GW_Demo_Array_API.html
- [name=Pamphile] Decision on new name for RNG ([gh-14322](https://github.com/scipy/scipy/issues/14322))
- [name=Pamphile] Extras: SciPy-Users is no more :tada:, GitPod is gone, [editable builds](https://meson-python.readthedocs.io/en/latest/how-to-guides/editable-installs.html) with new meson-python (0.13), poster accepted for SciPy2023 (on the new `scipy.stats.sobol_indices`)

## Agenda for April 5, 2023

**Present:** Melissa Mendonça (@melissawm), Pamphile Roy (@tupui), Kai Striega (@Kai-Striega), Steven Gough-Kelly (@steventgk), Jake Bowhay (@j-bowhay), Evgeni Burovski

- [name=Pamphile] drop GitPod in favour of GitHub CodeSpaces, [PR](https://github.com/scipy/scipy/pull/18241)
    - Everyone in favor.
- [name=Pamphile] retire SciPy-Users, email sent.
    - Pamphile will ask Matti to put it in archive/read-only mode.
    - We can moderate every message and auto-respond with a recommendation to post on SciPy-dev or join slack
- [name=Pamphile] do we want a tag on Scientific Python's Discuss server?
    - Related to the previous item: we could direct people there for user support.
- [name=Melissa] Notebook infrastructure, [PR](https://github.com/scipy/scipy/pull/17322)
    - Melissa to send a message to the mailing list asking for feedback
- [name=Melissa] NumFOCUS Zoom
- [name=Pamphile] Informational: NumFOCUS has been helping us secure a Slack pro account for us


## Agenda for March 22, 2023

**Present:** Melissa Mendonça (@melissawm), Jake Bowhay (@j-bowhay), Ralf Gommers (@rgommers), Tyler, Andrew Hawryluk (@ahawryluk)

- [name=Melissa] DEI grant: Pamphile joins as Contributor Experience Lead :tada:
- [name=Melissa] Final look at [Legacy directive?](https://github.com/scipy/scipy/pull/17597)
- [name=Melissa, Pamphile] Document mailing list admin team
    - Add names of current moderators in the mailing list section of scipy.org
- [name=Ralf] Gitpod: planning to propose removing it from SciPy, following NumPy
    - [NumPy mailing list discussion](https://mail.python.org/archives/list/numpy-discussion@python.org/thread/SSPI7HVL2PLWPFL42T6UNR2ENARE5A5E/)
    - No opposition to remove. Gitpod will still be available (but not pre-built) and Codespaces is another option.
    - Pamphile will send an email to the mailing list.
- [name=Andrew] If there's time, [an open namespace issue](https://github.com/scipy/scipy/issues/17771)
    - Looks like a reasonable solution - PR incoming!
- [name=Ralf] Accelerate is coming back
    - Several enhancements are made, looks like it matches OpenBLAS and is way faster
    - We may need to re-add it
    - Team seems responsive and we can re-enable and see if we're happy with performance and maintenance
    - Requires a PR to meson first (Ralf will do that)
- [name=Pamphile] New paper?
    - Who would lead this effort?
    - Pamphile will send a message to the mailing list to gauge interest
- [name=Jake] Linter
    - `ruff` doesn't seem equivalent to the previous linter we used. Not picking up some changes (ideally should be paired with `black` but we don't use it)
    - `ruff` author is open to feedback if we need extra features
    - No action items for now, but in the future we may need to have our own `scientific black`?
- [name=Pamphile] Welcome Jake as a core team member of SciPy :tada:


## Agenda for March 8, 2023
**Present:** Melissa Mendonça (@melissawm), Ralf Gommers (@rgommers), Pamphile Roy (@tupui), Jake Bowhay (@j-bowhay)
> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Melissa] GSoC?
    - Deadline approaching, no concrete follow-up -> fine to leave as is this time around.
- [name=Ralf] Cirrus CI & cross-compile CI job
    - Any feedback on how it's working so far?
    - Some failures, but not anything critical
    - May be possible to move away from Azure in the future, but not yet
- [name=Pamphile] We may have seen some movement on the [pydata-sphinx-theme performance regression issue](


## Agenda for February 22, 2023

**Present:** Pamphile Roy (@tupui), Tyler Reddy (@tylerjereddy), Jake Bowhay (@j-bowhay)


- [name=Pamphile] Seed rewritting in HTML [15852](https://github.com/scipy/scipy/issues/15852)
    - Got merged
- [name=Pamphile] NEP29: Drop support for Python<3.9 and NumPy<1.21.6
- [name=Tyler] Release of 1.10.1
    - All good, on Fedora some small failures to track down for the next major release 
- [name=Pamphile] NEP supported arch
    - Would be really helpful!
- [name=Ralf] Some Windows issue after Windows patch update
    - Something in the binary is not "conform" -> MSVC issue
- [name=Ralf] Merge [18006](https://github.com/scipy/scipy/pull/18006) to address some venv issues


## Agenda for February 8, 2023

**Present:** Kai Striega (@Kai-Striega), Pamphile Roy (@tupui), Melissa Mendonça (@melissawm), Jake Bowhay(@j-bowhay)

- [name=Melissa] Alternate new contributor meeting times
    - Next meeting will be at 8pm UTC
    - Should we create a SciPy twitch/youtube account?
    - We could stream the new contributor's meeting
- [name=Pamphile] Seed rewritting in HTML [15852](https://github.com/scipy/scipy/issues/15852)
    - Depends on patching numpydoc
    - Not necessarily related, but there is a proposal for a doctest update here: https://github.com/scipy/scipy/pull/16391
    - Pamphile will send a message to the mailing list
    - Will also check for docs build time
- [name=Kai] Support [Hypothesis](https://hypothesis.readthedocs.io/en/latest/) for testing?
    - Matt and Tirth already did some initial discussion about it
    - It's planned for in the CZI grant
    - NumPy did this a couple of years ago, may be a starting point
- [name=Melissa, Pamphile] To move the pydata-sphinx-theme to the newer version for scipy.org, should we remove our custom templates?
    - PR: https://github.com/scipy/scipy/pull/16660

- [name=Jake] Improve deprecation process documentation https://github.com/scipy/scipy/issues/16846
    - Everyone loves it :)
- [name=Melissa] Updating the roadmap?
    - If there are recent/relevant changes, we could try and update the roadmap
    - Doesn't have to be in sync. Could be over a PR or some offline discussion in addition to a meeting
- [name=Melissa] Community discussion
    - How to have high-level discussions with multiple submodule contributors?
    - Pamphile mentions we could do better on new maintainer onboarding
    - We could improve the maintainer documentation
    - Swag :)
    - Could we have special "maintainer" swag?


## Agenda for January 25, 2023

**Present:** Melissa Mendonça (@melissawm), Daniel Schmitz, Pamphile Roy (@tupui), William Tirone (@willtirone), Ralf Gommers (@rgommers), Jake Bowhay (@j-bowhay), Stéfan van der Walt (@stefanv)

> please add your names (and github handle in parenthesis). This will make it easier to stay in touch later on issues and pull requests (PRs) 😉
> This is optional since these notes will be recorded in our Github repository. If you'd like you can also paste your answer in the zoom chat 😉

*Feel free to add items for discussion to this agenda!*

- [name=Melissa] [DOC: Update pull request review guidelines #17843](https://github.com/scipy/scipy/issues/17843)
    - Include policy for inactive PRs
    - Maybe just copy what NumPy does (or even link to that docs)

- [name=Will] [ENH: working on #17719 and need some help figuring out testing](https://github.com/scipy/scipy/pull/17719)
    - Any guidance on adding tests for enhancements?
        - Test for as many cases as you can, try to include corner cases or use domain knowledge to write interesting 
        - Ask the reviewer for tips on the tests
        - Check literature/papers for tests and known values from literature that your algorithm should match
        - Look for tests in other similar functions
        - Check out [hypothesis](https://hypothesis.readthedocs.io/en/latest/) for probing for weaknesses and corner cases (NumPy uses this library for testing)
 
- [name=Stéfan] [Add optional pre-commit hook](https://github.com/scipy/scipy/pull/17812)
    - Not pre-commit (the tool) but a custom check
    - Move to ruff instead of flake8 (optional). The difference is that this will check the whole file instead of just the diff.
    - Pending is a documentation change, and a single flake8 fix commit. After that this should be ready to merge

- [name=Daniel] Labeling issues that "don't need" to be fixed (because they are part or a larger project by the core team)
    - No need for a label, but adding a comment to the issue explaining the block can be useful

- [name=Tyler] 1.10.1
    - Still pending a couple of bug fixes, could be out in the next ~10 days.

---

Please remember to archive this file and commit it to https://github.com/scipy/archive

### Useful Resources

* [Our contributor Guide](http://scipy.github.io/devdocs/dev/dev_quickstart.html)
* This is where we keep past meeting notes from the new contributors meeting https://github.com/scipy/archive/
	* You will soon find today's meeting notes there
	* You can also have a look at topics and links that were shared before 🧐

### Communication channels

How will we communicate asynchronously while working on the project?
* [Developer mailing list](https://mail.python.org/mailman/listinfo/scipy-dev)
	* We publish information which is important for contributors on this list. People from other projects might also share useful information or questions here.
* Slack [(Invitation link)](https://join.slack.com/t/scipy-community/shared_invite/zt-1a76bomjr-fuS1ZTnmP7b32kIhLb6QMg)
