### Authors: 
- [Vishal Gupta](https://py-ranoid.github.io/Resume) (student,UTC+5:30) 
- Nikolay Mayorov (mentor)

#### Created: 2018-02-25

***

### Rotation formalism in 3 dimensions

#### General info
- Required knowledge and skills: Python, understanding how to vectorize operations in numpy, ability to read and grasp papers/books on the subject
- Difficult level: easy to medium
- Potential mentors: Eric Larson, Nikolay Mayorov

#### Description
There are several ways to represent a rotation in 3-dimensional space: Euler angles, direction cosine (or rotation) matrices (DCM), quaternions, rotation vectors and some others. Different representations are preferable in different scenarios and there exists a correspondence between all of them. You can find a good overview in [1] and a more comprehensive treatment in [2]. Note that there are many different conventions in this field, one of which should be chosen and described properly. Also note that "rotation" and "orientation" can be used interchangeably: an orientation between two frames is determined by a rotation required to superimpose one frame onto another.

The aim of this project is to create a module which will allow to conveniently describe, apply and compose rotations. The proposed module name is `scipy.spatial.rotation` or if are looking for wider perspectives `scipy.spatial.transform`. The content of this module is preliminarily seen as follows:

1. The main class of the module may be called `Rotation`. 
   1. It should represent an arbitrary rotation or several rotations (i.e. we should aim for vectorized approach for efficiency). 
   2. It should be possible to create `Rotation` from any sensible representation and in vectorized fashion. The most widely used of them are listed above, more exotic parametrizations can also be considered.
   3. Internally `Rotation` should use either DCMs or quaternions to represent rotations. Both of these choices are good with some minor pros and cons.
   4. `Rotation` should be able to return any required representation, like for example we would like to know which Euler angles describe our rotation, etc. These representations can be returned as numpy arrays.
   3. `Rotation` should have methods to rotate or project a vector or a set of vectors. See [3] to get an idea about the difference of this views. Overall it should be intuitive and clear for the user what he is doing with which operation (i.e. it should be explained sufficiently in the documentation). Also here we need to consider how vectorized operations are performed, i.e. one rotation on many vectors, many rotations on one vector and many rotations on many vectors (most likely we need 1-to-1 correspondence in this case).
   4. `Rotation` should have a method (likely `__mul__`) to compute a representation of a consecutive application of two rotation, like `C = A * B`. If DCMs are used internally this composition comes down simply to matrix multiplication.
   5. The main difficulty in implementing this class is to implement conversions between an arbitrary representation to/from the internal representation. There are some peculiar points.
2. Apart from `Rotation` class we can include some useful algorithms regarding rotations. Some that I'm aware of:
   1. Interpolation between orientations using SLERP algorithm [4].
   2. Finding a rotation which gives the best match between the set of vectors measured in two frames [5].
   3. "Cubic spline" interpolation for the set of orientations [6].
   4. Optimal "averaging" of orientations [7].
   5. Orthogonalization of a 3x3 matrix, one of simpler approaches is described in [8].
   6. Uniform random sampling of rotations. One way to achieve this is to sample quaternions as unit vectors distributed uniformly on a unit sphere in 4D.

#### References

1. https://en.wikipedia.org/wiki/Rotation_formalisms_in_three_dimensions
2. "A Survey of Attitude Representation" by Malcolm D. Shuster
3. https://en.wikipedia.org/wiki/Rotation_matrix#Ambiguities
4. https://en.wikipedia.org/wiki/Slerp#Quaternion_Slerp
5. https://en.wikipedia.org/wiki/Wahba%27s_problem
6. http://qspline.sourceforge.net/qspline.pdf
7. "Quaternion Averaging" by F. Landis Markley et al.
8. "Unit Quaternion from Rotation Matrix" by F. Landis Markley