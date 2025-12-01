# MCMC_Bed_Simulation
Authors: Jake Ross, Emma (Mickey) MacKie, Niya Shao
**Overview:**

This repository contains my workflow for generating probabilistic realizations of Ninnis Glacier’s subglacial topography using a Markov Chain Monte Carlo (MCMC) framework combined with geostatistical simulation. This approach produces mass-conserving bed elevation realizations, allowing us to quantify uncertainty and explore the non-uniqueness inherent in subglacial topography. By constructing many plausible bed geometries, this method supports improved modeling of glacier dynamics, ice-sheet evolution, and sea-level contributions.

Ninnis Glacier is a fast-flowing outlet glacier on the George V Coast of East Antarctica, draining into the Southern Ocean through the broad Ninnis Glacier Tongue. The glacier has a long history of rapid advance–retreat cycles: satellite observations show multi-decadal tongue regrowth punctuated by major calving events roughly every 20–30 years. These cycles highlight the glacier’s dynamic nature and the structural vulnerability of its floating extension.

Modern geophysical work reveals that deep troughs and seafloor irregularities beneath the glacier tongue allow warm ocean water to access its cavity, promoting basal melting and influencing grounding-line stability. Geological studies also suggest that both Ninnis and its neighbor, Mertz Glacier, may overlie ancient impact crater structures—long-term controls that have helped guide ice flow and shape present-day glacier morphology. Together, these oceanic, geological, and dynamic factors make Ninnis an excellent testbed for understanding how local bed conditions influence outlet-glacier behavior in East Antarctica.

We additionally compare our generated bed realizations with existing large-scale products, including Bedmap and BedMachine, to evaluate consistency, differences, and potential improvements in localized bed estimates for the Ninnis region.


![github figures 2](https://github.com/user-attachments/assets/e2efbc46-deab-4a72-abf6-c0c6b1982802)

**Data:**

- Bedmap3:

  Pritchard, H.D., Fretwell, P.T., Fremand, A.C. et al. Bedmap3 updated ice bed, surface and thickness gridded datasets for Antarctica. Sci Data 12, 414 (2025). https://doi.org/10.1038/s41597-025-04672-y. Date Accessed 11-18-2025.
- BedMachine Antarctica v3:

  Morlighem, M. (2022). MEaSUREs BedMachine Antarctica. (NSIDC-0756, Version 3). [Data Set]. Boulder, Colorado USA. NASA National Snow and Ice Data Center     Distributed Active Archive Center. https://doi.org/10.5067/FPSU0V1MWUB6. Date Accessed 11-18-2025.
- MOA2014:

  Haran, T., Klinger, M., Bohlander, J., Fahnestock, M., Painter, T. & Scambos, T. (2018). MEaSUREs MODIS Mosaic of Antarctica 2013-2014 (MOA2014) Image Map. (NSIDC-0730, Version 1). [Data Set]. Boulder, Colorado USA. NASA National Snow and Ice Data Center Distributed Active Archive Center. https://doi.org/10.5067/RNF17BP824UM. Date Accessed 11-18-2025.

- Ice Surface Velocity:

  Mouginot, J., Rignot, E. & Scheuchl, B. (2019). MEaSUREs Phase-Based Antarctica Ice Velocity Map. (NSIDC-0754, Version 1). [Data Set]. Boulder, Colorado USA. NASA National Snow and Ice Data Center Distributed Active Archive Center. https://doi.org/10.5067/PZ3NJ5RXRH10. Date Accessed 11-18-2025.

- Grounding Line:

  Rignot, E., Mouginot, J. & Scheuchl, B. (2023). MEaSUREs Grounding Zone of the Antarctic Ice Sheet. (NSIDC-0778, Version 1). [Data Set]. Boulder, Colorado USA. NASA National Snow and Ice Data Center Distributed Active Archive Center. https://doi.org/10.5067/HGLT8XB480E4. Date Accessed 11-18-2025.

- Van Wessem, J. M., Van de Berg, W. J., and Van den Broeke, M. R.: Data set: Monthly averaged RACMO2.3p2 variables (1979–2022), Antarctica, Zenodo [data set], https://doi.org/10.5281/zenodo.7845736 Date Accessed 11-18-2025

**Python Packages**

- numpy
- scipy
- matplotlib
- pandas
- xarray
- netCDF4
- scikit-learn
- pyproj
- cartopy
- tqdm

**Environment**

We recommend creating a conda (or R) environment with the necessary packages.
For example
- conda env create -f environment.yml
- conda activate gstatsMCMC
- jupyter lab

**Software:**

- Python 3.10.9
- https://github.com/NiyaShao/geostatisticalMCMC
  
