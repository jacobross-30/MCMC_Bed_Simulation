# MCMC_Bed_Simulation
Authors: Jake Ross, Emma (Mickey) MacKie, Niya Shao
**Overview:**

This repository contains my workflow for generating probabilistic realizations of Ninnis Glacier’s subglacial topography using a Markov Chain Monte Carlo (MCMC) framework combined with geostatistical simulation. This approach produces mass-conserving bed elevation realizations, allowing us to quantify uncertainty and explore the non-uniqueness inherent in subglacial topography. By constructing many plausible bed geometries, this method supports improved modeling of glacier dynamics, ice-sheet evolution, and sea-level contributions.

Ninnis Glacier is a fast-flowing outlet glacier on the George V Coast of East Antarctica, draining into the Southern Ocean through the broad Ninnis Glacier Tongue. The glacier has a long history of rapid advance–retreat cycles: satellite observations show multi-decadal tongue regrowth punctuated by major calving events roughly every 20–30 years. These cycles highlight the glacier’s dynamic nature and the structural vulnerability of its floating extension.

Modern geophysical work reveals that deep troughs and seafloor irregularities beneath the glacier tongue allow warm ocean water to access its cavity, promoting basal melting and influencing grounding-line stability. Geological studies also suggest that both Ninnis and its neighbor, Mertz Glacier, may overlie ancient impact crater structures—long-term controls that have helped guide ice flow and shape present-day glacier morphology.

Together, these oceanic, geological, and dynamic factors make Ninnis an excellent testbed for understanding how local bed conditions influence outlet-glacier behavior in East Antarctica.

We additionally compare our generated bed realizations with existing large-scale products, including Bedmap and BedMachine, to evaluate consistency, differences, and potential improvements in localized bed estimates for the Ninnis region.


<img width="1051" height="552" alt="figures for github" src="https://github.com/user-attachments/assets/32e45893-04db-4a56-a776-f10e15f0278a" />


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
- matplotlib
- pandas
- xarray
- verde
- geopandas
- gstatsim
- Topography
- MCMC
- sklearn
- skstat

**Environment**

We recommend creating a conda (or R) environment with the necessary packages.
For example
- conda env create -f environment.yml
- conda activate gstatsMCMC
- jupyter lab

**Software:**

- Python 3.10.9
- https://github.com/NiyaShao/geostatisticalMCMC

**File Descriptions**

T1_LoadData_update.ipynb

- Used to load all the required data files and crop the study area to look at the high velocity region
- Outputs:

  - Cropped study-area grids (surface, SMB, velocity, mask).
  - Preview figures of the high-velocity region.
  - Saved NumPy/NetCDF arrays used by later steps.

Lab2_IceFluxaDivergence.ipynb

- Used to determine the mass flux residual of the study area.
- Outputs:
  
  - Mass flux divergence residual map.
  - Diagnostic plots of flux difference.
  - Residual arrays saved for later loss calculations.
  
Lab3_Geostatistics_2.ipynb

- Normalizes the data so we cand create a geostatistical realization.
- Creates a variogram and compares it to the Bedmachine variogram.
- Generates an SGS realization.
- Outputs:

  - Normalized bed and geostatistical inputs.
  - Variogram plots and BedMachine comparison.
  - An SGS bed realization.

T2_StatisticalAnalysis_update.ipynb

- Used to generate an SGS bed (use this one to initiate the MCMC large scale chain)
- Outputs:

  - The SGS bed used to initialize the large-scale MCMC chain.
  - Statistical summaries of variogram structure and SGS behavior.

T3_LargeScaleChain_3.ipynb

- The large scale chain guesses possible bed topographies and accepts or rejects the guess
- run for however many iterations it takes for the loss curve to flatten out
-Outputs:

  - Full MCMC chain of accepted beds.
  - Loss curve vs. iteration (to assess convergence).
  - Intermediate diagnostic plots and arrays.
  -Final accepted bed used to start the small-scale chain.

T4_SmallScaleChain_3.ipynb

- The small scale chain takes the last bed from the large scale chain and finely tunes it.
- run this until the small scale chain levels off.
- the final loss should be around or lower than the loss of bedmachine
- Outputs:

  - Fine-tuned bed solution starting from the large-scale chain’s final bed.
  - A second loss curve showing refinement behavior.
  - Final optimized bed realization (should approach or beat BedMachine loss).

MCMC.py

- Contains the full implementation of the Markov Chain Monte Carlo (MCMC) algorithm used to explore possible bed topographies.
- Proposes perturbations to the current bed, evaluates the mass-conservation loss, and accepts or rejects each proposal based on the likelihood function.
- Tracks chain diagnostics (loss history, accepted states, iteration count) and outputs the accepted bed realizations used in the large-scale and small-scale chains.

Topography.py

- Defines functions for handling, modifying, and evaluating bed topography grids.
- Computes spatially correlated perturbations, applies smoothing or tapering as needed, and prepares bed updates for the MCMC sampler.
- Includes utilities for loading existing bed datasets (e.g., BedMachine), computing gradients/slopes, and generating topographic fields used during both initialization and the proposal steps within the MCMC workflow.

**Usage Instructions**

1. Clone the repository
2. Prepare the data
   
  Place all required datasets into a data directory:

4. Run the preprocessing notebooks

- T1_LoadData_update.ipynb – loads and crops data
- Lab2_IceFluxDivergence.ipynb – computes mass flux residual
- Lab3_Geostatistics_2.ipynb – builds variogram and generates SGS realization
- T2_StatisticalAnalysis_update.ipynb – produces the initial SGS bed for MCMC
These steps prepare all inputs for the MCMC inversion.

5. Run the MCMC inversion in T3 and T4
  
