---
tags: SciPy
---

# 2022-09-21 Community Meeting

- Time: 12pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Ralf Gommers (@rgommers), Pamphile Roy (@tupui), Andrew Nelson, Evgeni Burovski (@ev-br)

## Agenda

- [name=rgommers] platform support for wheels came up again in https://github.com/scipy/scipy/issues/17054
- [name=Julien Jerphanion (@jjerphan)] ~~Might not be able to join~~ I won't be able to join (it clashes with another meeting for me):
  - [I need to fix the auto-labelling](https://github.com/scipy/scipy/pull/16870#issuecomment-1251301776)
  - I would like to follow-up with stalled Cython PRs when I get some time:
      - [ENH: Implementing minimum cost flow (network simplex) #14540](https://github.com/scipy/scipy/pull/14540)
      - [ENH: Rewriting distance metrics to _distance_pybind #14611 ](https://github.com/scipy/scipy/pull/14611)
      - [ENH: Extending _distance_pybind with additional distance metrics #14640](https://github.com/scipy/scipy/pull/14640)
   - Please, feel free to suggest PRs to review or other things. :slightly_smiling_face: 

We mostly talked about supported platforms for wheels (resolution: Ralf to open a PR to add the consensus answer to the docs), and about CI platforms (less is more).
