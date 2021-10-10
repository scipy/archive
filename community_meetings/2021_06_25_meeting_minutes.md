---
tags: SciPy
---


# 2021-06-25 What's up SciPy


- Time: xx:00 CEST
- Join via Zoom at https://zoom.us/j/93827717491?pwd=UGdkMzlnWEFjbDNQUmxpRkp6L0VLdz09 (or [dial-in](https://zoom.us/u/abpCzJ5DAn))
- [Previous community meetings](https://hackmd.io/@tupui/scipy-meetup-2/edit)


**Present:** Tirth Patel, Bas van Beek, Melissa Mendonca, Ralf Gommers, Ross Barnowski




## Follow-up from last meeting / discussions
[//]: # (Things we did not have time to discuss)

- On using community [planning](https://github.com/scikit-image/scikit-image/issues/5169) to manage GitHub issues/PR
- [Optimization](https://github.com/scipy/scipy/pull/8414) refactoring
        - Maybe needs a separate discussion where Andrew Nelson could be present.


## Topics
[//]: # (The heart of SciPy, its community and code)

- Release of SciPy 1.7, actions?
    - CuPy hit issue on Windows
    - AIX build failing unless Pythran is disabled
    - Build time increased, which causes issues for conda-forge packaging (and our Windows CI)
    - Move to PyData Sphinx theme caused inbound links to API docs to break (patched up now, but links to tutorial will break again for 1.7.1)
- macOS M1 support for 1.7.1
- Sprinting at SciPy2021?
- Priorities for making working on SciPy more pleasant - what are blockers?
    - CI failures
    - build times
    - PR review backlog
    - docs for CODEOWNERS file --> Melissa will look into updating the docs for it, to see who to ping




### Code Specifics
- Careful with [seeding](https://github.com/scipy/scipy/pull/13863) in examples
- PRs in need of special attention?
- Special [`__repr__`](https://mail.python.org/pipermail/scipy-dev/2021-May/024772.html)?
- Using Black to format code? No [blame issues](https://black.readthedocs.io/en/stable/guides/introducing_black_to_your_project.html#avoiding-ruining-git-blame).
    - Overall: maybe useful. Dealing with PR conflicts is tricky -> see how scikit-learn does it.
    - Try this out (someone who cares) and report back please!
    - For now, `darker` may be useful to people who want to use `black` only on the code they write themself.
    - Should also check if math formulas in code are properly formatted. Checked: `black` does the wrong thing for `(2*a + 3*b)**2` :(:( --> we should fork `black` to fix this!!


### Static Typing (copy from last meeting)

- Scalar-type typing: strictness vs corectness considerations
    - _e.g._ `arg: float` vs `arg: Union[float, np.floating, np.integer]`
        - Options: make `np.floating` a proper subtype (preferred); or hide the union somewhere in a private SciPy module so can write `arg: float_`.
    - The `numbers` ABCs are unfortunately useless here (xref [python/mypy#3186](https://github.com/python/mypy/issues/3186))

- Unsafe unions: avoid them; use `Any` or `@overload` instead
    - _i.e._ unions that are used as return-type: `def func() -> Union[TypeA, TypeB]: ...`
    - Type checkers demand that operations on union-types must be compatible with _all_ of its members, and will start throwing errors otherwise.
      As these errors are generally false positives, all this accomplishes is forcing users to use excesive `isinstance()` checks, `typing.cast()` calls or adding `# type: ignore` comments (xref [python/mypy#1693](https://github.com/python/mypy/issues/1693)).
    - ```
      IntArray: Union[np.int64, np.ndarray]
      for i in IntArray:  # error: Item "signedinteger[_64Bit]" of ... has no attribute "__iter__"
           pass
      ```
    - Exceptions: ABCs and outputs that the user is reasonably expected to narrow down (via `isinstance()` for example).

Is it time to document design patterns/rules for typing in a developer docs section? It seems like we have most of the hard problems figured out, and once things are documented it's relatively straightforward to add type annotations to more functions/modules.


### Triage
[//]: # (Can we improve everyone's life and get the numbers down)

- On using tags in general
- Who?
- Going through [needs-decision](https://github.com/scipy/scipy/issues?q=is%3Aopen+is%3Aissue+label%3Aneeds-decision)
    - import numpy in examples for [instance](https://github.com/scipy/scipy/issues/13049)


### Documentation

- `pydata-sphinx-theme` polishing
    - update on accessibility
    - [Version badge](https://github.com/scipy/scipy/pull/14132)
- Tutorials and [scipy-cookbook](https://github.com/scipy/scipy-cookbook/)


## Interestings Bytes?
[//]: # (A general section to drop interesting links for instance.)

- On [black :(](https://lukasz.langa.pl/1d1a43c4-9c8a-4c5f-a366-7f22ce6a49fc/)
- [PEP 604](https://www.python.org/dev/peps/pep-0604/): Writing `typing.Union[A, B]` as `A | B`; it just looks much cleaner.
  - Available on Python 3.7 with `from future import __annotations__` now.

---

[//]: # (Still need to decide what to do)
Please remember to archive this file and commit it to github.com/scipy/...

