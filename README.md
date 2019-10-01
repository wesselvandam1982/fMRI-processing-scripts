# fMRI_processing_scripts
scripts for analyzing fMRI data in AFNI

In this repository you'll find a set of shell scripts that will be helpful in processing functional MRI data.
For example, it includes an AWK script that goes through an output file created by for example Presentation or E-prime 
and extracts the onset times for each subject and condition and stores it in the correct format to be processed during subsequent first and second level processing steps. 

In addition it includes scripts for: creating masks, extracting mask statistics, general preprocessing, making tables based on contrast files, applying cluster thresholding, calculating ACF-values and running second level group statistics. 
