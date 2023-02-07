---
tags: SciPy
---

# 2022-08-24 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa (@melissawm), Ralf Gommers (@rgommers), Pamphile Roy (@tupui), Matti Picus (@mattip), Andrew Nelson, Anirudh Dagar

## Agenda

- [name=...] _add your topic(s) here_
- [name=Melissa] Triage guide
    - [WIP document](https://hackmd.io/@melissawm/SkxA3bk3c)
- [name=Pamphile] [PR labeler](https://github.com/scipy/scipy/pull/16870)
    - Looks good, we can try and remove if it doesn't work
- [name=Melissa] Can we close?
    - https://github.com/scipy/scipy/pull/3597
    - [Migrated from Trac](https://github.com/scipy/scipy/issues?q=is%3Aopen+sort%3Aupdated-desc+label%3A%22Migrated+from+Trac%22) -> yes, can be removed
    - "Triage requested" label? Not at this point.
- [name=Anirudh] [Improve SciPy deprecation process](https://github.com/scipy/scipy/issues/16846)
    - improve refguide_check?
    - How can we improve/document the process to make it easier for people to not forget
    - Include clear comments/TODO items
    - https://github.com/scipy/scipy/pull/16866 -> how to list deprecation warnings that might show up in docs examples
- [name=Pamphile] PyData Sphinx theme regression
    - Comes from the autosummary templates. Team is investigating a solution
