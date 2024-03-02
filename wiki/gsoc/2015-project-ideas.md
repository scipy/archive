## Introduction

This is the GSoC'15 ideas page for both SciPy and NumPy.  The SciPy library is one of the core packages that make up the SciPy stack. It provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization.  NumPy is the fundamental package for scientific computing with Python. It contains a powerful N-dimensional array object, sophisticated (broadcasting) functions, tools for integrating C/C++ and Fortran code,linear algebra, Fourier transform, and random number capabilities.

This page lists a number of ideas for Google Summer of Code projects for both Scipy and Numpy, plus gives some pointers for potential GSoC students on how to get started with contributing and putting together their application.  It's a joint page because the Numpy and Scipy projects are quite closely related; there is a large overlap in both user community and in developers.

### Guidelines & requirements

SciPy and NumPy participate in GSoC 2015 under the [umbrella of Python Software Foundation](https://wiki.python.org/moin/SummerOfCode/2015).

PSF student guidelines: http://wiki.python.org/moin/SummerOfCode/Expectations

[Advice on writing a proposal](http://turnbull.sk.tsukuba.ac.jp/Blog/SPAM.txt#how-to-spam-in-detail) (written with the Mailman project in mind, but generally applicable)

The application template for 2015 doesn't yet exist, but it's expected to be very similar to that of 2014: [Application template for 2014](https://wiki.python.org/moin/SummerOfCode/ApplicationTemplate2014)

We expect from students that they're at least comfortable with Python (intermediate level). Some projects may also require Cython or C skills. Knowing how to use Git is also important; this can be learned before the official start of GSoC if needed though.

### Advice

Potential candidates should to take a look at [the guidelines on how to contribute to Scipy](https://github.com/scipy/scipy/blob/master/HACKING.rst.txt). Making a small enhancement/bugfix/documentation fix/etc (does not need to be related to your proposal) to Scipy or Numpy before applying for the GSoC is a requirement from the PSF; it can help you get some idea how things would work during the GSoC. 

Start on your proposal early, post a draft to the mailing list and iterate based on the feedback you receive. This will not only improve the quality of your proposal, but also help you find a suitable mentor.


## SciPy Project ideas

### ``scipy.stats`` improvements

``scipy.stats`` is one of the largest and most heavily used modules in Scipy. There has been an ongoing effort to improve the quality of this module, and it is now approaching what is needed for "Scipy 1.0". There are however still a few important improvements to be made and maintenance issues to be addressed:
  1. all the hypothesis tests should get a keyword ``'alternative'`` to give the user a choice of hypotheses to use (see stats.kstest for an example)
  2. documentation and test coverage of a number of functions is lacking (see Statistics Cleanup in Related reading below).
  3. a few functions may need to be deprecated (also part of Statistics Cleanup)
  4. we want to convert functions that return multiple parameters to return NamedTuples (see issue 4192 linked below)
  5. functions for working with missing data (``scipy.stats.mstats``) need to be made consistent with their ``scipy.stats`` counterparts

- Required knowledge: Python, preferably some knowledge of statistics
- Difficulty level: easy
- Potential mentors: Ralf Gommers
- Related reading: https://github.com/scipy/scipy/milestones/StatisticsCleanup, https://github.com/scipy/scipy/issues/4192


### Discrete Wavelet Transforms

Solid support for discrete wavelet transforms is one of the main missing features of scipy.signal, and perhaps even of Scipy as a whole.  Adding this support would start by integrating https://github.com/rgommers/pywt - includes integrating it into the Scipy build system, fixing some remaining inconsistencies in the API and adding documentation to the Scipy Reference guide - then adding some new features. Feature ideas:
  1. 1-D and 2-D inverse SWT (have been requested several times on the PyWavelets list and issue tracker).
  2. signal denoising (SureShrink & co, for scipy.signal)
  3. image compression/denoising/... algorithms (for scikit-image)

- Required knowledge: Python, Cython. Knowledge of wavelet transforms and programming in C will also be useful.
- Difficulty level: easy/intermediate
- Potential mentors: Ralf Gommers, Stefan van der Walt
- Related reading: https://github.com/scipy/scipy/wiki/GSoC-2014-:-Discrete-Wavelet-Transform-proposal-draft


### Porting scipy.ndimage to Cython

This would be a joint project between scikit-image and Scipy that would provide a major improvement in maintainability and extensibility of ``ndimage``. Please see the [scikit-image GSoC page](https://github.com/scikit-image/scikit-image/wiki/GSoC-2015) for details.


### Improve interpolation capabilities

Implement routines for evaluating, manipulating, and fitting B-splines and their tensor products to data. Currently, Scipy relies largely on the FITPACK Fortran library for its B-spline functionality. Using this library is not the best option for Python-based software, and reimplementing and extending the functionality set would bring additional flexibility. A start in this direction is in [gh-3174](https://github.com/scipy/scipy/pull/3174) --- however, the task is likely to be large enough to keep several people occupied.

Implement cubic regular grid interpolation schemes that does not need additional memory. Nearest-neighbor and linear schemes are implemented here: [gh-3323](https://github.com/scipy/scipy/pull/3323). ``scipy.ndimage`` contains similar schemes, but is restricted to uniformly spaced grids.

(Course material on B-splines: http://www.uio.no/studier/emner/matnat/ifi/INF-MAT5340/v05/undervisningsmateriale/ )

- Required knowledge: Python, Cython, spline math
- Difficulty level: intermediate
- Potential mentors: Evgeni Burovski

### Optimization

Implement and test Levenberg-Marquardt / trust region nonlinear least squares algorithm that supports additional features such as sparse Jacobian matrices and inequality constraints.
(This project involves a literature search for determining a suitable algorithmic approach.)

- Required knowledge: Python
- Difficulty level: intermediate
- Potential mentors: Pauli Virtanen
- Related reading: https://github.com/scipy/scipy/pull/90


### Implement scipy.diff (numerical differentiation)

Numerical derivative calculation methods are a set of core scientific numerical tools that are currently missing in SciPy. There has been discussion (and general agreement) on creating a new ``scipy.diff`` sub-package starting with the ``numdifftools`` code and some code in ``statsmodels`` (see https://github.com/scipy/scipy/issues/2035).
The project would be roughly (1) familiarise yourself with the code and methods in `numdifftools` and `statsmodels` (and maybe look at equivalent packages in other languages), (2) define the API, specifically broadcasting behavior, to make sure it covers all major use cases efficiently, (3) implement `scipy.diff`, including tests and docs.
Optionally, if there's time left, these methods could be used to compute Hesse and covariance matrices and fit parameter error in `scipy.optimize` or other packages like `statsmodels` or `lmfit` if they are considered out of scope for `scipy.optimize` for some reason.
- Required knowledge: Python, numerical derivatives
- Difficulty level: intermediate
- Potential mentors: Christoph Deil
- Related reading: https://github.com/scipy/scipy/issues/2035


### Your own idea

The above projects are just suggestions --- it is also very good to suggest a project idea of your own if you have something in mind that you want to do. Ask people on the [mailing list](http://scipy.org/scipylib/mailing-lists.html) for suggestions in this case.


### And more...

A miscellaneous set of additional ideas can be found on the tentative [Scipy 1.0 roadmap](https://github.com/rgommers/scipy/blob/roadmap/doc/ROADMAP.rst.txt). You can help us reach this goal!


## NumPy Project ideas


### Airspeed Velocity (ASV) compatible benchmarks

Work is currently being done to add ASV compatible benchmarks to Scipy, see [4501](https://github.com/scipy/scipy/pull/4501), [4534](https://github.com/scipy/scipy/pull/4534), [4541](https://github.com/scipy/scipy/pull/4541). A similar set of benchmarks for Numpy would be useful. A selection of benchmarks using vbench are currently maintained by [yarioptic](http://yarikoptic.github.io/numpy-vbench/).

- Required knowledge: Python, Numpy, ASV would be plus.
- Difficulty level: intermediate
- Potential mentors: Charles Harris


### Vector math library integration

Some operations like powers, sin, cos etc are relatively slow in numpy
depending on the c library used. There are now a few free libraries
available that make use of modern hardware to speed these operations up,
e.g. sleef and yeppp. This project is to evaluate these libraries, and integrate one or more of them into numpy, providing a nice speedup to many operations.

- Required knowledge: C
- Difficulty level: intermediate
- Potential mentors: Julian Taylor


### Porting parts of Numpy from C to Cython

The numpy core contains tons of complicated C code implementing
elaborate operations like indexing, casting, ufunc dispatch, etc. It
would be really nice if we could use Cython to write some of these
things -- and especially, this would make it a lot nicer to add *new* features. However, there is a practical problem: Cython assumes that
each .pyx file generates a single compiled module with its own
Cython-defined API. Numpy, however, contains a large number of .c
files which are all compiled together into a single module, with its
own home-brewed system for defining the public API. And we can't
rewrite the whole thing. So for this to be viable, we would need some
way to compile a bunch of .c *and .pyx* files together into a single
module, and allow the .c and .pyx files to call each other. This might
involve changes to Cython, some sort of clever post-processing or glue
code to get existing cython-generated source code to play nicely with
the rest of Numpy, or something else.

So this project would have the following goals, depending on how
practical this turns out to be: (1) produce a hacky proof-of-concept
system for doing the above, (2) turn the hacky proof-of-concept into
something actually viable for use in real life (possibly this would
require getting changes upstream into Cython, etc.), (3) use this
system to actually port some interesting numpy code into cython.

- Required knowledge: Python, Cython, C
- Difficulty level: hard
- Potential mentors: Nathaniel Smith

### Pythonic dtypes

Numpy has two fundamental types: `ndarray`, which implements a strided multi-dimensional array of binary data, and `dtype`, which tells `ndarray` how to interpret that binary data as something actually useful (e.g., a floating point number). This project involves making a fundamental improvement in one of these fundamental pieces.

Numpy's current dtype system is kludgy. It basically defines its own class
system, in parallel to Python's, and unsurprisingly, this new class
system is not as good. In particular, it has limitations around the
storage of instance-specific data which rule out a large variety of
interesting user-defined dtypes, and causes us to need some truly
nasty hacks to support the built-in dtypes we do have. And it makes
defining a new dtype much more complicated than defining a new Python
class.

This project would be to implement a new dtype system for numpy, in
which np.dtype becomes a near-empty base class, different dtypes
(e.g., float64, float32) are simply different subclasses of np.dtype,
and dtype objects are simply instances of these classes. Further
enhancements would be to make it possible to define new dtypes in pure
Python by subclassing ``np.dtype`` and implementing special methods for
the various dtype operations, and to make it possible for ufunc loops
to see the dtype objects.

This project would provide the key enabling piece for a wide variety
of interesting new features: missing value support, better handling of
strings and categorical data, unit handling, automatic
differentiation, and probably a bunch more I'm forgetting right now.

- Required knowledge: Python, C
- Difficulty level: hard
- Potential mentors: Nathaniel Smith

### Improve Numpy datetime functionality

Handling of time zones in numpy.datetime is currently problematic.  A write-up and several ideas to improve it are summarized at http://article.gmane.org/gmane.comp.python.numeric.general/53805. This project would start by writing a NEP (Numpy Enhancement Proposal) on which alternative to choose, and then implement the NEP. Requires solid C skills.

- Required knowledge: Python, C
- Difficulty level: hard


## Student applications for 2015 to Scipy and Numpy
- Maniteja Nandana: *Scipy: proposal to add scipy.diff package* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/inspiremaniteja/5629499534213120),   [public draft proposal](https://github.com/maniteja123/GSoC/wiki/Proposal%3A-add-finite-difference-numerical-derivatives-as-%60%60scipy.diff%60%60)

- Abraham de Jesus Escalante Avalos: *Scipy: scipy.stats improvements* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/abraham_escalante/5629499534213120),   [public draft proposal](https://onedrive.live.com/view.aspx?resid=E5548AD35687C4B2!494&ithint=file%2cpdf&app=WordPdf&authkey=!AESFhKX64QBOPd8)

- Nikolay Mayorov: *Improve nonlinear least squares minimization functionality in SciPy* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/nmayorov/5629499534213120),   [public draft proposal](https://stackedit.io/viewer#!provider=gist&gistId=d806ad6048c7e3df4797&filename=GSOC_proposal.md)

- Anastasiia Tsyplia: *SciPy: FITPACK alternative with Python/Cython* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/vermelha/5629499534213120),   [public draft proposal](https://drive.google.com/open?id=0BzveGSDwNVtBVDZiUlgybGNpcFk&authuser=0)

- Anastasiia Tsyplia: *SciPy: Multivariate tensor product spline* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/vermelha/5707702298738688),   [public draft proposal](https://drive.google.com/open?id=0BzveGSDwNVtBaW02VktrZndJdnc&authuser=0)

- Tsutsumi Fukumu: *SciPy: Implement scipy.diff (numerical differentiation)*   [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/levelfour/5629499534213120),   [public draft proposal](http://markdownshare.com/view/fdd1aa36-3399-4498-a8a9-57a956bafb9d)

- Oguzhan Unlu: *Numpy - Vector math library integration*  [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/blacksimit/5741031244955648),   [public draft proposal](https://gist.github.com/oguzhanunlu/1f8bf3ffc6ac5c420dd1)

- Marcos Chavez: *Numpy - Porting core functions of Numpy from C++ to Python/Cython* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/marcospc6/5629499534213120),   [public draft proposal](https://github.com/marcospc6/GSoC-Proposal/blob/master/gsocproposal.md)

- Shubhankar: *Vector Math Library Integration in Numpy* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/mshubhankar/5629499534213120),   [public draft proposal](https://github.com/mshubhankar/gsoc2015/blob/master/Proposal.md)


And one proposal to Scikit-image which is intended to be a joint effort between the Scikit-image and Scipy teams:

- Aman Singh: *Scikit-Image: rewriting scipy.ndimage to cython* [Melange proposal](http://www.google-melange.com/gsoc/proposal/review/org/google/gsoc2015/bewithaman/5629499534213120),   [public draft proposal](https://docs.google.com/document/d/11RTVaDQDu38mrEv3WPdguxprJ-ha5kGnx2LhpEUFE8g/edit)

