---
tags: SciPy
---

# 2022-03-16 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonca, Matt Haberland, Inessa Pawson, Pamphile Roy, Ralf Gommers, Ross Barnowski, Tyler Reddy, Stefan van der Walt

## Agenda

### Agenda items left from last meeting
- [name=Pamphile] What about having a Twitter or other media presence?
    - If we just want to post announcements, we can do it right away. If we want to do more, we need to have a social media policy.
    - Pamphile will look at setting this up. Announcements right now. We can look at a policy later if there's interest.

### New agenda items
- [name=Pamphile] Removing numpydoc submodule [PR](https://github.com/scipy/scipy/pull/15789)
    - Making sure that scipy is part of the procedure for numpydoc releases.
    - Make sure versions are pinned to the correct versions of numpydoc.
    - Looks good!
- [name=Ralf] NumFOCUS will start using Open Collective, so project financial balance and transactions will become visible at https://opencollective.com/scipy
    - No further action is needed for the moment.
- [name=Ralf] Platform/wheel support requests: musllinux, macOS universal2, Debian niche architectures, Windows on ARM, PyPy, etc.
    - Do we have priorities or obvious reasons not to do them?
    - Musllinux is the most popular with users, we should be able to do this. Windows-on-ARM perhaps in the future. The rest is all quite niche and perhaps not worth the maintenance effort.
    - We do have universal2 wheels now, they may be removed when we move to `cibuildwheel` though. That move may happen for 1.9.0 (copying the NumPy GH Action setup); would be nice, but it's not essential. 
- [name=Melissa] Google Season of Docs
    - Create and investigate *user journeys* ([wikipedia article](https://en.wikipedia.org/wiki/User_journey)) and profiles/personas for the documentation readers.
    - Should be similar for NumPy; two separate projects.
    - Adding examples to docstrings was high on the list for the NumPy survey; good deliverable and allows generating new content.
- [name=rossbar] Appetite for deprecating duplicate functionality in `scipy.sparse`?
  * Many examples: `spdiags` & `diags`, `random` and `rand`
  * Also some one-liners with imprecise names now that there are both sparse array and sparse matrices
    - e.g. `isspmatrix_<fmt>` where `fmt` is coo, csr, etc. All one-liners that could be removed in favor of explicit `isinstance` checks
  * No objections, things that are actually duplicate can be removed in principle (does need a mailing list setup).
 
- Lazy loading: should we document the new behavior for importing scipy?
    - We should probably not use it in our docs, but we should mention that it may be useful for interactive usage.

- [name=Pamphile] [Benckmarks are slow for meson](https://github.com/scipy/scipy/pull/15686)
    - Fixed. OpenBlas threading setting was off.
- Can we replace azure with github actions?
    - Could be a goal in the future.
