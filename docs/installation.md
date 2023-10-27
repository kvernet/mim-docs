# Installation

Before using the library or the Python interface, a user must have it on his/her computer. In the following, we will describe how to get the source code, to compile it and use it to radiography a volcano. 

## Prerequisites

To get the source code and to use it, a user must have some software pre-installed on his/her computer. The following describes the prerequisites to be able to use the codes.

### Git

To get a cloned of the repository, a user should have git software on his/her computer. If a user does not have it installed yet on his/her computer, it can be installed from the [git page](https://git-scm.com/). Assuming git software is already installed, the package can be cloned by typing the following in a terminal:

```git
git clone https://github.com/kvernet/mim-pdd.git
cd mim-pdd
git submodule update --init
```

The last instruction allows the user to get the submodule named [mim](https://github.com/kvernet/mim) in the deps directory.

### The contents of the repository
The contents of the repository are as follows:

- src that contains the source code (.h, .c) and a python file used when compiling the library
- mim that contains the Python core interface
- examples that contains the C and Python examples
- README.md and LICENSE.txt
- Makefile and setup.sh to compile the package
- .gitignore


### Python version 3

A user that wants to use Python language to radiography a target of interest can also use the package. In that case, Python should be installed. If not yet, installation instructions can be found on the [Python web page](https://www.python.org/).

After installing Python language, make sure that a version 3 or newer is. A user couls verify the Python version that is installed on his/her computer by taping the following in a terminal:

```python
python3 --version
```
The result should be something like "Python 3.x.y". If so, the user is good to go.


### CMake

For both C and Python applications, a user must have the CMake already installed on his/her computer. Instructions to install CMake could be found on the [CMake page](https://cmake.org/). CMake version 3.xx was used to test the sofware on a Linux (debian) machine. Any newer version may work also.

## Compilation

To compile the library, a user must go to where the source code is on the computer and type the following:

```cmake
make package
```
By executing the above instruction, the library should be installed in the lib/ directory. Note that, that instruction uses the setup.sh and the files in the src/ directory to build the dynamic library named mim. It also links the h header file (mim.h) into mim/include/ and the library (libmim.so) into mim/lib/. And finally it creates the wrapped file mim/wrapper.abi3.so used in Python applications by mim/core.py.

## Examples

The C examples could be compiled and installed by executing the following instruction:

```cmake
make examples
```
They are linked to the library. Thus, by executing the above instruction, the library is created if it does not already exist. The examples binary will be installed in the bin/ directory.

The Python examples, on the other hand, can be executed directly using Python.