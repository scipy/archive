---
tags: SciPy
---

# 2022-05-25 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça, Kai Striega, Evgeni Burovski, Sayantika Banik, Pamphile Roy, gz, Ralf Gommers, DWesl, Axel, Rafael, Chuba

## Agenda

- [name=Melissa] Newcomers' meeting this Friday, May 27 at 7pm UTC.
- [name=Pamphile] Work for the release of 1.9?
    - Planned release branch creation: 26 May (the day after this meeting)
    - There is one blocker. No new items should be added to the milestone. There will be a meson-python release today, hopefully this will be resolved soon.
- [name=Melissa] Secondary communication channel
    - Please [vote on your preference here](https://forms.gle/ysnhASSBmSzCtGKq7)
- [name=Pamphile] CZI full proposal
    - Waiting for feedback; deadline is June 2.
- [name=Pamphile] Use projects on GitHub (e.g. for deprecation, grants, specific projects, releases)
    - Ralf notes that this should not be a new place to look (all work should still be captured in issues)
    - Projects can also be created on people's forks to prevent pollution in the main org.
    - There are two separate "Project" features on github; be aware to be consistent.
- [name=Evgeni] doctests/refguide-check : separate to a package (a first pass at https://github.com/ev-br/scpdt)
    - Initial work: https://github.com/ev-br/scipydoctest
    - What is the maintenance cost of keeping this separate plugin? (pytest releases may break plugins)
    - What about https://github.com/astropy/pytest-doctestplus?
    - Context: https://github.com/numpy/numpy/issues/21070
- [name=Axel] Notes on the successful deprecations happening on the repo. 
    - Having separate issues is useful for discoverability and tracking purposes.
    - If issues are not immediately actionable, we can capture them as comments in a tracking issue
- [name=Sayantika] formatting using combination of `pre-commit` and `darker`, [link](https://github.com/sayantikabanik/scipy/blob/testing_pre_commit_black_darker/.pre-commit-config.yaml) to basic implementation
    - NumPy converted their pre-commit PR to draft (no decisions yet)
    - Alternatively, we could have a lighter pre-commit (or *pre-push*) hook
- [name=Melissa] Gitpod fix (coming soon)
- [name=Melissa] DataUmbrella talk about contributing to SciPy: https://t.co/p9EVSzlt40
