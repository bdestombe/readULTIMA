# readULTIMA
Reading measurement data of the ULTIMA DTS device, by Silixa

@author: Bas des Tombe, bdestombe@gmail.com

To process files generated by the ULTIMA, by Silixa. Supports both the old (when Windows xp was installed) and the new format (windows 7)!

Reads all the xml files from the specified folder. The data is merged into a
single netCDF file. That data usually contains:
LAF: length along fiber
ST: Stokes intensity
AST: anti-Stokes intensity
REV-ST: reverse Stokes intensity
REV-AST: reverse anti-Stokes intensity
TMP: By the device calibrated temperature

The meta-data from the first (alphabetically chosen) xml
file is added to the netCDF file, containing information on the method of
calibration some discretizations. Good practice to keep it all together

This should be considered step 1 of data processsing. This netCDF-file can be
used to create an actual dataset, including coordinates complying with
netCDF conventions CF. <cfconventions.org/cf-conventions/cf-conventions.html>

Vertical temperature profiles can use 'timeSeriesProfile', chp 5.2 of
cfconventions. Having a single spatial coordinate and a height above surface
attribute, one file per section.

Steps for further processing / archiving:
- data was recorded for the entire cable. split this netCDF file into sections
    when needed
- Add meta data according to CF conventions per splitter NETCDF file. 


# Usage
This script makes use of the beautiful xarray package (<xarray.pydata.org>).

1. Fill in the "User input" section, halfway the script.
2. A netCDF file is stored for further processing
3. Or plot directly, using xarray:
```python
# Read the same netCDF file
ds_disk = xr.open_dataset(os.path.join(path_nc, fn_nc))


# plot
import matplotlib.pyplot as plt
plt.imshow(ds['TMP']._variable._data.T[1500:], vmin=3, vmax=20)
```
More plotting examples on the xarray website
