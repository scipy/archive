## Introduction

This is the GSoC'16 ideas page for both SciPy and NumPy.  The SciPy library is one of the core packages that make up the SciPy stack. It provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization.  NumPy is the fundamental package for scientific computing with Python. It contains a powerful N-dimensional array object, sophisticated (broadcasting) functions, tools for integrating C/C++ and Fortran code,linear algebra, Fourier transform, and random number capabilities.

This page lists a number of ideas for Google Summer of Code projects for both Scipy and Numpy, plus gives some pointers for potential GSoC students on how to get started with contributing and putting together their application.  It's a joint page because the Numpy and Scipy projects are quite closely related; there is a large overlap in both user community and in developers.

### Guidelines & requirements

SciPy and NumPy participate in GSoC 2016 under the [umbrella of Python Software Foundation](https://wiki.python.org/moin/SummerOfCode/2016).

PSF student guidelines: http://wiki.python.org/moin/SummerOfCode/Expectations

[Advice on writing a proposal](http://turnbull.sk.tsukuba.ac.jp/Blog/SPAM.txt#how-to-spam-in-detail) (written with the Mailman project in mind, but generally applicable)

The application template for 2016 doesn't yet exist, but it's expected to be very similar to that of 2014: [Application template for 2014](https://wiki.python.org/moin/SummerOfCode/ApplicationTemplate2014)

We expect from students that they're at least comfortable with Python (intermediate level). Some projects may also require Cython or C skills. Knowing how to use Git is also important; this can be learned before the official start of GSoC if needed though.

### Advice

Potential candidates should to take a look at [the guidelines on how to contribute to Scipy](https://github.com/scipy/scipy/blob/master/HACKING.rst.txt). Making a small enhancement/bugfix/documentation fix/etc (does not need to be related to your proposal) to Scipy or Numpy before applying for the GSoC is a requirement from the PSF; it can help you get some idea how things would work during the GSoC. 

Start on your proposal early, post a draft to the mailing list and iterate based on the feedback you receive. This will not only improve the quality of your proposal, but also help you find a suitable mentor.


## SciPy Project ideas


### Porting scipy.ndimage to Cython

This would be a joint project between scikit-image and Scipy that would provide a major improvement in maintainability and extensibility of ``ndimage``. Please see the [scikit-image GSoC page](https://github.com/scikit-image/scikit-image/wiki/GSoC-2015) for details.

- Required knowledge: Python, Cython, C
- Difficulty level: intermediate
- Potential mentors: 


### Implement scipy.diff (numerical differentiation)

Numerical derivative calculation methods are a set of core scientific numerical tools that are currently missing in SciPy. There has been discussion (and general agreement) on creating a new ``scipy.diff`` sub-package starting with the ``numdifftools`` code and some code in ``statsmodels`` (see https://github.com/scipy/scipy/issues/2035).
The project would be roughly (1) familiarise yourself with the code and methods in `numdifftools` and `statsmodels` (and maybe look at equivalent packages in other languages), (2) define the API, specifically broadcasting behavior, to make sure it covers all major use cases efficiently, (3) implement `scipy.diff`, including tests and docs.
Optionally, if there's time left, these methods could be used to compute Hesse and covariance matrices and fit parameter error in `scipy.optimize` or other packages like `statsmodels` or `lmfit` if they are considered out of scope for `scipy.optimize` for some reason.

- Required knowledge: Python, numerical derivatives
- Difficulty level: intermediate
- Potential mentors: 
- Related reading: https://github.com/scipy/scipy/issues/2035


### Improve the parabolic cylinder functions

The parabolic cylinder functions are a family of special functions that have applications in PDEs and quadratures. SciPy has implementations of these functions (`special.pbdv`, `special.pbvv`, and `special.pbwa`), but significantly improved implementations are possible thanks to research advances in the last several years. The project would be to study a sequence of papers by Gil, Segura, and Temme and implement their algorithm for the parabolic cylinder functions from scratch in Cython.

- Required knowledge: Cython, enough comfort with mathematics to learn about asymptotics and quadrature
- Difficulty level: intermediate
- Potential mentors: Josh Wilson
- Related reading: https://dl.acm.org/citation.cfm?doid=1132973.1132978 (Only look at the paper! The license for the source code is incompatible with SciPy.)

### Your own idea

The above projects are just suggestions --- it is also very good to suggest a project idea of your own if you have something in mind that you want to do. Ask people on the [mailing list](http://scipy.org/scipylib/mailing-lists.html) for suggestions in this case.


### And more...

A miscellaneous set of additional ideas can be found on the tentative [Scipy 1.0 roadmap](https://github.com/rgommers/scipy/blob/roadmap/doc/ROADMAP.rst.txt). You can help us reach this goal!


## NumPy Project ideas


### Vector math library integration

Some operations like powers, sin, cos etc are relatively slow in numpy
depending on the c library used. There are now a few free libraries
available that make use of modern hardware to speed these operations up,
e.g. sleef and yeppp. This project is to evaluate these libraries, and integrate one or more of them into numpy, providing a nice speedup to many operations.

- Required knowledge: C
- Difficulty level: intermediate
- Potential mentors:


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
- Potential mentors:

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
- Potential mentors: 

### Improved duck typing support for N-dimensional arrays

NumPy provides a powerful N-dimensional array object, but it isn't
the only N-dimensional array in Python. There are many variants of
NumPy arrays that it would be nice to work with using a similar API.
Examples include:

- [Sparse matrices in SciPy](http://docs.scipy.org/doc/scipy/reference/sparse.html)
- NumPy's [MaskedArray](http://docs.scipy.org/doc/numpy/reference/maskedarray.html)
- Labeled arrays in [xarray](http://xarray.pydata.org) and [pandas](http://pandas.pydata.org)
- Alternative array backends such as [dask.array](http://dask.pydata.org/en/latest/array.html) and [Bolt](http://bolt-project.org/).
- [DyND](http://libdynd.org/)'s N-dimensional array
- Unit implementations such as [pint](https://pint.readthedocs.org) and [astropy.units](http://docs.astropy.org/en/stable/units/).

These objects are all "array-like" in various ways (some more so than others),
but none of them use the exact same underlying implementation as NumPy's ``ndarray``.
Still, in cases where their functionality overlaps with NumPy arrays, in an ideal
world it would be possible to interact with them using the same API.
NumPy functions such as ``np.sin`` and ``np.concatenate`` should work when
called on these alternative arrays by dispatching to implementations written
by these third party libraries instead of coercing everything to NumPy arrays first.

NumPy has already made some progress towards this goal, most notably with
the proposed [``__numpy_ufunc__`` special method](http://docs.scipy.org/doc/numpy-dev/neps/ufunc-overrides.html).
However, there are still some important details to be worked out, especially for
[extending this approach to other NumPy functions](https://github.com/numpy/numpy/issues/4164).

This project could have a large impact on the SciPy ecosystem, and should be straightforward to break into incremental tasks. From a technical perspective, implementing the desired functionality should not be especially challenging. However, determining the proper API design will require active engagement with the NumPy community and authors of these third party libraries (e.g., on mailing lists and GitHub). Interested students should have strong communication skills. Broad experience working with different libraries in the SciPy/PyData stack (including the above mentioned array libraries) would also be helpful.

- Required knowledge: Python, C
- Difficulty level: hard
- Potential mentors: [Stephan Hoyer](http://github.com/shoyer)

### Improved Dealing with overlapping input/output data

Numpy operations where output arrays overlap with 
input arrays can produce unexpected results.
A simple example is
```
x = np.arange(100*100).reshape(100,100)
x += x.T        # <- undefined result!
```
The task is to change Numpy so that the results
here become similar to as if the input arrays
overlapping with output were separate (here: `x += x.T.copy()`).
The challenge here lies in doing this without sacrificing 
too much performance or memory efficiency.

Initial steps toward solving this problem were taken in
https://github.com/numpy/numpy/pull/6166
where a simplest available algorithm for detecting
if arrays overlap was added. However, this is not yet
utilized in ufuncs. An initial attempt to
sketch what should be done is at https://github.com/numpy/numpy/issues/6272
and issues referenced therein.

- Required knowledge: C
- Difficulty level: hard
- Potential mentors: 