# **MIM**

**MIM** (**M**uon **IM**aging) is a kernel-based algorithm allowing to image the density of volcanoes using atmospheric muons. The reconstruction of the density of a target in muon imaging involves various stages : telescope construction, calibration, data acquisition and robust algorithms for inverting the measurement into a density estimation. Here, we define muon imaging as the algorithms for inverting the measurement of the transmitted muon through the target into its density. 

**MIM** consists essentially of two parts : A library and a Python interface. The library is developped using C language. That means, anyone can use the library in C applications or directly the Python interface. In this document, we will describe the main features of **MIM**.

The idea here, is not to describle the muon imaging concepts but how to use **MIM** to reconstruct the density distribution of a target like volcanoes. The user could refer to the [**MIM** publication]() for muon imaging concepts. We will first of all, describe the problem we solve in muon imaging and the method. In a second time, we will describe how to [install](installation.md) and use the package in a C applications or the Python interface (see [examples](examples.md)).


## The problem we solve

In muon imaging, it is necessary to detect sufficient number of muons to be able to reconstruct precisely the density distribution of a target. Unfortunately we are dependent on what the nature provides and our detectors have limited acceptance. Reconstruct the density of a target in a short time needs robust algorithm. The solution provided by **MIM** is to make the most of every muon we detect while preserving the best possible spatial resolution. The [algorithm](algorithm.md) consists first of all, of accreting the closest bins to have the minimum number of muons and then reconstruct the spatial resolution by appliying a weight to each bins.

Note also, assuming that the number of detected muons follows a Poisson distribution then the statistical uncertainty on the reconstructed density is, in first approximation, function inverse of $\sqrt{n}$ (with $n$, the number of detected muons). We can easily deduce that the algorithm implicitly allows to reconstruct the density of a target with a statistical uncertainty not exceeding a threshold value. The statistical uncertainty will only depend on the direction.


## The methodology

To reconstruct the density of a target we compare simulations for different models of the target (in terms of density) to the measurements. The density that best reproduces the data is our estimation of the target's density. In that case, as described in the [API](api.md), **MIM** takes as input different models of the target and an observation to be inverted into te target density.

Theses models could be obtained by any third-party program that allows to estimate the transmitted muon flux through a target. For example, a user could use the [mulder project](https://github.com/niess/mulder) to estimate the muon flux through a target.


## An example of use of case

**MIM** has been already used to radiography the puy de Dôme (a volcano in the Auvergne, France region) in a complete [C application](https://github.com/kvernet/mim-pdd). The same results have been obtained using the [Python interface](https://github.com/kvernet/mim-pdd-python). The results were very promising.