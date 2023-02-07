---
tags: SciPy
---

# 2022-11-02 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça (@melissawm), Pamphile Roy (@tupui), Tyler Reddy, Evgeni Burovski, Alberto Scomparin, Kevin Anderson

## Agenda

- [name=Daniel, Pamphile] CI skipping strategy
    - https://mail.python.org/archives/list/scipy-dev@python.org/thread/YPXVP23DGXMDRYDGB4AZW2426ZEHEV3D/
    - Proposal: add more options for skipping (for example, `[skip group1]`)
    - Pamphile will submit a proposal to the mailing list with some groups
- [name=Melissa] [PR for notebook infrastructure for docs](https://github.com/scipy/scipy/pull/17322)
    - Will try to prioritize this before branching 1.10 (Dec 6)
- [name=Melissa] [Testing guide: remove runtests.py?](https://scipy.github.io/devdocs/dev/contributor/runtests.html)
    - Maybe wait until distutils goes away, but this should happen soon
    - 32-bit windows is still a problem for meson, so we can't get rid of it entirely
    - Add note at top of this page about using meson whenever possible.
- [name=Melissa] (Reminder) Upcoming Sprints
    - PyData NYC (November 8, In person/virtual)
        - Melissa will be there in person, for half a day
    - PyData Global (December 1-3, Virtual)
    - Melissa to try and recover a few small(ish) projects to offer sprint participants
- [name=Melissa] Legacy directive
    - Do we want it fully automatic, or with options?
