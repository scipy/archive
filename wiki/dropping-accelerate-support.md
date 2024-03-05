**UPDATE: the plan was implemented in [gh-8670](https://github.com/scipy/scipy/pull/8670) which is merged and appeared in 1.2.0 (december 2018)**

Motivation
----------

SciPy relies extensively on LAPACK and BLAS libraries and for that reason the SciPy building process involves linking to these Fortran sources. 
While building NumPy/SciPy is still a quite problematic area in Windows systems for the average users, the situation for Linux and OSX systems is quite the opposite if the documentation is followed. In the building procedure  for OSX systems, many users rely on the readily-provided Accelerate Framework by Apple, which among other tools, includes LAPACK and BLAS libraries.

Recently, this convenience that many still enjoy for OSX systems, has become a bottleneck for the SciPy development team for various reasons, mainly for the following: 

- Apple support for Accelerate (as for other Apple code) is opaque.  Bug reports, and replies to reports, are [private to the Apple engineers](https://developer.apple.com/bug-reporting/).  As a result we find ourselves having to patch around bugs that are due to Accelerate (e.g. [gh-7131](https://github.com/scipy/scipy/pull/7131), [#7050](https://github.com/scipy/scipy/issues/7050)). Because of the opaque support process, the Accelerate framework bugs are difficult to discover/blame.
- The APIs implemented by the LAPACK and BLAS libraries are outdated by about a decade.  Currently the LAPACK version is 3.7.1 vs. Accelerate's 3.2.1 from 2009.  This is an issue because Scipy cannot make use of recently introduced functionality in LAPACK (e.g. [gh-6831](https://github.com/scipy/scipy/pull/6831), [#7500](https://github.com/scipy/scipy/issues/7500)). Internal LAPACK deprecations create extra maintenance efforts across different versions (e.g., [#5266](https://github.com/scipy/scipy/issues/5266)).
- The new features to-be-added to SciPy are blocked by the absence of routines introduced in later versions LAPACK/BLAS libraries.
- Known issues/deprecations of LAPACK/BLAS need to be addressed at the SciPy level since later fixes can't be incorporated which adds complication for build processes.

We have thus far defaulted to maintaining Accelerate support because:

- Accelerate is present on every Mac, meaning that we do not have to install other libraries in order to build Numpy.
- It appears to be optimized for the hardware it is running on.
- At least by reputation, Accelerate has top-of-range or competitive performance.
- [Some users](http://vtk.1045678.n5.nabble.com/VTK-and-Python-on-OS-X-El-Capitan-tp5734265p5734280.html) want Accelerate support specifically, usually because they believe it gives the best performance.

We might be getting to the point where the cons outweigh the pros.  We are therefore considering alternative build options for OSX. This document is a summary of various discussions, mainly under [gh-6051](https://github.com/scipy/scipy/pull/6051).  

For any alternative building process, Accelerate (or parts of) needs to be overshadowed (See [gh-2620](https://github.com/scipy/scipy/pull/7131) for a similar attempt which was cancelled). 

## Options

See also discussion at [OpenBLAS for OSX numpy thread](https://mail.python.org/pipermail/numpy-discussion/2016-June/075681.html) continued [here](https://mail.python.org/pipermail/numpy-discussion/2016-July/075700.html).

### Keep supporting Accelerate as we do now

**Pros**: least effort, building/installing SciPy on OS X is easy.

**Cons**: cannot make use of recently introduced functionality in LAPACK (e.g. [gh-6831](https://github.com/scipy/scipy/pull/6831)) or fix bugs that are due to Accelerate (e.g. [gh-7131](https://github.com/scipy/scipy/pull/7131), [#7050](https://github.com/scipy/scipy/issues/7500)). Internal LAPACK deprecations create extra maintenance efforts across different versions (e.g., [#5266](https://github.com/scipy/scipy/issues/5266))

### Drop Accelerate support completely

**Pros**: can move to LAPACK x.y.z, can remove Accelerate patching in ``scipy._build_utils``

**Cons**: some people want to use Accelerate for performance reasons (see above). We force users to install another BLAS/LAPACK which is not easy right now. This could be addressed by shipping OpenBLAS with the Scipy wheel, or by packaging OpenBLAS as a wheel.  Packaging OpenBLAS as a wheel is a significant amount of work – we (@njsmith) know how to do it and have implemented the nasty binary rewriting stuff that's required, but work is still needed to set up build scripts etc. But in any case we don't need to decide this now, because we already have the infrastructure to ship OpenBLAS inside the wheel, just like we do on Linux.

Shipping a Numpy / OpenBLAS wheel is relatively trivial, using the existing [multibuild](https://github.com/matthew-brett/multibuild) / [delocate](https://github.com/matthew-brett/delocate) machinery - see [this PR](https://github.com/MacPython/numpy-wheels/pull/1) for the changes required.  The Delocate program copies the OpenBLAS library into the Numpy wheel.

### Keep using Accelerate BLAS but shadow LAPACK

The actual discussion is difficult to summarize and needs to be read through in [gh-6051](https://github.com/scipy/scipy/pull/6051). A brief recollection of the ideas proposed
- Using ``vecLibFort``, see https://github.com/scipy/scipy/pull/6051#issuecomment-225431271
- Just bundling missing + broken routines: https://github.com/scipy/scipy/pull/6051#issuecomment-225431600

and other possible options. 

**Pros**: Still utilize Accelerate for build convenience selectively.

**Cons**: Issues such as Integer overflow ([gh-7131](https://github.com/scipy/scipy/pull/7131)) is even present in fundamental BLAS functions like `*GEMM`. Even if we build LAPACK on top of Accelerate's CBLAS, it will still possibly be unstable and do not shield SciPy from further bugs in Accelerate.

## Other considerations

### Which minimum LAPACK version to support?

We've always used the guideline that the BLAS/LAPACK versions shipped with the
most popular Linux distributions should be supported until the distribution
becomes end-of-life.  The LAPACK versions shipped with the oldest not yet
end-of-life distributions are:

- Debian 7 (Wheezy): 3.4.1
- Ubuntu 14.04 LTS: 3.5.0
- Fedora 25: 3.6.1
- CentOS 7: 3.4.2

There are three BLAS/LAPACK libraries that we support on all platforms:

- Intel MKL 11.1.4 (latest supported MKL version for Python 2.7 on Windows, see https://github.com/scipy/scipy/pull/6051#issuecomment-329542591): 3.4.0 
- Intel MKL 11.3: 3.6
- OpenBLAS 0.2.20: 3.7.0
- ATLAS 3.10.3: 3.6.1

Supporting those old Linux distributions can be important, because users often
have to work on clusters running such distributions.  They can build the latest
SciPy version, and we'd like them to be able to do that without also having to
build a LAPACK library by themselves (that tends to be harder).

However, there's a couple of arguments we may want to not support Linux
distributions till their end-of-life:

1. It means we'll always be many years behind the latest LAPACK. E.g. CentOS 7
   is supported until 2020, and has LAPACK 3.4.1 from 2012.
2. On OS X and Windows we will require users to install a LAPACK library
   themselves.  If they can deal with it, then Linux users can too.
3. OpenBLAS has become stable enough for general use, and is *much* easier to
   compile than ATLAS.
4. We're going to have to provide OpenBLAS wheels for OS X users.  If we do
   that, then we can also provide ``manylinux`` wheels.

Those seem like compelling arguments for a more aggressive update strategy, and
require at least 3.5.0 or 3.6.0.  Another downside is that we will be making a
lot of install instructions out in the wild obsolete (they will all have
something like ``sudo apt-get install libatlas-dev``).

Another consideration could be our continuous integration needs.  TravisCI runs
Ubuntu LTS, so provides 3.5.0.  It's a minor issue compared with all the other
considerations though - easy enough to build 3.6.0 once and download it (or
grab it from the cache) for each CI run.

However, the most important factor seems to be MKL. MKL needs to be supported for all Python versions we support, because it's the default LAPACK used on Windows with Anaconda, Canopy, etc. Because MKL + Python 2.7 (needs MSVC 2008) only supports LAPACK 3.4.0, that is the highest we can bump the minimum supported version to.

### ABI issues with shadowing

MKL also uses a g77 ABI, see https://github.com/scipy/scipy/pull/6051#issuecomment-225431914 

### NumPy-related Impact

The scenario in which SciPy drops support for Accelerate but NumPy stays with it, has not been discussed yet.

There is also some discomfort raised in the NumPy mailing list about linking to Accelerate. A blocking issue example has been provided about multiprocessing which can be read [in this mailing list thread (with a quote from Apple)](https://mail.scipy.org/pipermail/numpy-discussion/2012-August/063589.html). This problem was due to a bug in multiprocessing and is fixed in Python 3.4 and later; Accelerate was POSIX compliant but multiprocessing was not.

## Rejected alternatives

Dropping all of LAPACK into SciPy (see https://github.com/scipy/scipy/pull/6051#issuecomment-266380190).