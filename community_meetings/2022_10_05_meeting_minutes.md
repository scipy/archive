---
tags: SciPy
---

# 2022-10-05 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça, Ralf Gommers, Tyler Reddy, Pamphile Roy, Evgeni Burovski

## Agenda

- [name=Melissa] [add infrastructure for examples as IPython notebooks #5233](https://github.com/scipy/scipy/issues/5233)
    - No plans to convert the current tutorials to notebooks. Initially, start by adding new tutorials in the new format (.md)
    - https://nbval.readthedocs.io/en/latest/ can be used for testing. 
    - https://nbval.readthedocs.io/en/latest/#Avoid-output-comparison-for-specific-cells
    - Related issue: https://github.com/ev-br/scpdt/issues/56

- PROPACK issues: multiple structural issues, consider rewriting in Cython or C++
- Release process for 1.9.2 on track
- `import numpy as np`: let's finish this off

- Add a `legacy` directive to use in the docs
    - Should inherit from one of the other admonitions
    - Add a note to the developer docs on how to use it
    - [ML thread](https://mail.python.org/archives/list/scipy-dev@python.org/thread/Z33JO27EX6BX7LVBI6CW6MX64VQZIJ66/#6GLVRHX5XBTZNL62LFN4YPGACY5BDPLA)

- Evgeni is working on interpolate
    - Will need review effort once this is done