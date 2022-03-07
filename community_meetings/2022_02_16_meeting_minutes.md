---
tags: SciPy
---

# 2022-02-16 Community Meeting

- Time: 8pm UTC
- Join via Zoom at https://zoom.us/j/93827717491?pwd=UGdkMzlnWEFjbDNQUmxpRkp6L0VLdz09 (or [dial-in](https://zoom.us/u/abpCzJ5DAn))

**Present:** Melissa Mendonça, Ralf Gommers, Pamphile Roy, Rohit Goswami, Carl Kleffner, Gregory Lee, Ross Barnowski, Stéfan van der Walt, Matti Picus

## Agenda

- [name=Melissa] DataUmbrella sprint
    - July 9, 2022:  Post-sprint follow-up (1 hour)
    - June 25, 2022:  Day of Sprint (4 hours)
    - June 18, 2022:  Pre-sprint session (1 hour)

- [name=Melissa] Do we want to participate in [Google Season of Docs](https://developers.google.com/season-of-docs/docs/timeline)?
    - Updating https://scipy-lectures.org/, https://scipy-cookbook.readthedocs.io/?
    - Deadline for organization applications is March 25th
      - Focus on scipy-lectures
        - Get maintainers on board; perhaps Nicolas Rougier?
    - scipy-cookbook examples are likely outdated (ported from old cookbook site, but not maintained since); will at minimum need review to see what is still relevant

- [name=Pamphile] What about [Google Summer of Code](https://developers.google.com/open-source/gsoc/timeline)?
  - [name=Rohit] Ideas for SciPy+NumPy e.g. F2PY? --> all of these are preliminary and can be bullet pointed
      - Convert all fortran code to `pyf`
          - This leads the way towards eventual modernization, e.g. adding PROPACK from Fortran-lang
      - Updating the `pyf` format (this might need some Fortran knowledge)
      - Revamping our frontend (`argparse`, not conceptually tricky but still useful). Doesn't require any real Fortran information.
      - For SciPy, improving `meson` support for `pyf` might be relevant as well
      - Rework the build system generation (part of the `np.distutils` deprecation)
      - Test coverage (relying on SciPy as a testsuite isn't great)
      - For someone interested in the numpy C API we wanted to revamp the core `fortranobject`
          - This is happening anyway for derived types, but no real Fortran knowledge is required (is more Python-C though)
      - For Fortran afficionados --> `pyf` files to LFortran ASR; probably better [for Fortran-lang](https://github.com/fortran-lang/fortran-lang.org/wiki/GSoC-2022-Project-ideas)
- [name=Pamphile] Sprinting at [SciPy2022](https://www.scipy2022.scipy.org/sprints)?
    - Deadline for talks and posters has been extended again (Feb 22) and there will be some remote sessions
    - I will submit an application
- [name=Ralf] CoC committee update
    - Ralf will send an announcement to the mailing list
    - It might be interesting to have shared resources for handling CoC incidents
- [name=Pamphile] Release notes formatting
    - Adding contributors names/github handles?
    - https://scikit-learn.org/stable/whats_new/v1.0.html#changes-1-0
    - https://github.com/scipy/scipy/issues/15543
- [name=rossbar] Remove `numpydoc` submodule and rely on released version instead?
    - As long as numpydoc is tested against the SciPy docs build before release, this should work.
    - S: Presumably we can still pin to a specific version in SciPy, instead of relying on "latest release"?
    - Action item: [name=rossbar] have testing `numpydoc` release-candidates against the SciPy doc build formalized as part of the numpydoc release process
- [name=rossbar] Turn `scipy-cookbook` into a SciPy-centric tutorials site, similar to [numpy-tutorials](https://numpy.org/numpy-tutorials/)?
  - Action item: [name=rossbar] initial triaging of `scipy-cookbook`

- Unify CLI tools: https://github.com/scipy/scipy/issues/15489
    - Sayantika Banik is working on this and exploring different tools.


### From last meeting

- [name=Melissa] Installation page and instructions
- API docs on mobile is not ideal. Could we raise this with the pydata-sphinx-theme folks?
    - https://github.com/pydata/pydata-sphinx-theme/issues?q=is%3Aissue+is%3Aopen+mobile+

- [name=Pamphile] Blog posts? (blog like https://scipython.com)
    - Proposal for a joint space between projects: blog.scientific-python.org
    - Like https://planet.scipy.org/?
- Backlog marathon?
