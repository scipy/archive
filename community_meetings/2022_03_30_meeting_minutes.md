---
tags: SciPy
---

# 2022-03-30 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça, Anirudh Dagar, Ralf Gommers, Evgeni Burovski, Inessa Pawson, Noa Tamir, Sayantika Banik, Shresth Chomal

## Agenda

- [name=Ralf] redo Zoom link? Should work without host.
    - Melissa to change, it should not require host to be present. Either link with password or signing in is fine.
- [name=Ralf] agenda topics, I am reordering them based on (my perceived) prio of a topic
- [name=Melissa] Contributor interviews for NumFOCUS Contributor Diversification & Retention (CDR) project
    - Possible someone from NumFOCUS will reach out - in case of any questions, Melissa is happy to help.
- [name=Pamphile] The Scientific Python blog is alive! And we are looking for people to write (and review) content. All info on the website or contact me: https://blog.scientific-python.org
- [name=Melissa] [GSoD project is submitted](https://github.com/scipy/scipy/wiki/Google-Season-of-Docs-2022---SciPy-Project). Accepted organizations will be announced on April 14.
    - Asked for $15,000
- [name=Pamphile] Azure timeout, we can start the move to GH with this job. Any volunteer? Part of [gh-15814](https://github.com/scipy/scipy/issues/15814)
    - No volunteers so far. We should still investigate the root cause, it may be this is not Azure but windows itself.
    - It is possible the NASA Roses grant can support this work (there's 0.5 FTE for CI & build topics across the four projects involved).
- [name=Pamphile] Merge new global optimizer: DIRECT [gh-14300](https://github.com/scipy/scipy/pull/14300)
  - [name=AndrewN] just haven't found time to review this.
  - [name=Ralf] same comment as Andrew, little time at the moment. Also, code was persistently crashing, so needs review
- [name=Pamphile] Update logos NumFOCUS. Who is responsible for sending them news for their mailing list?
    - NumFOCUS contacts are: Matt Haberland, Ralf Gommers. They get sent an email with a request for news.
    - Melissa will reach out to Arliss at NumFOCUS
- [name=Pamphile] Again spam on the Mailing List. Who has access to moderate?
    - Ralf: I believe only Matti Picus.
    - We should confirm this is the case, and if anyone else wants to share the responsibility we should have another moderator for redundancy. (Inessa could help.)
    - Inessa volunteers to help with this :tada: 
- [name=Ralf] update on / preview of developer CLI (see [gh-15489](https://github.com/scipy/scipy/issues/15489))
    - Sayantika Banik showed us the preview
    - This should be available for the DataUmbrella sprint (June 25th)
- [name=Pamphile] Follow up [gh-13955](https://github.com/scipy/scipy/pull/13955) on doc/code style. Some decisions to make. We can use the renaming wrapper introduced by Matt in [gh-15624](https://github.com/scipy/scipy/pull/15624) to make the changes at once.
    - How do we name `lambda`: `lam, lmb, lamb,
 lmbda, lambda_`?
     - Whatever it is named now
    - Where to put `versionadded`.
        - In `Notes`
    - How to name use of rng: `seed, random_state,???` ?
        - Consistency between existing APIs (e.g, `random_state` for `stats`)
    - Document how to seed documentation and tests.
        - DOC: do we want the wrapper proposed in [gh-15852](https://github.com/scipy/scipy/issues/15852)
        - TST: we promote `np.random.Generator` or `np.random.RandomState`? NEP19 seems to direct to `np.random.RandomState`.
            - Indeed, what NEP 19 says.
- [name=Pamphile] Use pre-commit hooks for the linter?
    - Is it mandatory or optional? Is there an issue or docs? Evgeni volunteers to test it.
    - Melissa: some good experience
    - Question: how would lint failures be dealt with? Some lint failures are okay and we ignore them on purpose.
    - Sayantika volunteers to do some research on this.
    - Warning not error? How to avoid extra overhead here?
    - Anirudh shares that you can add a configuration file as an argument: https://github.com/pre-commit/pre-commit-hooks/issues/112
- [name=Melissa] Should we ~~expose~~ create structure for GitHub teams?
    - https://numpy.org/teams
    - Already at https://scipy.org/teams/?
    - Melissa will invite people to the NumPy docs meeting and check for interest on creating a docs team.    
