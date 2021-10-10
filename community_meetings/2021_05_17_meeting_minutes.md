---
tags: SciPy
---


# 2021-05-17 What's up SciPy


- Time: 16:00 CET
- Join via Zoom at https://zoom.us/j/93827717491?pwd=UGdkMzlnWEFjbDNQUmxpRkp6L0VLdz09 (or [dial-in](https://zoom.us/u/abpCzJ5DAn))
- [Next community meetings](https://hackmd.io/@tupui/scipy-meetup-2/edit)


**Present:**

Kevin Topolski, Pamphile Roy, Melissa Mendonça, Serge Guelton, Xingyu Liu, Ralf Gommers, Bas Van Beek, Peter Bell, Gregory Lee, Mazen Sayed, Tyler Reddy, Evgeni Burovski, Matt Haberland, Warren Weckesser, Nicholas McKibben


## Follow-up from last meeting / discussions

This is our first meetup in 2 years!

## Topics

[//]: # (The heart of SciPy, its community and code)

- Meeting frequency
    - Consider meetings every two weeks with different time slots to include more contributors (all over the globe); e.g. a EU/Africa/Americas friendly time 1x/month, and a Pacific/Asia/EU friendly time 1x/month
    - P.R. will send an email to the mailing list
    - Scikit-image tried this (G.L.).
- Meetup frequency/organization/archiving/recording?
    - Serge: notes preferred over video
    - A number of thumbs up for recording. Let's do that now, and figure out after where to put it (e.g. link from an issue, rather than on YouTube)
    - Meeting is being recorded locally by Ralf
- Governance/maintainer/community update
- Roadmap [update](https://github.com/scipy/scipy/pull/13849)
    - Still need some final decision about Sensitivity Analysis
        - There has been discussion about a `scipy.diff` in the past [gh-7457](https://github.com/scipy/scipy/issues/7457)
        - There are separate packages for that. If there are a number of people who want to bring in such a package and maintain it, it could make sense. But it is difficult to add a new module and even more work to maintain it for all time.
    - [SEP](https://github.com/scipy/scipy/issues/13761) Input validation
        - Many SciPy functions are currently checking for infs/NaNs; most NumPy functions don't. Keep it consistent. (R.G.)
        - There are different reasons for doing this: organization of code VS speed things up by eliminating the validation (W.W.).
        - Decision to have an interface for eliminating validation depends on the time it takes. If it's 1%, forget about it; if it's 50%, probably a good idea. (R.G.)
        - Example case of slowdown due to input validation (and other overhead): scipy.stats continuous distributions. `stats.norm.cdf` is much slower than `special.ndtr`. (W.W.)
    - [Optimization](https://github.com/scipy/scipy/pull/8414) refactoring
        - Maybe needs a separate discussion where Andrew Nelson could be present.
    - To be considered for Roadmap:
        - Build system change
            - Meson needs better Cython and other language support; in progress. (R.G.)
            - R.G. may submit a PR that others can test out
            - Many complex projects do not use setuptools
            - There could be some pain in moving away from setup.py, but there is recent some work that will ease the transition
            - Meson does not allow in-place builds
            - Can we have a cookiecutter template to make it easier to adopt build system changes? --> yes we should do this!
            - For the Python packaging work to make pip and other installers independent from build tools (from setuptools in particular), there is a lot of standardization work going on: PEP 517, 518, 621, etc.
        - Dispatching / distributed arrays (make more concrete proposal)
            - Issue related to Dask and CuPy dispatching for ndimage: [gh-10204](https://github.com/scipy/scipy/issues/10204) (G.L.)
- Planning the release of 1.7
    - Release cycle discussion: continuous deployment
    - Branch slated for 5/26
        - PR that would replace RBF would be nice to include [gh-13595](https://github.com/scipy/scipy/pull/13595)
        - [gh-13371](https://github.com/scipy/scipy/pull/13371) (Bootstrap) and [gh-133919](https://github.com/scipy/scipy/pull/13319) (Fast Numeriocal Inverse) are close and would be nice to include
- GSoC (only if meetup after 17-05) - can't discuss because results aren't public yet
- NumFOCUS SDG round 2 (proposal due before June, 4)
    - Please submit proposals!
- GitHub workflow (approval, ownership, responsibilities, projects, meta-issues, request-review, pinging)
    - Should we make use of additional features like "Assign"
    - New feature "Code Owners" being used so that frequent maintainers get notified of related code and can easily filter
    - Use meta-issues or GH Projects?
        - R.G. prefers meta-issues
        - Check on whether any maintainer can create a GH Project
    - Might be nice to move from current (but very outdated) mailing list system (e.g. Discourse)
        - Needs to maintain existing records
        - If we get CZI Cycle 4 grant, this could be part of that work
- Review/merge policy for PRs from students who work with a maintainer offline, e.g. as a class/university project. Do we require a second review (similar to a general "don't merge your own PRs" policy)? [@ev-br's question]
    - At discretion, but probably depends on how controversial the change is.
    - If a student implements the maintainer's big idea, is the maintainer's review really independent?



## Interestings Bytes?
[//]: # (A general section to drop interesting links for instance.)


I used the following to prepare this:
- Pandas using a google doc, NumPy md archived in a repo.
    https://github.com/numpy/archive
- Things to borrow?
    https://dev.pandas.io/docs/development/maintaining.html
    https://github.com/scikit-image/scikit-image/issues/5169
- Interesting reading
    https://matthewrocklin.com/blog/2019/05/18/maintainer
    http://gael-varoquaux.info/programming/technical-discussions-are-hard-a-few-tips.html

---

Please remember to archive this file and commit it to github.com/scipy/...



