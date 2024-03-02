## Introduction

This is the Google Summer of Code 2021 (GSoC'21) ideas page for SciPy.  The SciPy library is one of the most widely used libraries for scientific computing with Python. It provides many user-friendly and efficient numerical routines for everything from linear algebra and numerical optimization to statistics and graph algorithms.

This page lists a number of ideas for Google Summer of Code projects for SciPy, plus gives some pointers for potential GSoC students on how to get started with contributing and putting together their application. 

### Guidelines & requirements

SciPy plans to participate in GSoC'21 under the [umbrella of Python Software Foundation](http://python-gsoc.org). 

We expect from students that they're at least comfortable with Python (intermediate level). Some projects may also require Cython or C skills. Knowing how to use Git is also important; this can be learned before the official start of GSoC if needed though.

If you have an idea of what you would like to work on (see below for ideas) and are considering participating:

1. Read the [PSF page](http://python-gsoc.org/) carefully, it contains important advice on the process.
2. Read [advice on writing a proposal](http://turnbull.sk.tsukuba.ac.jp/Blog/SPAM.txt#how-to-spam-in-detail) (written with the Mailman project in mind, but generally applicable)
3. Look at [the guidelines on how to contribute to SciPy](http://scipy.github.io/devdocs/dev/hacking.html).
4. Make a enhancement/bugfix/documentation fix -- it does not have to be a large PR, and it does not need to be related to your proposal. Doing so before applying for the GSoC is a hard requirement for SciPy. It helps everyone by providing some idea on how things would work during GSoC.
5. Start writing your proposal early, post a draft to the [scipy-dev mailing list](https://www.scipy.org/scipylib/mailing-lists.html) and iterate based on the feedback you receive. This will both improve the quality of your proposal and help you find a suitable mentor.

### Contact

If you have a question *after checking all guideline pages above*, you can email the [scipy-dev mailing list](https://www.scipy.org/scipylib/mailing-lists.html).

## SciPy Project ideas

### Improve performance through use of Pythran or Cython

SciPy has long used [Cython](https://cython.org/) as a tool to improve performance of code that would be too slow as pure Python. More recently we added experimental support for [Pythran](https://github.com/serge-sans-paille/pythran), to make it easier to accelerate Python code. Furthermore we use [Airspeed Velocity](https://asv.readthedocs.io/) for performance benchmarking (see [code](https://github.com/scipy/scipy/tree/master/benchmarks) and [published results](https://pv.github.io/scipy-bench/)). This project may include:

- writing new benchmarks for functionality in SciPy,
- accelerating algorithms with Pythran or Cython,
- if the student sees opportunities to do so: improve the documentation or contributor workflow around writing and running benchmarks

Functionality in any SciPy submodule that is performance sensitive can be worked on. Modules like `scipy.stats` and `scipy.optimize` have a lot of algorithms that could be accelerated.

- Required knowledge: Python is required, experience with C/C++/Pythran/Cython or benchmarking tools is helpful but not required
- Difficulty level: easy-medium
- Potential mentors: Ralf Gommers, Serge Guelton


### Add type annotations to a submodule

NumPy 1.20 (Dec'20) was the first NumPy release with support for type annotations. This makes it possible to add type annotations to SciPy as well. Early examples include [this PR for `spatial.distance`](https://github.com/scipy/scipy/pull/13448) and [these annotations for `stats.qmc`](https://github.com/scipy/scipy/blob/master/scipy/stats/_qmc.pyi). Because type annotations are so new and SciPy wasn't designed with them in mind, this project may be more challenging than expected. The project may include:

- Writing type annotations for a submodule
- Ensuring we can test type annotations in continuous integration with Mypy
- If needed, report issues or contribute improvements to NumPy's type annotations

- Required knowledge: Python is required, experience with Mypy or knowledge of type systems is helpful but not required
- Difficulty level: medium
- Potential mentors: Ralf Gommers, Melissa Weber Mendonça


### Experiment with transitioning SciPy to a new build system

SciPy is currently built with `numpy.disutils`, which relies on `distutils` and `setuptools`. `distutils` is deprecated, and will be removed in Python 3.12 in ~2.5 years time. Transitioning from `disutils` to `setuptools` is a fair amount of work. And because that would still leave us with a very poor build system, now is a good time to explore switching to a better build system. Meson and CMake are the two obvious candidates. Benefits would include: faster/parallel builds, better support for cross-compiling, less maintenance both for SciPy's build tooling and for `numpy.distutils`. Meson seems preferred because of its better docs and clean pure Python codebase, although CMake can be explored in the proposal phase too. The goal of this project is to get SciPy to build with Meson, so we can make an informed decision about switching to it. Activities may include:
- Making a choice about build system together with SciPy maintainers and input from the wider community (this conversation could be started before the coding period)
- Doing a small proof-of-concept with one or a couple of SciPy submodules
- Extending to more submodules, ensuring we cover different languages and code generation patterns
- Identifying and discussing solutions to issues for distributing SciPy (e.g. on PyPI and conda-forge), as well as developer workflows.

See https://github.com/scipy/scipy/issues/13615 for more details.

This is a challenging project, which could have a major impact on SciPy if it's successful. 

- Required knowledge: Python, as well as at least some experience building C, C++, Cython or Fortran code, are required
- Difficulty level: hard
- Potential mentors: Ralf Gommers, Matti Picus

### Object-oriented design of digital filtering in scipy.signal

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
- Difficulty level: medium-hard
- Potential mentors: Nikolay Mayorov

### Integrate library UNU.RAN into scipy.stats

The goal is to integrate the functionality of the C library UNU.RAN (http://statmath.wu.ac.at/software/unuran/) into SciPy. UNU.RAN is a C library that contains a collection of algorithms for generating non-uniform pseudorandom variates. It is designed to provide a consistent tool to sample from distributions with various properties. Its emphasis is on the generation of non-standard distributions. Since there is no universal method that fits for all situations, various methods for sampling are implemented. Adding such methods to scipy.stats would help to improve the available functionality for random variate generation.

- Required knowledge: Experience with Python, C / Cython and knowledge in probability theory / statistics is required. 
- Difficulty level: medium-hard
- Potential mentors: Christoph Baumgarten, Nicholas McKibben

### Your own idea

The above projects are just suggestions --- it is also very good to suggest a project idea of your own if you have something in mind that you want to do. Ask people on the [mailing list](http://scipy.org/scipylib/mailing-lists.html) for suggestions in this case.

### And more...

A set of additional new feature ideas can be found on the [SciPy detailed Roadmap](http://scipy.github.io/devdocs/roadmap-detailed.html).