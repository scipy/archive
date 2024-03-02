## Introduction

This is the Google Summer of Code 2022 (GSoC'22) ideas page for SciPy.  The SciPy library is one of the most widely used libraries for scientific computing with Python. It provides many user-friendly and efficient numerical routines for everything from linear algebra and numerical optimization to statistics and graph algorithms.

This page lists a number of ideas for Google Summer of Code projects for SciPy, plus gives some pointers for potential GSoC students on how to get started with contributing and putting together their application. 

### Guidelines & requirements

SciPy plans to participate in GSoC'22 under the [umbrella of Python Software Foundation](http://python-gsoc.org). 

We expect from students that they're at least comfortable with Python (intermediate level). Some projects may also require Cython or C skills. Knowing how to use Git is also important; this can be learned before the official start of GSoC if needed though.

If you have an idea of what you would like to work on (see below for ideas) and are considering participating:

1. Read the [PSF page](http://python-gsoc.org/) carefully, it contains important advice on the process.
2. Read [advice on writing a proposal](http://turnbull.sk.tsukuba.ac.jp/Blog/SPAM.txt#how-to-spam-in-detail) (written with the Mailman project in mind, but generally applicable)
3. Look at [the guidelines on how to contribute to SciPy](http://scipy.github.io/devdocs/dev/hacking.html).
4. Make a enhancement/bugfix/documentation fix -- it does not have to be a large PR, and it does not need to be related to your proposal. Doing so before applying for the GSoC is a hard requirement for SciPy. It helps everyone by providing some idea on how things would work during GSoC.
5. Start writing your proposal early, post a draft to the [scipy-dev mailing list](https://mail.python.org/mailman3/lists/scipy-dev.python.org/) and iterate based on the feedback you receive. This will both improve the quality of your proposal and help you find a suitable mentor.

### Contact

If you have a question *after checking all guideline pages above*, you can email the [scipy-dev mailing list](https://mail.python.org/mailman3/lists/scipy-dev.python.org/).

## SciPy Project ideas


### f2py improvements

#### Restructuring the F2PY frontend
- The plan is to migrate the front-end to `argparse`
- Subsequently, as part of the `np.distutils` deprecation, the goal is to replace the build system with generators for `meson` and `cmake`

Within scope will also be improvements to the `meson` support and enabling extended compilers. In particular, LLVM based Intel, LFortran and Flang should be usable with the new CLI interface.


- Required knowledge: Understanding of build systems (`meson`, `cmake`), `argparse` CLI design, testing
- Project length: 175 hours
- Difficulty level: Low-Medium
- Potential mentors: Rohit Goswami

#### Unifying F2PY C structures with NumPy-C


- Since the `meson` conversion, only `pyf` files are used.
- The code-generation should be cleaner to reduce the warnings under `gcc` and `clang`

Subsequently, we intend to work on improvements to the `f2py` `pyf` file format. Ideally, the goal is to reduce or eliminate `usercode` blocks within the signature files.


- Currently certain types are replicated in NumPy and F2PY, e.g. `complex`, the goal is to reduce the maintainability burden of `f2py` by using more of the NumPy-C API
- From SciPy's perspective, consider `fitpack.pyf` which defines (in `C`) local `typedef`s
  + Some of these make more sense in the context of the relatively newer `.f2py_f2cmap` dictionary
- Extensions include cleaning up the `fortranobject` code
   + In particular, moving to the limited API for ABI compatibility across versions

Tests are also required for this portion of the code-base.

- Required knowledge: Python-C API, NumPy-C API, some interest in understanding how Fortran maps to C structures
- Project length: 350 hours
- Difficulty level: Medium-Hard
- Potential mentors: Rohit Goswami

#### Fortran Python interoperability extensions
- Generating `ufuncs` for elemental functions
- Improving code-generation, by using f-strings instead of the global dictionary structure
- Adding support for coarrays and teams via MPI [extension]
 
This more open ended, there are a lot of features to support and there will be overlap with compiler projects.

- Required knowledge: Understanding of new Fortran features, and extensive familiarity with the NumPy-C API, interest in parallel computing
- Project length: 350 hours
- Difficulty level: Hard
- Potential mentors: Rohit Goswami

### Object-oriented design of digital filtering in scipy.signal

**NOTE: not yet updated from last year, TBD if this is still a potential idea**

Digital filters design, analysis and signal filtering are core functionalities of `scipy.signal`. The design approach and naming conventions there are largely adopted from MATLAB. While it was a good approach for the initial stages of development, now it seems somewhat dated, convoluted and hard to use, especially for people without MATLAB background or when simple filtering with minimum efforts is needed ("non expert usage").

The scope of this project is to condense all functionality related to digital filters into an easy-to-use class and possibly accompanying functions. It will involve writing new code as well as reusing (wrapping) existing functions.

By a linear digital filter we mean a single-input single-output system which implements a linear difference equation and can be fully described by its impulse response (also called a linear time-invariant system).

The proposed design is similar to the design of `scipy.spatial.transform.Rotation` and follows "object focused" section in this [issue](https://github.com/scipy/scipy/issues/6137). The digital filter is represented by `DigitalFilter` or simply `Filter` class, which encapsulates internal representation of the filter and has the following core functionality:

- Initialize from and convert to commonly used representations
    * Transfer function coefficients (a and b, or denominator and numerator): `from_tf`/`as_tf`.
    * Zeros, poles and gain: `from_zpk`/`as_zpk`.
    * Sequence of second order sections: `from_sos`/`as_sos`.
    * State-space representation matrices: `from_ss`/`as_ss` - possibly
- Combining filters
    * To combine two filters in cascade we can use `__mul__` operator: `C = A * B` also `C = 0.5 * A` - gain adjustment
    * To combine two filters in parallel we can use `__add__` operator: `C = A + B`
- Query filter properties
    * Frequency response
    * Group delay
    * Impulse response
    * Step response
- Filter a signal. Most likely a single method `filter` or `__call__` should be provided, but which can be supplied with additional arguments
    * Default call should implement `lfilter` logic
    * Initial conditions can be supplied, covering `lfiltlc, lfilter_zi` and maybe some other logic
    * Filtering with zero phase shift with `filtfilt` logic 
    * With linear-phase FIR filters, a result similar to `filtfilt` can be achieved by shifting the output by the fixed number of taps (constant group delay), perhaps such logic could also be activated with an argument

More difficult subject is whether new filter design functionality should be provided or we should stick to existing functions. I think that "non expert usage" filter design functionality is clearly lacking and generally everything can be done more elegant, clean and concise, but it will require significant work and expert knowledge.

New filter design functionality could be implemented as class (factory) methods or as standalone functions. For the updated filter design functionality I think we should strive for the following:

- Functions or methods and their arguments have good, descriptive names
- Few entry points and good conceptual generalization
- Arguments should be intuitive and have good default values. Maybe special "no expert usage" functions or methods should exist. For example, a user should not think how many coefficients he needs to create a reasonably good low-pass FIR filter with a given cutoff frequency. Low-pass filtering with delayed compensation should be done with a short line of code with minimum thinking. Something like that `DigitalFilter.simple_fir(cutoff=0.1).filter(x, compensate_delay=True)`
- Consistent and logical approach to frequency specification. Probably the best idea is to accept the sampling frequency for more intuitive treatment, but set it to 1 by default which will mean that all frequencies are measured as fractions of the sampling frequency, i. e. "normalized frequency" in cycle/sample is used.

Project summary:

- Required knowledge: Python, API design, experience and interest in Digital Signal Processing
- Project length: 175 hours
- Difficulty level: medium-hard
- Potential mentors: Nikolay Mayorov

### PyData/Sparse C++ Rewrite
[PyData/Sparse](https://github.com/pydata/sparse/) is a sparse array library that provides N-dimensional sparse arrays in the `COO`, `DOK` and a generalized version of the `CSR` format for N dimensions. We plan to re-write the library with a solid theoretical foundation for optimized run-time performance. There is an attempt underway at [this repository](https://github.com/hameerabbasi/xsparse/).

The ideas implemented are mainly taken from the [TACO papers by Fred Kjølstäd](https://arxiv.org/search/?query=Kjolstad%2C+F&searchtype=author&abstracts=show&order=-announced_date_first&size=50), but these will often be extended and modified as needed.

The general plan of attack will be as follows:

* Read/understand the TACO papers, particularly [this one](https://arxiv.org/abs/1804.10112).
* Discuss with your mentor how you would convert the code generation approaches into compile-time templated C++.
* Learn to explore and extend these approaches to cover other methods not explained in these papers, such as reshaping, transposing and partial evaluation.
* Implement these approaches as you learn.
* (Stretch goal) Write a cppyy wrapper and expose the NumPy API with this wrapper.

Project summary:

- Required knowledge: C++ templates, API design, interest in researching sparse arrays
- Project length: 350 hours
- Difficulty level: hard
- Potential mentors: Hameer Abbasi, [Gagandeep Singh](https://github.com/czgdp1807) (co-mentor)

### Your own idea

The above projects are just suggestions --- it is also very good to suggest a project idea of your own if you have something in mind that you want to do. Ask people on the [mailing list](https://mail.python.org/mailman3/lists/scipy-dev.python.org/) for suggestions in this case.

### And more...

A set of additional new feature ideas can be found on the [SciPy detailed Roadmap](https://scipy.github.io/devdocs/dev/roadmap-detailed.html).