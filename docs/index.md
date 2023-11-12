# **MIM**

**MIM** (**M**uon **IM**aging) is a kernel-based algorithm allowing to image the density of volcanoes using atmospheric muons. The reconstruction of the density of a target in muon imaging involves various stages: telescope construction, calibration, data acquisition and robust algorithms for inverting the measurement into a density estimation. We define muon imaging as the algorithms for inverting the measurement of the transmitted muon through the target into its density. 

**MIM** consists essentially of two parts: A library and a Python interface. The library is developped using C language. That means, anyone can use the library in C applications or directly the Python interface. In this document, we will describe the main features of **MIM**.

The idea here, is not to describle the muon imaging concepts but how to use **MIM** to reconstruct the density distribution of a target like volcanoes. We will first of all, describe the contenu of the git repo. In a second time, we will describe how to compile, install and use the package in a C applications or the Python interface (see [examples](examples.md)).


## The problem we solve

In muon imaging, it is necessary to have sufficient number of muons to be able to properly reconstruct the density distribution of a target. Unfortunately we are dependent on what the nature provides and our detectors have limited aceptance and often we need to reconstruct the interior of the target in a short time. The solution provided by **MIM** algorithms is to make the most of every muon we detect while preserving the best possible spatial resolution. The accretion algorithm that allows to integrate the closest bins to have the minimum number of muons is described [here](algorithm.md).

Note also, assuming that the number of detected muons follows a Poisson distribution then the statistical uncertainty on the reconstructed density is, in first approximation, function inverse of $\sqrt{n}$ (with $n$, the number of detected muons). We can easily deduce that the algorithms implicitly allow to reconstruct the density of a target with a statistical uncertainty not exceeding a threshold value. The statistical uncertainty will only depend of the direction.


## The methodology

The density is reconstructed by comparing measurements and simulations for different target models (in terms of density). The density that best reproduces the data is our estimation of the target's density. In that case, as described in the [API](api.md), **MIM** takes as input different models of the target and an observation to be inverted into te target density.

Theses models could be obtained by any third-party program that allows to estimate the transmitted muon flux through a target. For example, a user could use the [mulder project](https://github.com/niess/mulder) to estimate the muon flux through a target.


## An example of use of case

**MIM** has been already used to radiography the puy de Dôme (a volcano in the Auvergne, France region) in a complete C application and the results were very promising. The git repository of that project can be found [there](https://github.com/kvernet/mim-pdd).