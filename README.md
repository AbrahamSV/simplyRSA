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
brikpath = [path to my .BRIK file]
brikdata = nib.load(brikpath).get_fdata()
```
