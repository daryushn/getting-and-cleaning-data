# Getting And Cleaning Data - Course Project

This repository contains the files submitted as part of the final assignment of the Coursera "Getting And Cleaning Data" course.

List of files contained in this repository:

1. **README.md** - this file.
2. **CodeBook.md** - file containing a detailed description of the data and the transformations performed on it for the purposes of the course.
3. **run_analysis.R** - the R script containing a single function **meanMeasurements()** that performs all tasks required for the purposes of this course.

In order to run the **meanMeasurements()** function:

1. Ensure you have the **dplyr** and **tidyr** R packages installed.
2. Download and unzip the data sets as per the **CodeBook.md** file.
3. Place the **run_analysis.R** file in the same directory as the *'UCI HAR Dataset'* directory.
4. Set the working directory to the directory containing the **run_analysis.R** file.
5. Load the **run_analysis.R** file.
6. Call the **meanMeasurements()** function.
7. The output tidy data set will be saved as a CSV file in the working directory and will have the name **tidy.csv**.


