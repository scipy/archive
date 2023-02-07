---
tags: SciPy
---

# 2022-08-10 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Tyler Reddy, Pamphile Roy (@tupui), Tiger Nie (@kwsp), Ralf Gommers (@rgommers)

## Agenda

- [name=rgommers] Fallout of the 1.9.0 release & next steps
    - Not many backport-candidate issues just yet; no plans for 1.9.1
    - The missing `.pxd` files require a 1.9.1 - Tyler plans to start on that around Aug 26.
    - PyData-Sphinx-Theme update is delayed due to performance regresssions.
- [name=rgommers] Attempt to remove `libnpymath` dependency
    - Discussed: helps with cross-compiling.
- [name=Tiger] Newcomers with experience and insentive to do C++. Proposes in [gh-16802](https://github.com/scipy/scipy/issues/16802) to port `signal.oaconvolve` to C++.
