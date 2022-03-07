---
tags: SciPy
---

# 2022-03-02 Community Meeting

- Time: 12pm UTC (noon)
- Join via Zoom at https://us06web.zoom.us/j/82228328335?pwd=R1Z5V21hZ3M1S2FyOEpXYkJSdTFsZz0

**Present:** Ralf Gommers, Tyler Reddy, Andrew Nelson, Pamphile Roy, Evgeni Burovski

## Agenda

*Feel free to add items for discussion to this agenda!*

- [name=Ralf] `scipy.datasets` & `scipy.misc` deprecation
    - Do tests and benchmarks datasets need to be public? -> perhaps not, and it saves work to keep them private
- [name=Pamphile] On pinning NumPy: can be problematic for downstream libraries, see [this](https://iscinumpy.dev/post/bound-version-constraints/) article for in-deep analysis from some Python core devs.
    ```
    ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
    scipy 1.7.3 requires numpy<1.23.0,>=1.16.5, but you have numpy 1.23.0.dev0+817.gd85bc111b which is incompatible.
    ```
    - Release procedure here, could we have updated our pin for `1.7.3`?
- [name=Pamphile] There is a [list](https://github.com/scipy/scipy/wiki/Ideas-for-changes-&-cleanups-in-SciPy-2.0) of wish for SciPy 2.0. Also [discussions](https://github.com/scipy/scipy/issues/15528) about where to go after 1.9
    - Include a link to this wish list in the roadmap!
- [name=Pamphile] NumFOCUS proposal from Matt
    - Yes

### Was not discussed
- [name=Pamphile] What about having a Twitter or other media presence?
