## RcppCNPy [![Build Status](https://travis-ci.org/eddelbuettel/rcppcnpy.svg)](https://travis-ci.org/eddelbuettel/rcppccnpy) [![License](http://img.shields.io/badge/license-GPL%20%28%3E=%202%29-brightgreen.svg?style=flat)](http://www.gnu.org/licenses/gpl-2.0.html) [![CRAN](http://www.r-pkg.org/badges/version/RcppCNPy)](http://cran.r-project.org/package=RcppCNPy) [![Downloads](http://cranlogs.r-pkg.org/badges/RcppCNPy?color=brightgreen)](http://www.r-pkg.org/pkg/RcppCNPy)

Rcpp bindings for NumPy files

### About

This package uses the [cnpy](https://github.com/rogersce/cnpy) library
written by Carl Rogers to provide read and write facilities for files created
with (or for) the NumPy extension for Python.  Vectors and matrices of
numeric types can be read or written to and from files as well as compressed
files. Support for integer files is available if the package has been built
with -std=c++11 which is the default starting with release 0.2.3 following
the release of R 3.1.0, and available on all platforms following the release
of R 3.3.0 with the updated 'Rtools'.

### Example

The following Python code

```{.python}
>>> import numpy as np
>>> fm = np.arange(12).reshape(3,4) * 1.1
>>> fm
array([[  0. ,   1.1,   2.2,   3.3],
       [  4.4,   5.5,   6.6,   7.7],
       [  8.8,   9.9,  11. ,  12.1]])
>>> np.save("fmat.npy", fm)
>>> 
>>> im = np.arange(3,4)
>>> im = np.arange(12).reshape(3,4)
>>> im
array([[ 0,  1,  2,  3],
       [ 4,  5,  6,  7],
       [ 8,  9, 10, 11]])
>>> np.save("imat.npy", im)
>>> 
```

saves two matrices in floating-point and integer representation.

With this R code we can read and assign the files:

```{.r}
R> library(RcppCNPy)
R> fmat <- npyLoad("fmat.npy")
R> fmat
     [,1] [,2] [,3] [,4]
[1,]  0.0  1.1  2.2  3.3
[2,]  4.4  5.5  6.6  7.7
[3,]  8.8  9.9 11.0 12.1
R> 
R> imat <- npyLoad("imat.npy", "integer")
R> imat
     [,1] [,2] [,3] [,4]
[1,]    0    1    2    3
[2,]    4    5    6    7
[3,]    8    9   10   11
R> 
```

Going the opposite way by saving in R and reading in Python works equally
well. An extension not present in [CNPy](https://github.com/rogersce/cnpy)
allows reading and writing of gzip-compressed files.

The package has been tested and used on several architecture, and copes
correctly with little-vs-big endian switches.

More details are available in the [package vignette](https://cran.r-project.org/web/packages/RcppCNPy/vignettes/RcppCNPy-intro.pdf).

### Status

On [CRAN](https://cran.r-project.org/package=RcppCNPy), stable and mostly
feature-complete.

### Author

Dirk Eddelbuettel and Wush Wu

### License

GPL (>= 2)
