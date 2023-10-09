# RIT-DEC_SVI_Project
RIT-DEC SVI Project: Partner Code README  
README Date: 10/9/2023  

## Metadata
Data type: Python notebooks and a .txt file with bash code  
Script author: Liam Megraw  
Datasets needed to run code:  
- Model data in one to three forms:
  - Raw CSVs: used in model_result_processing_batch to import and threshold predicted presence points and lines
  - Imported, unthresholded panorama points: used in the gap analysis for thresholdless sums/ratios and to remove cells with no model data
  - Thresholded predictions: used in the gap analysis for thresholded sums and ratios
- iMapInvasives data for species of interest: used in the gap analysis to compare with model-predicted values and in priority grid cell creation to remove cells with all target species already found
  - Default data configuration: Confirmed, unconfirmed, and not detected records for Common reed grass, Japanese knotweed, Bohemian knotweed, Giant knotweed, Knotweed (species unknown), Wild Parsnip, Purple loosestrife, and Tree-of-heaven (spelling mirrors iMap spelling).
- NYNHP Comprehensive Spatial Prioritization: used to identify high-priority grid cells
- NY Department of Environmental Conservation Potential Environmental Justice Areas - 2022 release: used to identify high-priority grid cells
- NYNHP Partnership for Regional Invasive Species Management (PRISM) Boundaries - 2016 release: used in the high-priority grid cell analysis to assess per-PRISM comprehensive score percentile
- US Census TIGER/Line Shapefiles All Roads (per-county shapefiles): used when creating not-detected lines
- US Geological Survey National Hydrography Dataset for NYS: used in the reporting analysis and for high-priority grid cells to remove cells completely within water

## Description
This package contains code from and applied to a computer vision model designed by Rochester Institute of Technology and University California San Diego researchers (Flores et al., in prep.). The model was applied to identify five target invasive plants along roadside imagery. Broadly, computer vision (CV) is a discipline focused on enabling computers to perform image recognition (Huang, 1996), where artificial intelligence is one of the more recent methods to carry out these tasks which we utilized here. Each point represents an individual 360-degree panorama that the computer vision model has “viewed” and assigned a confidence score. In general, as higher thresholds are chosen, fewer plant presences are detected; the model is less “sensitive.” The "precision" scenario separated here is the least sensitive, but also the least prone to false positives. More information on thresholds can be viewed below.

### Example of descriptive entries:
- Item 1: Description of item
- Item 2: Description of item

### Files:
- reporting_analysis.ipynb: Creates the reporting analysis grid with join counts and ratios
- model_prediction_priority.ipynb: Assigns priority levels 1-4 to thresholded CV model predictions (run before reporting_analysis)
- model_result_processing_batch.ipynb: Thresholds CV model results and creates not-detected lines (run before model_prediction_priority)
- priority_grid_cells.ipynb: Creates the high priority grid (run before model_prediction_priority)

## Performance Criteria

Performance criteria at various confidence score threshold options for model target species. True positive rate (TPR) and false discovery rate (FDR) for each option is displayed. The true positive rate (TPR) refers to the proportion of all panoramas with plant presences correctly detected as a presence by the model. The false discovery rate (FDR) can be interpreted as the proportion of panoramas the model classified as presences but are actually absences. Each species has a test set with a different number of records. (\*) F1, Recall, and Precision values are the maximum unweighted mean of three test sets, which do not have identical numbers of records. (^) Thresholds could have been set higher and/or lower, but precision drops precipitously for only minor gain in recall and vice versa. (+) These numbers are based on much smaller test sets than those of Phragmites and Knotweed Complex. 

Model Target Species,Criteria Prioritized,Threshold,TPR,FDR,Note  
Common Reed,Recall,0.07,0.96,0.32,\*^  
Common Reed,F1,0.33,0.88,0.17,\*  
Common Reed,Precision,0.9,0.5,0.06,\*  
Knotweed Complex,Recall,0.03,0.95,0.39,\*^  
Knotweed Complex,F1,0.29,0.83,0.13,\*  
Knotweed Complex,Precision,0.8,0.66,0.01,\*^  
Wild Parsnip,Recall,0.25,0.88,0.56,+  
Wild Parsnip,F1,0.49,0.78,0.39,+  
Wild Parsnip,Precision,0.8,0.59,0.24,+  
Tree-of-Heaven,Recall,0.09,0.85,0.53,+  
Tree-of-Heaven,F1,0.63,0.66,0.1,+  
Tree-of-Heaven,Precision,0.9,0.4,0.04,+  
Purple Loosestrife,Recall,0.05,0.88,0.62,+  
Purple Loosestrife,F1,0.44,0.75,0.35,+  
Purple Loosestrife,Precision,0.93,0.39,0.3,+  

## References
Flores, A., Acharya, M., Megraw, L., Miller, A., Cwitkowitz F., Sharma, D., Wilkinson, M, Belongie, S., Tyler, A. C., and Kanan, C. (in prep.). Large-scale invasive species detection and monitoring using deep learning. 
Huang, T. S. (1996). Computer vision: Evolution and promise (C. Vandoni, Ed.). CERN. https://doi.org/10.5170%2FCERN-1996-008.21
