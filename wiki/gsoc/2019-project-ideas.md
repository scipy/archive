## Introduction

This is the Google Summer of Code 2019 (GSoC'19) ideas page for SciPy.  The SciPy library is one of the core packages that make up the SciPy stack for scientific computing with Python. It provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization.

This page lists a number of ideas for Google Summer of Code projects for SciPy, plus gives some pointers for potential GSoC students on how to get started with contributing and putting together their application. 

### Guidelines & requirements

SciPy plans to participate in GSoC'19 under the [umbrella of Python Software Foundation](http://python-gsoc.org). 

We expect from students that they're at least comfortable with Python (intermediate level). Some projects may also require Cython or C skills. Knowing how to use Git is also important; this can be learned before the official start of GSoC if needed though.

If you have an idea of what you would like to work on (see below for ideas) and are considering participating:

1. Read the [PSF page](http://python-gsoc.org/) carefully, it contains important advice on the process.
2. Read [advice on writing a proposal](http://turnbull.sk.tsukuba.ac.jp/Blog/SPAM.txt#how-to-spam-in-detail) (written with the Mailman project in mind, but generally applicable)
3. Look at [the guidelines on how to contribute to Scipy](http://scipy.github.io/devdocs/hacking.html).
4. Make a enhancement/bugfix/documentation fix -- it does not have to be big, and it does not need to be related to your proposal. Doing so before applying for the GSoC is a hard requirement for SciPy. It helps everyone you get some idea how things would work during GSoC.
5. Start writing your proposal early, post a draft to the [scipy-dev mailing list](https://www.scipy.org/scipylib/mailing-lists.html) and iterate based on the feedback you receive. This will both improve the quality of your proposal and help you find a suitable mentor.

### Contact

If you have a question *after checking all guideline pages above*, you can email the [scipy-dev mailing list](https://www.scipy.org/scipylib/mailing-lists.html).

## SciPy Project ideas

### Revamp scipy.fftpack

Revamping the `scipy.fftpack` interface will allow us to address a number of maintenance issues, and increase performance (both accuracy and speed). Possible goals and related benefits:

- In general it would be good to have a backend system for various 3rd party fft implementations, such as [pyFFTW](https://github.com/pyFFTW/pyFFTW), [mkl-fft](https://github.com/IntelPython/mkl_fft), and possibly [CuPy](https://cupy.chainer.org/). These libraries provide various features such as pre-planned transforms, multi-threading, support for long-double precision and/or GPU support that do not exist in SciPy's fftpack. pyFFTW, mkl-fft and CuPy provide fftpack-compatible functions and it is possible to use pyFFTW to [monkeypatch SciPy](https://hgomersall.github.io/pyFFTW/sphinx/tutorial.html#monkey-patching-3rd-party-libraries). It would be preferable to instead have SciPy provide a formal backend interface for allowing 3rd party fft implementations to be used in place of scipy's fftpack.
- Once a fft backend system has been defined, it would be useful to users provide some example of their use and relative performance (e.g. expanding scipy's existing fft benchmarks or providing IPython notebooks to demonstrate the relative performance).
- A stretch goal related to the backend system would be to contribute to third party libraries such as pyFFTW to fill in existing gaps in their functionality to provide complete coverage of the functions currently available in scipy.fftpack. For pyFFTW and cupy, the gap is mainly in the lack of real-to-real transforms (discrete cosine transform and discrete sine transform).

Outside of providing a system for handling different fft backends, there are other potential goals related to improving FFT support in SciPy.

- NumPy now has [pocketfft](https://github.com/numpy/numpy/pull/11888), we should also have it for SciPy. Of particular interest regarding performance is the Bluestein algorithm (or chirp Z-transform), which we have been wanting to add to fftpack for a long time.
- The APIs of numpy.fft and scipy.fftpack [should agree better](https://github.com/scipy/scipy/issues/2487). This is a lower priority because it's hard (requiring lots of discussion on impact on users if we deprecate things, etc.), but it's an important one as well. The large overlap with numpy.fft has to change (both are too widely used to deprecate one); in the documentation we should make clear that scipy.fftpack is preferred over numpy.fft. If there are differences in signature or functionality, the best version should be picked case by case (example: numpy’s rfft is preferred, see gh-2487).
- We probably want to deprecate fftpack.convolve as a public function (it was not meant to be public). 

This project will require in-depth API thinking, and robust, possibly extensive discussions with other devs on GitHub and the SciPy mailing lists. A basic familiarity with discrete Fourier transforms will be useful in understanding and contributing to the project.

- Required knowledge: Python, linear algebra
- Difficulty level: medium
- Potential mentors: Gregory Lee and Eric Larson

(Ideas and text adapted from [scipy-dev](https://mail.python.org/pipermail/scipy-dev/2018-December/023221.html) and the [scipy detailed roadmap](https://scipy.github.io/devdocs/roadmap-detailed.html#fftpack).)

### Improve ODE solvers

Since version 1.0 scipy includes a set of ODE [solvers](http://scipy.github.io/devdocs/generated/scipy.integrate.solve_ivp.html#scipy.integrate.solve_ivp) implemented in pure Python. It gives the advantage of the ease of their modification and extension. There are many possible ways to improve and refine the existing solver or implement new ones. The exact plan of work should be determined by a student, based on his or her expertise and interests. Here we list possible directions:

1. Implement a test/benchmark suite of ODE/DAE problems. A good starting point is https://archimede.dm.uniba.it/~testset
2. Implement DOP853 Runge-Kutta method. This high-order method, popular in celestial mechanics, has a rather complex math behind it and a non-trivial implementation. There exists a canonical Fortran [source code](http://www.unige.ch/~hairer/prog/nonstiff/dop853.f), however its literal translation into Python 
doesn't seem a satisfactory or viable approach. Ideally, a student should produce a thorough and easy-to-understand theoretical derivation of the core formulas of the method as a part of his work. The ideas behing the method are explained in "Solving Ordinary Differential Equations, Part I". There is an [ongoing work](https://github.com/scipy/scipy/pull/9290), which is likely to be correct but needs to be checked, explained (in terms of math) and finished.
3. Improve adaptive step-size control strategies for better computational stability and predictable behavior as suggested [here](https://github.com/scipy/scipy/issues/9822). This item is going to require a lot of experiments, tuning and ad-hoc decisions. A suite of test problems is going to be essential.
4. Implement a solver of implicit differential equations and [differential-algebraic equations](https://en.wikipedia.org/wiki/Differential-algebraic_system_of_equations). A suitable form for such equations is ``M(t, y) y' = f(t, y)`` and in case of DAEs matrix `M(t, y)` is singular. It seems that this solver is better to be implemented as a separate function, focused on a high-quality implementation of a single algorithm. This task assumes selecting a suitable algorithm, its thorough understanding, API design, implementation and testing.
5. Implement a solver of [delayed differential equations](https://en.wikipedia.org/wiki/Delay_differential_equation). There are several possible types and forms of such equations, a most appropriate of which must be selected. For the rest, this task is similar to the previous one.
6. Student own ideas.

A reasonable plan would be to work on 2 and either 1 and 3 or one of 4 and 5.

- Required knowledge and skills: Python, strong background in mathematics or numerical methods, ability to grasp essential information from papers and books
- Difficulty level: medium to high
- Potentail mentors: Nikolay Mayorov, Peter Solfest

### Your own idea

The above projects are just suggestions --- it is also very good to suggest a project idea of your own if you have something in mind that you want to do. Ask people on the [mailing list](http://scipy.org/scipylib/mailing-lists.html) for suggestions in this case.

### And more...

A set of additional new feature ideas can be found on the [Scipy Roadmap](http://scipy.github.io/devdocs/roadmap.html).