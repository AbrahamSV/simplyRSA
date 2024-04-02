# simplyRSA
Simple package to run RSA analyses on fMRI data
Currently, it only contains 1 module for RSA searhclight.
Some features are missing, like cross-run validation

### Setup

__Before installation__

The package uses the following dependencies:

pandas, numpy, nibabel, scipy, joblib, tqdm, collections

If you don't have them installed, simply run:

```pip install pandas numpy nibabel scipy joblib tqdm collections```

__Installation__

1. Download the package
2. Go to the directory in which it was downloaded
3. Run ```pip install [package_file_name]```

### Usage

Here is a simple example on how to use the _searchlight_ module:

__Imports__
```
import pandas as pd, numpy as np
import nibabel as nib
from simplyRSA.searchligh import *
```

1. Read your functional images and create a brain mask
Here, I'm reading a .BRIK file from AFNI, but you can read other files (like Nifti).

```
brikpath = [path to my .BRIK file]  # Define image path
brikdata = nib.load(brikpath).get_fdata()  # Read and extract the data from the image
```
My .BRIK file is a 4d image, with volumes (or trials) as the last dimension

So I isolate 1 volume, and create a binary brain mask, with _True_ where there is a value in the image,
and _False_ where there is no value (i.e. 0) 

```
onevol = brikdata[...,0]  # Isolate 1 volume
mask = onevol!=0  # Binary mask
```
2. Create all possible spheres within the mask

We need 2 important values: _voxel size_ (you can check that on your image header), and _sphere radius_
My voxel size is 2x2x2, and I want 5mm radius spheres 

```
sphere_radius = 5  # Adjust the radius as needed
voxel_size_mm = 2  # Adjust the voxel size if it's different
```
Then we call the first function, which is _searchlight_spheres_parallel_ as it follows: 

```
spheres_info = searchlight_spheres_parallel(mask, sphere_radius, voxel_size_mm, jobs=24)
```

The _jobs_ argument specifies how many CPUs are used in parallel for this (hence the name)

If you are unsure of how many CPUs your PC has, by providing _-1_ you tell the function to use ALL. 
It defaults to 5, which is a number most PCs will have. 
