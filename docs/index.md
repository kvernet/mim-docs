# MIM (Muon IMaging)
MIM (**M**uon **IM**aging) is a kernel-based algorithm allowing to image the density of volcanoes using atmospheric muons. It consists essentially of two parts: A library and a Python interface. The library is developped using C language. That means, anyone can use the library in C applications or directly the Python interface. In this document, we will describe the main features of MIM.

The idea here, is not to describle the muon imaging but to describe how to use the repository to reconstruct the density distribution of a target like volcanoes. We will first of all, describe the contenu of the git repo. In a second time, we will describe how to compile, install and use the package in a C applications or the Python wrapper.

## The problem and the solution provided by MIM

In muon imaging concepts, sometimes it is necessary to have sufficient number of muons to be able to properly reconstruct/invert the density distribution of a target. Unfortunately we are dependent on what the nature provides and our detectors have limited aceptance and often we need to reconstruct the interior of the target in a short time. The solution provided by MIM algorithms is to make the most of every muon we detect while preserving the best possible spatial resolution.

Two algorithms are developped to solve the problems. The accretion algorithm allows the user to integrate the closest bins to have the minimum number of muons and the kernel algorithm allows to affect the reconstructed density to all accreted bins with different weights. These two algorithms are described in the [accretion algorithm](algorithms/accretion.md#the-accretion-algorithm) and in the [kernel algorithm](algorithms/kernel.md#the-kernel-algorithm). Note also, assuming that the number of detected muons follows a Poisson distribution then the statistical uncertainty on the reconstructed density is, in first approximation, function inverse of $\sqrt{number\, of\, muons}$. We can easily deduce that the algorithms implicitly allow to reconstruct the density of a target with a statistical uncertainty not exceeding a threshold value.


## The contents of the repository
The contents of the repository are as follows:

- src that contains the source code (.h, .c) and a python file used when compiling the library
- mim that contains the Python core interface
- examples that contains the C and Python examples
- README.md and LICENSE.txt
- Makefile and setup.sh to compile the package
- .gitignore

## An example of use of case
The library has been already used to radiography the puy de Dôme (a volcano in the Auvergne, France region) in a complete C application and the results were very promising. The git repository of that imaging can be found [there](https://github.com/kvernet/mim-pdd).