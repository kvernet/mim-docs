# MIM API

## The image interface
```c
struct mim_img {
    const size_t width;
    const size_t height;
    
    mim_img_get_t *get;
    mim_img_set_t *set;
    mim_img_ref_t *ref;
    
    mim_img_destroy *destroy;
};
```

The **mim_img** struct represents any 2D image defined by its dimensions: **width** and **height** and the following functions:

```c
double get(const struct mim_img *self,
        const size_t i, const size_t j
);
```
to get a **mim_img** value at index (i, j) ;

```c
void set(struct mim_img *self,
        const size_t i, const size_t j, const double value
);
```
to set/modify/update a **mim_img** at index (i, j) with a given value **value** ;

```c
double *ref(struct mim_img *self,
        const size_t i, const size_t j
);
```
to get the reference of a **mim_img** at index (i, j) ;

```c
void destroy(struct mim_img **self_ptr);
```
to destroy/free a **mim_img**.

### Create a mim_img

Two main functions are defined to create a **mim_img** as follows:

```c
struct mim_img *mim_img_empty(const size_t width, const size_t height);
```
allows the user to create an empty **mim_img**. The values of a **mim_img** created by that function are uninitialiazed. It is the user's responsability to set the values of the created **mim_img** by calling either the **set** or **ref** functions defined above.

```c
struct mim_img *mim_img_zeros(const size_t width, const size_t height);
```
allows the user to create a zeroed **mim_img**. That means all the values are initialiazed with zero.


## The model interface

A model is a representation of a collection of images. Each image in a model is characterized by a unique parameter. The structure of a model is defined as follows:

```c
struct mim_model {
    const size_t width;
    const size_t height;
    const double pmin;
    const double pmax;
    
    mim_model_destroy_t *destroy;
};
```
where:

- **width** is the width of all the images
- **height** is the height of all the images
- **pmin** and **pmax** are respectively the min and max value of the parameter that describes the model.

The function **destroy** allows the user to destroy/free the allocated memory for the model.


### Create a model

To create a model from a parametric collection of images, a user could use the following function :

```c
struct mim_model *mim_model_create(const size_t size,
        const double parameter[],
        struct mim_img *images[]
);
```
where

- **size** is the model size parameter
- **parameter** is the array containing the model parameters
- **images** are the collection of images



### Get a snapshot of the model
A snapshot of the model is an image at a given parameter. It could be obtained by calling the following function on a model:

```c
enum mim_return mim_model_get(struct mim_img *image,
        const struct mim_model *model,
        double parameter
);
```
Note that, the snapshot is obtained by interpolation. The first argument of the function is the return value. The function simply fills the returned image so the user should create it first before calling that function either by using **mim_img_empty** or **mim_img_zeros** as described [here](#create-a-mim_img).

The function returns a C enum: **MIM_SUCCESS** if the function was able to get correctly the snapshot or **MIM_FAILURE** otherwise.


### Invert an image from the model

Inverting an image from a model means getting the best parameter values that correspond to that image from that model. It can be obtained by calling the following function :

```c
enum mim_return mim_model_invert(struct mim_img *image,
        const struct mim_model *model,
        const struct mim_img *observation,
        const struct mim_img *filter
);
```
where:

- **image** is the image returned value
- **model** is the model
- **observation** is the image to be inverted
- **filter** is an optional image argument allowing to filter some indexes

To filter no index, the user should set the **filter** parameter to the **null** pointer.

The function returns **MIM_SUCCESS** or **MIM_FAILURE** if the inverting goes well or not.


### Inverting for a minimum value

In muon imaging concepts, sometimes it is necessary to have sufficient number of muons to be able to properly reconstruct/invert the density distribution of a target. Unfortunately we are dependent on what the nature provides and therefore we need to make the most of every muon we detect. In the MIM package, two algorithms are developped to solve the problems. The accretion algorithm that allows to integrate the closest bins to have the minimum number of muons is described [here](algorithm.md).

The following function allows the user to invert an observation from a model with a minimum value.

```c
enum mim_return mim_model_min_invert(struct mim_img *image,
        struct mim_img *bin_image,
        struct mim_img *value_image,
        const struct mim_model *model,
        const struct mim_img *observation,
        const struct mim_img *filter,
        const double min_value,
        const double sigma
);
```
where:

- **image** is the image parameter returned value
- **bin_image** is the image of the number of integrated bins returned value
- **value_image** is the image integrated bins returned value
- **model** is the model
- **observation** is the observation (the image to be inverted)
- **filter** is an optional image allow to filter indexes
- **min_value** the minimum value to be inverted
- **sigma** the Gaussian sigma parameter for kernel inversion

The function returns **MIM_SUCCESS** or **MIM_FAILURE** if the inverting goes well or not.