---
tags: SciPy
---

# 2023-01-11 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Kai Striega (@Kai-Striega), Pamphile Roy (@tupui), Ralf Gommers (@rgommers), Evgeni Burovski (@ev-br), Vinayak Dev (@vinayakdsci)

## Agenda

- [name=Melissa] SciPy fosstodon account?
    - Suggestion: mirror twitter content; announcements only. -> yes, sound good, let's do this!
    - also mention on the twitter account that we now have a Mastodon one.
- [name=Melissa] Update [Reviewing PRs](https://docs.scipy.org/doc/scipy/dev/contributor/reviewing_prs.html)
    - Could we add a policy for inactive PRs?
    - Example ([from NumPy](https://numpy.org/doc/stable/dev/reviewer_guidelines.html#for-maintainers)): *If the PR submitter doesn’t respond to your comments for 6 months, move the PR in question to the inactive category with the “inactive” tag attached. At this point, the PR can be closed by a maintainer. If there is any interest in finalizing the PR under consideration, this can be indicated at any time, without waiting 6 months, by a comment.*
    - Agreed that this is a good idea.
    - Don't want it to be a bot.

- [name=Evgeni] Cython 0.29.33 is out with cython depfile support, can we now simplify our meson.build files? Also `const fused` has landed in cython.
    - Now waiting on Meson to do the plumbing
    - See [gh-16293](https://github.com/scipy/scipy/issues/16293), where improved depfile support is tracked.

- [name=Ralf] For `sparse.csgraph` (and `optimize` too), should we better document that in case of multiple equivalent solutions, we don't guarantee which one is returned? See [gh-17734](https://github.com/scipy/scipy/issues/17734).
    - Can't guarantee which one is returned if no theoretical guarantees are available.
    - For dijkstra specifically, it seems well understood that solutions are not unique.
