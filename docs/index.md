# MIM (Muon IMaging)
MIM (for Muon IMaging) is a kernel-based algorithm allowing to image the density of volcanoes using atmospheric muons. The library is developped using C language and contains a Python interface. That means, anyone can use the library in C applications or directly the Python interface. In this document, we will describe the main features of the repository.

The idea here, is not to describle the muon imaging but to describe how to use the repository to reconstruct the density distribution of a target like volcanoes. We will first of all, describe the contenu of the git repo. In a second time, we will describe how to compile, install and use the package in a C applications or the Python wrapper.

## The contents of the repository
The repository contains three directories:
- src that contains the source code (.h, .c) and a python file used when compiling the library
- mim that contains the Python core interface
- examples that contains the C and Python examples
- README.md and LICENSE.txt
- Makefile and setup.sh to compile the package
- .gitignore

## An example of use of case
The library has been already used to radiography the puy de Dôme (a volcano in the Auvergne, France region) in a complete C application and the results were very promising. The git repository of that imaging can be found [there](https://github.com/kvernet/mim-pdd).