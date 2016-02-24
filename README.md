lcms_processing
===============

This is the initial readme file for the lcms_processing repository. 

This contains a processing script (lcms_procesing.R), in which you set your working directory, library directory and some parameters, 
and the main processing script(lcms.R) which you should not need to modify (unless you want to!).

First convert your .raw files to .mzML format using MSConvert (Proteowizard)

Place these files in a working directory in your C:/ drive (should be faster than H:/ drive). 

The mzML files are in your "spectra_dir" which you need to specify (see below). 

Note - there should be NO subfolders in your spectra folder, particularly if they hold other mzML files!

Then save both R scripts and the library files to anywhere on your computer.

Place the library files in a folder named "libraries". This is your "lib_dir" which you need to specify (see below).

Set some parameters: see below for example.

Check the main script (lcms.R) is sourced from the correct directory where you saved it. 

NOTE: 

For Waters data files - use the Waters software "Databridge" to covert to .CDF files. You should get multiple files for each sample - chose the largest in size for each and place in new folder.
Use the lcms_CDF.R and lcms_processing.CDF.R scripts! 

 ``` 

########### Script to process lcms data using xcms ########################################################################

###### Z.Hall, Aug 2014 ##################################################################################################


spectra_dir <- "C:/Users/hallz/Documents/Processing_temp/Frank/withoutblanks" # where your mzML files are stored


lib_dir <- "H:/Git/lcms_processing/libraries"      # the folder where your library files are stored


FWHM <- 3 # full width at half maximum - look at a representative chromatogram and estimate FWHM in seconds. 3 sec seems to work well for 5 min Velos LC method. 


snthresh = 5 # set the signal to noise threshold below which peaks are ignored


minfrac = 0.25 # minimum fraction of samples necessary for it to be a valid peak group 


adducts = c(H = T, NH4 = T, Na = T, K = F, dH = F, Cl = F, OAc = F) # choose which adducts you want to include in your library search


ppm.annotate = 10   # choose ppm tolerance for ID/annotations


ionisation_mode <- "positive"  # either "positive" or "negative" - determines which classes of lipids to search for - remember to adjust the adducts if using negative mode


source("H:/R/lcms.R") # source your R script from correct directory


####################################################################################################################################


```


Additional Notes:

*** Exclude blanks from the analysis if you want the retention time correction algorithm to work properly ***

File numbering: preferable to number with extension _001, _002 etc (> 100 files) or _01, _02 etc (1-99 files) as will order correctly

Output: You will get several output csv files, including filtered/raw peak area/height. 

Deisotoping and annotations are carried out on raw peak area. 

First three columns are mz, annotations and RT. The mz/RT group is unique. 

Currently set to choose only peaks that occur in 25% or greater of samples - can be adjusted using minfrac 



Advanced users:

May need to adjust "missing" and "extra" in retention correction stage (retcor) depending on data quality or use obiwarp retention time correction method

Missing - number of missing samples to allow in retention time correction groups

Extra -  number of extra peaks to allow in retention time correction groups






