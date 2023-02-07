---
tags: SciPy
---

# 2022-06-22 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Kai Striega, Ralf Gommers, Pamphile Roy, Carl Kleffner

## Agenda

- [name=Carl] Joined NumPy triage team. 
- [name=Carl] Started on 32-bit Mingw-w64 toolchain. Matthew will help out, e.g. with GitHub Actions.
  - No promises, but this could possibly be ready for 1.9.1
  - pyxl needs 32-bit Python for 32-bit Office
  - Think about a NEP on what architecture is supported/provided. Have a look at CPython [PEP11](https://peps.python.org/pep-0011/) for inspiration
  - Fortran?
- [name=Pamphile] Decision: NumPy imports in doctests [PR 13049](https://github.com/scipy/scipy/issues/13049)
    - Will conclude on the issue.
- [name=Ralf] Looks like we're ready for 1.9.0RC1
- [name=Ralf] We switched to the new `doit`-based CLI in `dev.py`. Anyone missing anything, or a smooth upgrade?
    - Tirth: it would be nice for the `-j8` flag in `python dev.py ipython -j8` to be passed to the build command.
    - Evgeni: `pdb` command history is garbled. With old `dev.py` and `runtests.py` it was fine. Evgeni will open an issue: [16452](https://github.com/scipy/scipy/issues/16452)
    - Pamphile: maybe it does not source `.bash_profile` when starting a new shell. Issue happens when in a conda env. The current session is not "propagated" correctly and may lead to errors.
- interpolate: Evgeni & Kai working on this, some nice progress.
- New idea: can we use `f2c` at build time on non-Linux platforms? It works for Pyodide, and would get rid of our compiler problems.
- (Evgeni): some Fortran pieces can be replaced; the whole thing will be hard though.   
    - We can rewrite some things (e.g. QUADPACK), or deprecate some things (e.g., `interpolative`)
