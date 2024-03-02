### Personal Info :

Name : Ankit Agrawal  
Email : aaaagrawal@iitb.ac.in  
github : [ankit-maverick](https://github.com/ankit-maverick)  
IRC nick : ankit_agrawal  
Skype : aaaagrawal  
Blog :  http://waveletsinscipy.blogspot.com/
GSoC RSS Feed :  http://waveletsinscipy.blogspot.com/feeds/posts/default/-/GSoC/?alt=rss
Telephone : Provided upon request  
Timezone : IST (UTC +5:30)  
University : Indian Institute of Technology(IIT), Bombay  
Major : Electrical Engineering with Masters in Communication and Signal Processing  
Current Year : Fourth year  
Expected Graduation date : June 2015  
Degree : Dual Degree(Bachelors + Masters in 5 yrs)   



### Personal Bio :
I am Ankit Agrawal, a fourth year student enrolled in a 5 year Dual Degree Program(B.Tech and Masters) in Electrical Engineering at IIT Bombay. My Masters specialization is in Communication and Signal Processing and I will pursue my Master's thesis along the lines of Machine Learning and Computer Vision. The relevant coursework that I have done in the past related to this project are Linear Algebra, Signals and Systems, Digital Signal Processing, Image Processing, Wavelets and Filter Banks*, Matrix Computations*, Probability and Stochastic Processes etc. I participated in GSoC 2013 under PSF with scikit-image, where I implemented some Image Feature Detectors and Binary Feature Descriptors(http://skimager.blogspot.in/). I have also made some minor contributions to other open source libraries in Python while peeking into specific parts of their codebase.


### Proposal Title :
#### SciPy : Discrete Wavelet Transforms and related algorithms  


### Proposal Abstract :
Discrete Wavelet Transform has been one of the important features missing from scipy.signal module and is a milestone in the Scipy 1.0 roadmap [1]. This project will start off by integrating the rgommers/pywt fork of the existing PyWavelets project into scipy.signal after some important API changes, followed by the implementation of 1D and 2D inverse Stationary Wavelet Transform. A private module of pywt will be included in scikit-image to support Image denoising algorithms like Sureshrink and Co. while preserving its compatibility with older scipy versions. Finally, a tutorial outlining some applications of Wavelets will be created for the general user to go through.


### Timeline :

##### Community Bonding period (21st April - 18th May):
* Reading papers more thoroughly and discussing implementation details
* Getting more familiar with the code-base

##### Week 1 and 2 (19th May - 1st June)
* API changes. This would involve introducing a new class for objects returned by wavedec function, adding idwtn and other changes discussed at [2].

##### Week 3 (2nd June - 8th June)
* Migrating rgommers/pywt into scipy.signal.
* Improving docs and adding a small tutorial describing how the API can be pipelined to perform some simple tasks using Wavelets. 

##### Week 4 and 5 (9th June - 22nd June)
* Introducing a private module _pywt into scikit-image to preserve scikit-image's compatibility with older scipy versions
* Modify and merge @thearn's PR[3] containing BayesShrink and VisuShrink on top of the _pywt module.

##### Mid-term Evaluation (23rd June - 27th June)
* Buffer period for completing any incomplete work

##### Week 6 (28th June - 4th July)
* 1d and 2d Inverse Stationary Wavelet Transform(iswt and iswt2).

##### Week 7, 8, 9 and 10(5th July - 3rd Aug)
* Implementing SureShrink Denoising method[4]
* Implementing wavelet based image compression algorithms[5]

##### Week 11 (4th Aug - 10th Aug)
* Creating a tutorial that illustrates how Wavelets can be used in applications like Signal and Image Denoising and Compression, Time Series data Forecasting etc.

##### Week 12 - Pencils Down Date (11th Aug - 17th Aug)
* Buffer Period for completing any incomplete work
* Making sure the existence of good test coverage and documentation

##### Endterm Evaluation (18th Aug - 22nd Aug)


### Patches :
* Correcting the normalization of chebwin window function(https://github.com/scipy/scipy/pull/3433)
* Taking on API issues in rgommers/pywt (https://github.com/rgommers/pywt/pull/49)


### Schedule Information :
My endterms for the current semester would end around 3rd May. My next semester would start in the last week of July and even though I would be able to devote at least 3-4 hrs a day during this period(because I have only 3 elective courses remaining to take), I would start coding by the 2nd week of May i.e. during the Community Bonding period to get a good head-start.  


### References and Links :

[(1)](https://github.com/scipy/scipy/pull/2908/files#diff-e79eb3278b3f95f251c02522330d7b1aR232) DWT in Scipy 1.0 Roadmap 

[(2)](https://github.com/rgommers/pywt/issues/38) rgommers/pywt/#38 : API issues to discuss or change

[(3)](https://github.com/scikit-image/scikit-image/pull/760) scikit-image/#760 : Implemented Wavelet Filter

[(4)](https://groups.google.com/forum/#!searchin/pywavelets/iswt/pywavelets/bNFdhb6D5r0/9LnLdpW-PCsJ) Mike Marino's implementation of 1d iswt

[(5)](http://statweb.stanford.edu/~imj/WEBLIST/1995/ausws.pdf) Adapting to Unknown Smoothness via Wavelet Shrinkage

[(6)](http://www.mathworks.com/help/wavelet/index.html) Matlab Wavelet Toolbox