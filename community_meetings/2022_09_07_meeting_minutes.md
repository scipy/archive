---
tags: SciPy
---

# 2022-09-07 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://us06web.zoom.us/j/6345425936?pwd=aDVFQzVmbk9SVU5jU0Jwc0s3YWUrdz09
    - If you need a passcode for zoom, `scipy` should work.

**Present:** Melissa Mendonça (@melissawm), Pamphile Roy (@tupui), Lev Maximov (@axil), Meekail Zain, Daniel Schmitz, Tyler Reddy, Ross Barnowski

## Agenda

- [name=Lev] [SciPy tutorial](https://betterprogramming.pub/python-spline-interpolation-how-to-ef059c214d28?sk=533401d8775bcea491307a386ce36fcc)
    - Request for feedback from maintainers
    - Related issue/question: https://github.com/scipy/scipy/issues/3164
    - Pamphile suggests sending an email to the mailing list to get feedback on this new feature (adding a kwarg)
    - What are the best practices for interpolation? (Evgeni is working on that, might help to connect)
    - Pamphile also mentions there is a [blog for the scientific Python community](https://blog.scientific-python.org)

- [name=Meekail Zain] CSR Hstack bug PR: https://github.com/scipy/scipy/pull/16628
    - Need some feedback/review. This bug is affecting scikit-learn
    - To request a review, a few options are to ask on the mailing list, or ask for other scikit-learn maintainers to comment on the issue and explain why this is important
    - Tyler will ping folks in the PR

- [name=Daniel] [In this page](https://docs.scipy.org/doc/scipy/dev/contributor/rendering_documentation.html), the CircleCI link to check the rendered docs now has a new caption. Docs should be updated
