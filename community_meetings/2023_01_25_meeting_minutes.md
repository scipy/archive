---
tags: SciPy
---

# 2023-01-11 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça (@melissawm), Daniel Schmitz, Pamphile Roy (@tupui), William Tirone (@willtirone), Ralf Gommers (@rgommers), Jake Bowhay (@j-bowhay), Stéfan van der Walt (@stefanv)

## Agenda

- [name=Melissa] [DOC: Update pull request review guidelines #17843](https://github.com/scipy/scipy/issues/17843)
    - Include policy for inactive PRs
    - Maybe just copy what NumPy does (or even link to that docs)

- [name=Will] [ENH: working on #17719 and need some help figuring out testing](https://github.com/scipy/scipy/pull/17719)
    - Any guidance on adding tests for enhancements?
        - Test for as many cases as you can, try to include corner cases or use domain knowledge to write interesting 
        - Ask the reviewer for tips on the tests
        - Check literature/papers for tests and known values from literature that your algorithm should match
        - Look for tests in other similar functions
        - Check out [hypothesis](https://hypothesis.readthedocs.io/en/latest/) for probing for weaknesses and corner cases (NumPy uses this library for testing)
 
- [name=Stéfan] [Add optional pre-commit hook](https://github.com/scipy/scipy/pull/17812)
    - Not pre-commit (the tool) but a custom check
    - Move to ruff instead of flake8 (optional). The difference is that this will check the whole file instead of just the diff.
    - Pending is a documentation change, and a single flake8 fix commit. After that this should be ready to merge

- [name=Daniel] Labeling issues that "don't need" to be fixed (because they are part or a larger project by the core team)
    - No need for a label, but adding a comment to the issue explaining the block can be useful

- [name=Tyler] 1.10.1
    - Still pending a couple of bug fixes, could be out in the next ~10 days.
