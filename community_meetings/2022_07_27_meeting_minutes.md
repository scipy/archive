---
tags: SciPy
---

# 2022-07-27 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça (@melissawm), Pamphile Roy (@tupui), Ralf Gommers (@rgommers), Matti Picus (@mattip), Julien Jerphanion (@jjerphan), Andrew Nelson

## Agenda

- [name=Julien Jerphanion (@jjerphan)] 
    - Hi, I am [Julien](https://jjerphan.xyz). I am new to this meeting and have read and agree with [SciPy COC](http://scipy.github.io/devdocs/dev/conduct/code_of_conduct.html).
    - I have contributed to SciPy a few times and am interested in getting involved in the project (time permitting, already quite busy with scikit-learn), especially regarding Cython / C++ / performance [as said here](https://github.com/scipy/scipy/pull/15493#discussion_r910096498).
    - Some idea of contributions which might be useful (mentionned to Pamphile):
        - Centralize Cython directives (see this [mention](https://github.com/scipy/scipy/pull/16483#discussion_r910769037))
        - Add a GitHub Action to label PRs modifying Cython code (see [the proposal for scikit-learn](https://github.com/scikit-learn/scikit-learn/pull/19850/files))
    - On a side note, part of the scikit-learn team will be at EuroScipy 2022.
    - On project projects features overlap, an example: 
        - distance metrics implementations also exist in scikit-learn, and duplicate on the ones of `scipy.spatial.distance`
        - In scikit-learn, there are implemented in Cython (rather than C++) and now support sparse (CSR) vector and are only accessible in Python.
        - The ones of SciPy might be more efficient for dense vectors and are technically accessible from C++, Cython and Python. 
        - Potentially: 
            - some project (e.g. scikit-learn) could use SciPy implementations
            - users might be a bit loss between functionality provide by scikit-learn and SciPy
            - for scikit-
        - but this is more of a example than a strong need for scikit-learn maintainers (at the moment), potentialy there might be overlap between the projects (e.g. BallTree and KDTree are other example) that we -- maintainers of scikit-learn, SciPy, etc. -- might want to minimize for the ecosystem clarity and maintainability


- [name=Pamphile] Scientific Python has a [Discord](https://discord.gg/vur45CbwMz)
- [name=Pamphile] SciPy2022 (conference)
    - Enthough is transfering the organization to NumFOCUS!
        - What about the SciPy.org domain?
    - Good feedback on SciPy during the conference.
    - Sprint was a success: >15 people, >10 PRs.
    - A few things to improve for new contributors. (done)
- [name=Pamphile] EuroSciPy2022
    - Talk: _Elevating Contributor Experience: Development of SciPy command-line interface (CLI)_, Sayantika Banik
    - Tutorial: _Introduction to SciPy_
        - Who? What is the program?
        - Intro-level, typically handled by people with teaching experience and not necessarily maintainers.

- [name=Pamphile] SDG: we got it 🥳 (partial funding) on UNU.RAN & `scipy.stats`

- [name=Ralf] 1.9 release should come soon

- [name=Pamphile] Documentation changes
    - Version switcher and search bar (in the navbar) need to be fixed for the new version of the docs theme. This is in progress.
    - Pamphile to coordinate with Tyler to make sure this goes smoothly.

Discussions:
 - Mentionning shared library and packaging: 
     - [name=Julien]: 
         - [threadpoolctl](https://github.com/joblib/threadpoolctl/) allows inspecting shared libraries that are used or distributed by packages.
         - [Scenario with multiple version of OpenMP objects](https://github.com/joblib/threadpoolctl/blob/master/multiple_openmp.md)
     - Matti opened an issue to [move to cibuildwheel](https://github.com/scipy/scipy/issues/16708) and is willing to help make it happen
     - [name=Ralf] https://github.com/MacPython/openblas-libs/
         - diagram of how this fits together in slides 12-13 of https://www.slideshare.net/RalfGommers/parallelism-in-a-numpybased-program
        - [name=Julien] This presentation sums up everything. Thanks!
