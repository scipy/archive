---
tags: SciPy
---

# 2022-04-27 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça, Ralf Gommers, Pamphile Roy, Evgeni Burovski, Kai 

## Agenda

- [name=Melissa] Newcomers' meetings
    - Frequency and times to be decided
    - Works well for NumPy; right now Melissa & Inessa are starting to determine effectiveness, whether PRs get reviewed, etc.
- [name=Pamphile] On-boarding/off-boarding maintainers
    - Security concerns (too many maintainers with PyPI access, 2FA if you have commit rights, etc.)
    - Workflow, communication
    - Responsibilities, expectations
    - Swag
    - Tidelift requests 2FA and other security actions to support us
    - This (both security concerns, and responsibilities/expectations for new maintainers) should be documented in the core developer guide
    - Can we have a list of people and their responsibilities? (We can do this on codeowners)
    - Offboarding: we do have an "Emeritus Maintainer" space on the website, but we don't have a policy for this. Should probably be added to the core developer guide.
- [name=Melissa] Sprints
    - DataUmbrella 
        - ~~June 25th~~ Canceled by DataUmbrella folks
    - PyCon US’22
        - Select a few issues and add a “sprint” label to them
            - [Deprecation tracking issue](https://github.com/scipy/scipy/issues/15765) is a possibility
        - Mentored sprints April 30, regular developer sprints May 2-3
            - *Pamphile (cannot sorry), Anirudh, & Tyler tentatively volunteer to help*
        - **Mentored sprints**
            - Saturday, April 30th, 8:00 pm to 12:00 am UTC. [on your timezone](https://www.timeanddate.com/worldclock/fixedtime.html?msg=PyCon+US+2022+mentored+sprints&iso=20220430T14&p1=220&ah=4.)
            - Please confirm your availability and the time slot preferred by [entering your name in this document](https://docs.google.com/spreadsheets/d/1FWamp-R1OBCkBFJccg7-K3BK0SAMMsc-Jb1DOc4itbs/edit?usp=sharing) You may choose to mentor for 2 hours only or stay for the entire sprint.

- [name=Melissa] SciPy development workflow video (https://www.youtube.com/watch?v=HgU01gJbzMY)
    - Put the script for the recording in `scipy/archive`.
    - no updates yet

- [name=Pamphile] Letter of Intent for CZI 
    - Very focused on biomedical applications
    - Submitted by Pamphile and Matt
    - Should have an answer about submitting a full proposal in a month or so

- [name=Ralf] Any more feedback on the new developer CLI?
    - After 1.9 is released, runtests.py should be removed
    - Possible concerns are install issues
    - Needs to be tested on windows in particular

- [name=Evgeni] Any outstanding meson integration issues?
    - BLAS: MKL testing, ILP64 not yet supported
    - pyproject.toml integration
    - Editable wheels are in progress: https://github.com/FFY00/mesonpy/issues/47
