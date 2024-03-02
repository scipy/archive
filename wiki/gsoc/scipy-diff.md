#Proposal: add finite difference numerical derivatives as ``scipy.diff``

* Authors: Maniteja Nandana(student)
           Christoph Deil(mentor)
* Date Created: 2015-03-09
* Date Last Revised: 2015-03-24
* Status: methods / API discussion
* Potentially related issues: [#2035](https://github.com/scipy/scipy/issues/2035)

This is very much work in progress (see open questions at the end).

Feedback on scipy-dev or Github as well as co-authors welcome!

##Abstract

We propose to add a ``scipy.diff`` sub-package containing several finite difference numerical methods to
compute derivatives of functions. Roughly analogous to the existing ``scipy.integrate`` ([tutorial](http://docs.scipy.org/doc/scipy-dev/reference/tutorial/integrate.html),
[reference](http://docs.scipy.org/doc/scipy-dev/reference/integrate.html))
sub-package that contains various numerical integration methods.

There have been discussions on a potential ``scipy.diff`` over the past year on the scipy-dev mailing list and has been discussion in [issue 2035](https://github.com/scipy/scipy/issues/2035) about the need for methods to be able to compute derivatives in Scipy.

The purpose of this document is to have a concrete API and method specification, to be implemented during [Google Summer of code 2015](https://www.google-melange.com/gsoc/homepage/google/gsoc2015) under [scipy.diff project idea](https://github.com/scipy/scipy/wiki/GSoC-2015-project-ideas#implement-scipydiff-numerical-differentiation)

-------------------------------------------------------------------------------
##Introduction

To make sure everyone is on the same page, here's some motivation why we think ``scipy.diff``
should be added as well as background info on notation and differentiation methods.

###Motivation

Most scientific computing libraries contain functions for numerical differentiation.

####Numpy
1. [numpy.diff](http://docs.scipy.org/doc/numpy/reference/generated/numpy.diff.html)
2. [numpy.gradient](http://docs.scipy.org/doc/numpy/reference/generated/numpy.gradient.html)

####Scipy
1. [scipy.misc.derivative](http://docs.scipy.org/doc/scipy/reference/generated/scipy.misc.derivative.html)
2. [scipy.misc.central_diff_weights](http://docs.scipy.org/doc/scipy-dev/reference/generated/scipy.misc.central_diff_weights.html)

But the methods in ``numpy`` and ``scipy`` were recently introduced and are insufficient for many applications where precise derivative estimates are needed.

There are suitable methods implemented in 

####statsmodels.tools.numdiff 

[*Reference*](https://github.com/statsmodels/statsmodels/blob/master/statsmodels/tools/numdiff.py)

####numdifftools
[*Reference*](https://github.com/pbrod/numdifftools)

we feel that moving those and adding extra ones to ``scipy.diff`` would benefit Scipy itself (they could be used e.g. in ``scipy.stats`` or ``scipy.optimize``) as well as the scientific Python community (avoid everyone rolling their own).


###Notation

For a function ![equation](http://i.imgur.com/fObhHT2.png) the [derivative](http://en.wikipedia.org/wiki/Derivative) is defined as ![equation](http://i.imgur.com/vm4DiSA.png)

For multi-variate functions ![equation](http://i.imgur.com/1t6onPj.png) we denote the [partial derivatives](http://en.wikipedia.org/wiki/Partial_derivative) as ![equation](http://i.imgur.com/eCWd58V.png)

For higher-order derivatives we use the notation ![equation](http://i.imgur.com/4xwkPos.png) for
[univariate functions](http://en.wikipedia.org/wiki/Derivative#Higher_derivatives)

and ![equation](http://i.imgur.com/FYiHID6.png) for [multivariate functions](http://en.wikipedia.org/wiki/Partial_derivative#Higher_order_partial_derivatives)

``Note``: we do **not** plan to directly support [multi-valued functions](http://en.wikipedia.org/wiki/Multivariable_calculus) ![equation](http://i.imgur.com/hOXhpab.png) in the ``scipy.diff`` API. Users that want to compute derivatives of such functions can loop over and process one single-valued component function ![equation](http://i.imgur.com/tffmULg.png) at a time.

###Methods

There are different methods to compute derivatives that greatly vary in terms of
generality (which functions they can be used for), speed and precision([comment](https://github.com/scipy/scipy/issues/2035#issuecomment-23628615))

Here we'd like to mention and briefly discuss these:

1. [Symbolic differentiation](http://en.wikipedia.org/wiki/Symbolic_computation)
2. [Automatic differentiation](http://en.wikipedia.org/wiki/Automatic_differentiation)
3. [Finite differences](http://en.wikipedia.org/wiki/Finite_difference)

####Symbolic differentiation

If your function is given by an analytic formula ![equation](http://i.imgur.com/cWifAAV.png)
it is usually possible to compute the formula for the derivatives ![equation](http://i.imgur.com/5bM2AeQ.png)
and ![equation](http://i.imgur.com/fOMqwEc.png)

Implementing these derivatives as separate functions results in very fast and precise
derivative computations and using them as part of your application.(e.g.
[scipy.optimize.minimize](http://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.minimize.html)
accepts `jac` and `hess` functions to compute first and second order
derivatives for a given function `fun`)

Computing the derivative formulas can be done with
[symbolic computation](http://en.wikipedia.org/wiki/Symbolic_computation) tools like
[Sympy](http://www.sympy.org/), even auto-generating and evaluating derivatives as part of
a larger Python application is possible.

Note that many functions are **not** given by formulae and this technique can't be applied.

Symbolic differentiation was considered out of scope for ``scipy`` from previous discussions among devs and will not be further considered.

####Automatic differentiation

Automatic differentiation](http://en.wikipedia.org/wiki/Automatic_differentiation) is a technique to compute function derivatives in a very fast and precise way.

It is very popular (see e.g.[Autodiff](http://www.autodiff.org/) or here [Julia](http://www.juliadiff.org),
there's currently 10 Python packages implementing it listed [here](http://en.wikipedia.org/wiki/Automatic_differentiation#Software)

The main drawbacks are that it doesn't work for all functions (only those that can be introspected
and decomposed into steps on which the [chain rule](http://en.wikipedia.org/wiki/Chain_rule>)
can be applied) and often requires the user to modify their function implementation.

There were comments that automatic differentiation could be in scope for ``scipy.diff`` and e.g.
the existing [algopy](https://github.com/b45ch1/algopy) and [ad](https://github.com/tisimst/ad) packages could be used as a basis.

We do not consider automatic differentiation further here, but if possible would like to implement
and API for ``scipy.diff`` that makes it possible to add it in the future as an extra method.

####Finite differences

The method we actually propose should be implemented in ``scipy.diff`` (see [here](http://en.wikipedia.org/wiki/Finite_difference) and [here](http://en.wikipedia.org/wiki/Numerical_differentiation#Finite_difference_formula).

It's biggest advantage is that it is completely general. It works for any input function
to be differentiated, the function is only evaluated at some points, it can be considered a black box.
Also derivatives of various orders can be very easily computed simply by using [different coefficients](http://en.wikipedia.org/wiki/Finite_difference_coefficient)

However the finite difference method is very imprecise because of
[round-off error](http://en.wikipedia.org/wiki/Round-off_error) for small step sizes ``h``
as explained and illustrated [here](http://en.wikipedia.org/wiki/Numerical_differentiation#Practical_considerations_using_floating_point_arithmetic)

A variety of adaptive methods that systematically vary the step size ``h`` or extrapolate to ![equation](http://i.imgur.com/o8lOi89.png) have been developed, increasing the precision of the derivative estimate at the cost of more function evaluations.

Another approach is to use the [complex step derivative approximation] (http://mdolab.engin.umich.edu/sites/default/files/Martins2003CSD.pdf) if the function is analytic and supports complex value inputs.

![equation](http://i.imgur.com/DUsKsaN.png)

The challenge is to identify the handful of methods that provide best stability and accuracy for a given cost
(number of function evaluations), giving users suitable tools for all applications.

###Overview of other packages

TODO: is there a paper or book or webpage giving an overview?

If no, we can briefly describe them here:


See section 5.7 "Numerical Derivatives" (page 186) in "Numerical Recipes in C":
http://apps.nrbook.com/c/index.html

#### GNU Scientific Library

* https://www.gnu.org/software/gsl/manual/html_node/Numerical-Differentiation.html
* https://www.gnu.org/software/gsl/manual/html_node/Numerical-Differentiation-functions.html#Numerical-Differentiation-functions
* https://github.com/ampl/gsl/blob/master/deriv/deriv.c
* https://root.cern.ch/drupal/content/function-derivation

####Statsmodels
* https://github.com/statsmodels/statsmodels/blob/master/statsmodels/tools/numdiff.py
* https://www.kent.ac.uk/smsas/personal/msr/webfiles/complexstep/deriv2.pdf

####Numdifftools
* https://github.com/pbrod/numdifftools/blob/master/numdifftools/core.py
* https://github.com/pbrod/numdifftools/blob/master/numdifftools/nd_algopy.py

####Julia
* http://www.juliadiff.org/

####Algopy
* https://github.com/b45ch1/algopy

####AD
* https://github.com/tisimst/ad

####R
* http://cran.r-project.org/web/packages/numDeriv/

####MATLAB
* http://in.mathworks.com/help/matlab/numerical-integration-and-differentiation.html

###Proposed API for ``scipy.diff``

Analogy to scipy.integrate (which contains functions that take functions or points as input):
http://docs.scipy.org/doc/scipy-dev/reference/integrate.html

Examples:
http://docs.scipy.org/doc/scipy-dev/reference/generated/scipy.integrate.quad.html
http://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.minimize.html

The classes as in [nd_cstep.py](https://github.com/pbrod/numdifftools/blob/master/numdifftools/nd_cstep.py) can be

     Derivative()
       def __init__(f, h=None, method=’central’, full_output=False)
       def __call__(self, x, *args, **kwds)

     Gradient():
       def __init__(f, h=None, method=’central’, full_output=False)
       def __call__(self, x, *args, **kwds)

     Jacobian():
       def __init__(f, h=None, method=’central’, full_output=False)
       def __call__(self, x, *args, **kwds)
 
     Hessian():
       def __init__(f, h=None, method=’central’, full_output=False)
       def __call__(self, x, *args, **kwds)

The classes in [core.py](https://github.com/pbrod/numdifftools/blob/master/numdifftools/core.py) have to be refactored into the following class structure, where the additional options like ``vectorizate=False`` to be removed to be made uniform with the rest of API structure.

     NDerivative():
       def __init__(f, n=1, h=None, method=’central’, full_output=False, **options)
       def __call__(self, x, *args, **kwds)

Where options could be

       Options = dict(order=2, Romberg_terms=2)

arguments

     f  : callable function

     x : ndarray values at which the derivative needs to be calculated

     method : str method to be used to approximate the derivative - 'central', 'forward', 'backward', 'complex', 'richardson'

     n : Integer from 1 to 4 (Default 1) defining derivative order. Only 1 for complex method

     order : Integer from 1 to 4 (Default 2) defining order of basic method used. For 'central' methods, it must be from the set [2,4].
  
     Romberg_terms : number of terms used in Romberg extrapolation

     args : tuple arguments for the function f

     kwrds : dict Keyword arguments for function `f`.

     full_output : bool Set to True to print error messages.

return 

     res : DiffResult

     The differentiation result represented as a DiffResult object. Important attributes are:

         x: ndarray solution array,

         success : bool a flag indicating if the derivative was calculated successfully

         message : str which describes the cause of the error, if occurred

         number_of_func_eval : int number of function evaluations

         abserr  : abserr_round + abserr_truncate : float absolute value of the roundoff and truncation errors, if applicable

####TODO
* whether the ``h=None`` default would mean best step-size found using by around ![equation](http://i.imgur.com/N9SK08f.png) where s depends on the method and derivative order or ``[StepGenerator](https://github.com/pbrod/numdifftools/blob/master/numdifftools/nd_cstep.py#L128)``, based on  epsilon algorithm by wynn.
* Whether the *args and **kwds should be in ``__init__`` or ``__call__``, the preference by Perk was for it being in ``__call__`` makes these object compatible with ``scipy.optimize.minimize(fun, x0, args=(), method=None, jac=None, hess=None,…..)`` where the args are passed both to the function and jac/hess if they are supplied.
* Are the input arguments for the ``__init__`` sufficient ?
* What should we compute and return for ``full_output=True``, are the present output terms in ``DiffResult`` sufficient ?
* Make and organize a pool of univariate scalar functions with known derivatives up to 4 which can be used for testing/performance purposes.
 * https://github.com/b45ch1/algopy/blob/master/algopy/nthderiv/nthderiv.py
 * https://github.com/b45ch1/algopy/blob/master/algopy/tests/test_nthderiv.py
* Make and organize a pool of  functions with known gradient/Jacobian/hessian which can be used for testing/performance purposes. (Maybe something can be taken from statsmodels)
 * https://github.com/statsmodels/statsmodels/blob/master/statsmodels/tools/tests/test_numdiff.py

#### Classes v/s Functions

Thanks to @Per Brodtkorb for this reasoning

The class interface better than the functional one because you can pass the resulting object as function to other methods/functions and these functions/methods do not need to know what it does behind the scenes or what options are used. This simple use case is exemplified here:

    g = lambda x: 1./x
    dg = Derivative(g, **options)
    my_plot(dg)
    my_plot(g)

In order to do this with a functional interface one could wrap it like this:

    dg2  = lambda x: fprime(g, x, **options)
    my_plot(dg2)


If you like the one-liner that the function gives, you could call the Derivate class like this
   
    Derivate(g, **options)(x)

Which is very similar to the functional way:

    fprime(g, x, **options)

###Proposed methods for ``scipy.diff``

Statsmodels and Numdifftools vary in aspects of speed and accuracy, in terms of approaches followed as mentioned in [comment](https://github.com/scipy/scipy/pull/2835#issuecomment-52372036)


####Adaptive step methods

* Richardson extrapolation and Romberg terms
* Tools to estimate optimal step size ``h``
* What [numdifftools](https://github.com/statsmodels/statsmodels/blob/master/statsmodels/tools/numdiff.py) does
* Numdifftools uses adaptive step-size to calculate finite differences, but will suffer from dilemma to choose small step-size to reduce truncation error but at the same time avoid subtractive cancellation at too small values.

####Fixed complex step method

* What's in [statsmodels](https://github.com/statsmodels/statsmodels/blob/master/statsmodels/tools/numdiff.py)
* Central, forward, backward difference up to third derivative for O(h^2) and O(h^4) accuracy?
* http://en.wikipedia.org/wiki/Finite_difference_coefficient
* Statsmodels used complex step derivatives, which are for first order derivatives and have only truncation error, no roundoff error since there is no subtraction.
* the complex-step method is only for first order derivatives and needs that function is analytic, so that Cauchy-Riemann equations are valid. So, is it possible to differentiate any function with this ?

###Acknowledgements

We would like to thank everyone that has given feedback on this document or ``scipy.diff`` in general
via Github or scipy-dev or private email.

* Alex Griffing (@argriffing)
* Ralf Gommers (@rgommers)
* Josef Perktold (@josef-pkt)
* Per Brodtkorb (@pbrod)
* Abraham Lee(@tisimst)
* Sebastian Walter (@b45ch1)
* Pauli Virtanen (@pv)

-------------------------------------------------------------------------------

###To be discussed / feedback needed

This is a list of open questions that are being discussed.
This sub-section will be removed soon.

* Is the name ``scipy.diff`` the best choice, or would people prefer something else (e.g. ``scipy.derivative``)?
  * It shouldn't be a problem later to take care of this

* API: Handling broadcasting behavior along axes for input points  (R^n and array of points)?

* Which methods?
  * Complex step method?

* API: Classes or Functions
  * Functions as in scipy.optimize (minimize, root) is better, since it is coherent with API
  * Discussed above in API

* API: Functions as input / output or x / y values?
  * Functions as input is the first priority

* API: Return results object with access to full info?
  * There will be cases where you want to return more info than (derivative estimate, derivative error estimate), e.g. number of function calls or even the function samples or a status code.
  * It’s easy to attach useful extra info to the results object, and the extra cost for simple use cases of having to type `.value` to get at the derivative estimate is acceptable.

* In scope? Parallel evaluation of function values to make use of multi-core? If yes, how (multiprocessing)?
  * Though useful, preferably out of scope for now until any other feedback is possible

* Automatic differentiation (AD) experts: is it possible to add AD methods to ``scipy.diff``
  later with the current API? Is there a different API that would make it easier?
  * still need feedback

###References

* DERIVEST, John, R. Errico [link](https://github.com/pbrod/numdifftools/blob/master/docs/DERIVEST.pdf)

* The Complex-Step Derivative Approximation, JOAQUIM R. R. A. MARTINS [link](http://mdolab.engin.umich.edu/sites/default/files/Martins2003CSD.pdf)

* Statistical Applications of the Complex-step Method of Numerical Differentiation, M. S. RIDOUT [link](https://www.kent.ac.uk/smsas/personal/msr/webfiles/complexstep/deriv2.pdf)

* Numerical Methods Using Matlab, John H. Mathews and Kurtis K. Fink [link](mathfaculty.fullerton.edu/mathews/n2003/differentiation/numericaldiffproof.pdf)

* Using Complex Variables to Estimate Derivatives of Real Functions, William Squire and George Trapp [link](http://www.jstor.org/stable/2653003)

* Richardson Extrapolation and Romberg Integration [link](http://www.eng.utah.edu/~cs6210/lecture24.pdf)

* NONLINEAR SEQUENCE TRANSFORMATIONS FOR THE ACCELERATION OF CONVERGENCE AND THE SUMMATION OF DIVERGENT SERIES [link](arxiv.org/pdf/math/0306302v1.pdf)