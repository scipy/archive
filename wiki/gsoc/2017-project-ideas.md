## Introduction

This is the Google Summer of Code 2017 (GSoC'17) ideas page for SciPy.  The SciPy library is one of the core packages that make up the SciPy stack for scientific computing with Python. It provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization.

This page lists a number of ideas for Google Summer of Code projects for SciPy, plus gives some pointers for potential GSoC students on how to get started with contributing and putting together their application. 

### Guidelines & requirements

SciPy will participate in GSoC'17 under the [umbrella of Python Software Foundation](http://python-gsoc.org).  Please read that page carefully, it contains important advice on the process.

Also read [advice on writing a proposal](http://turnbull.sk.tsukuba.ac.jp/Blog/SPAM.txt#how-to-spam-in-detail) (written with the Mailman project in mind, but generally applicable)

We expect from students that they're at least comfortable with Python (intermediate level). Some projects may also require Cython or C skills. Knowing how to use Git is also important; this can be learned before the official start of GSoC if needed though.

### Getting started on SciPy

Potential candidates should to take a look at [the guidelines on how to contribute to Scipy](http://scipy.github.io/devdocs/hacking.html). Making a small enhancement/bugfix/documentation fix/etc (does not need to be related to your proposal) to Scipy before applying for the GSoC is a hard requirement; it can help you get some idea how things will work during GSoC. 

Start on your proposal early, post a draft to the mailing list and iterate based on the feedback you receive. This will not only improve the quality of your proposal, but also help you find a suitable mentor.


## SciPy Project ideas

### Make the SciPy test suite work with pytest

SciPy currently uses ``nose`` for its test suite.  ``nose`` is not being maintained anymore, 
and migrating the test suite so it works with ``pytest`` as well is important for future-proofing.
Ideally as a result the test suite can be run with either of ``nose`` and ``pytest`` with all the bells and
whistles, with fast/slow/xslow tests, skipifs and knownfailures. Further improvements like easily identifying tests that are too slow [gh-6989](https://github.com/scipy/scipy/issues/6989#issuecomment-279668168) should be feasible as well for a good student.

This project will likely also require making changes in ``numpy.testing``.

- Required knowledge: Python
- Difficulty level: easy
- Potential mentors: Evgeni Burovski, Ralf Gommers


### Implement scipy.diff (numerical differentiation)

Numerical derivative calculation methods are a set of core scientific numerical tools that are currently missing in SciPy. There has been discussion (and general agreement) on creating a new ``scipy.diff`` sub-package starting with the ``numdifftools`` code and some code in ``statsmodels`` (see https://github.com/scipy/scipy/issues/2035).
The project would be roughly (1) familiarise yourself with the code and methods in `numdifftools` and `statsmodels` (and maybe look at equivalent packages in other languages), (2) define the API, specifically broadcasting behavior, to make sure it covers all major use cases efficiently, (3) implement `scipy.diff`, including tests and docs.
Optionally, if there's time left, these methods could be used to compute Hesse and covariance matrices and fit parameter error in `scipy.optimize` or other packages like `statsmodels` or `lmfit` if they are considered out of scope for `scipy.optimize` for some reason.

A private implementation of an important function that can be built upon (``approx_derivative``, see https://github.com/scipy/scipy/issues/6026) is already present in SciPy. 

- Required knowledge: Python, numerical derivatives
- Difficulty level: intermediate
- Potential mentors: Matt Haberland, Ralf Gommers
- Related reading: https://github.com/scipy/scipy/issues/2035, https://github.com/scipy/scipy/wiki/Proposal:-add-finite-difference-numerical-derivatives-as-scipy.diff


### Improve the parabolic cylinder functions

The parabolic cylinder functions are a family of special functions that have applications in PDEs and quadratures. SciPy has implementations of these functions (`special.pbdv`, `special.pbvv`, and `special.pbwa`), but significantly improved implementations are possible thanks to research advances in the last several years. The project would be to study a sequence of papers by Gil, Segura, and Temme and implement their algorithm for the parabolic cylinder functions from scratch in Cython.

- Required knowledge: Cython, enough comfort with mathematics to learn about asymptotics and quadrature
- Difficulty level: intermediate
- Potential mentors: Josh Wilson
- Related reading: https://dl.acm.org/citation.cfm?doid=1132973.1132978 (Only look at the paper! The license for the source code is incompatible with SciPy.)


### Improve support for B-splines

Recently a new ``BSpline`` class was added in SciPy.  This opened the way for many
possible improvements and new features for working with splines.
See https://github.com/scipy/scipy/issues/6730 and
https://github.com/scipy/scipy/issues/6710 for a list of possible sub-projects
of ranging difficulty. This project will require a student to be able to read
relevant literature and get an understanding of the math.

- Required knowledge: Python, Cython
- Difficulty level: intermediate
- Potential mentors: Evgeni Burovski, Ralf Gommers

### Your own idea

The above projects are just suggestions --- it is also very good to suggest a project idea of your own if you have something in mind that you want to do. Ask people on the [mailing list](http://scipy.org/scipylib/mailing-lists.html) for suggestions in this case.


### And more...

A set of additional new feature ideas can be found on the [Scipy Roadmap](http://scipy.github.io/devdocs/roadmap.html).


