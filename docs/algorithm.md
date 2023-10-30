# The accretion algorithm

To have sufficient muons to reconstruct a given direction we integrate the closest bins until we get that minimum number of muons (see figure)

![image](img/accretion-algo.png)

The density is reconstructed for the entire (accreted) bins and is affected to each bin with differents weights. Then a new bin is investigated. If a single bin contains enough muons then it is reconstructed alone otherwise the acrretion is applied. At the end of the process, each bin may have multiple entries affected with different weights. These weights come from different accreted bins centered at bins close to the main bin. These weights should take into account the distance between the main bin with respect to the others.

An estimation of the density in each direction (bin) is then obtained by weighted average of the contributions of that bin as follows.

$\hat{\rho} = \frac{ \sum_{i=1}^n w_i \times \rho_i }{ \sum_{i=1}^n w_i }$

The weight $w_i$ is chosen as it decreases with the distancce from the main bin to the bin $i$. A Gaussian centered to the main bin could be used to model these weights.