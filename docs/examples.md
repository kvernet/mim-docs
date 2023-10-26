# Simple projects

In the following, we provide some simple codes to help the user in using the MIM API. The directory examples/ contains other examples and may be used.


## MIM image

```c
/* Public API */
#include "mim.h"
/* C standard library */
#include <stdio.h>

int main(void) {
	/* Image dimension */
	const size_t width = 3;
	const size_t height = 2;
	
	/* Create a zeroed image */
	struct mim_img *zeros = mim_img_zeros(width, height);
	
	/* Access each pixel of the zeroed image */
	size_t i, j;
	for(i = 0; i < width; i++) {
		for(j = 0; j < height; j++) {
			const double zv = zeros->get(zeros, i, j);
			
			printf("zeros(%ld, %ld) = %g\n", i, j, zv);
		}
	}
	
	/* Free allocated memory */
	zeros->destroy(&zeros);
	
	return 0;
}

```


## MIM model

```c
const size_t width = 6;
	const size_t height = 4;
	const size_t size = 7;
	
	/* Model parameters */
	double parameter[size];
	struct mim_img *images[size];
	
	const double pmin = 1.0;
	const double pmax = 2.8;
	const double pdl = (pmax - pmin) / (size - 1);
	
	/* Model of images */	
	size_t i, j, k;
	for(k = 0; k < size; k++) {
		parameter[k] = 1.0 + k * pdl;
		images[k] = mim_img_empty(width, height);
	}
	/* Observation */
	struct mim_img *observation = mim_img_empty(width, height);
	
	/* Fill with abstract data */
	for(i = 0; i < width; i++) {
		for(j = 0; j < height; j++) {			
			double value;
			for(k = 0; k < size; k++) {
				value = get_count(parameter[k]);
				images[k]->set(images[k], i, j, value);
			}
			
			const double rdensity1 = parameter[rand() % size];
			const double rdensity2 = parameter[rand() % size];
			
			value = get_count(0.5 * (rdensity1 + rdensity2));
			observation->set(observation, i, j, value);
		}
	}	
	struct mim_model *model = mim_model_create(
			size, parameter, images);
	
	/* Inverted result */
	struct mim_img *result = mim_img_empty(width, height);

```