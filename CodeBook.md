# Code Book : Getting and Cleaning Data Course Project

This file describes the data used in the Getting and Cleaning Data Course Project; the data's source and the transformations applied to the data in order to get the final output as required by the project.

## Data source

A description of the data and its original source is available at this website:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

The actual data used for the project is this:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

Apart from the data itself, the linked ZIP file contains a detailed description of the data and the variables. The following files are of interest:

- 'UCI HAR Dataset/features_info.txt': Shows information about the variables used on the feature vector.

- 'UCI HAR Dataset/features.txt': List of all features. Same for both the test and train data sets.

- 'UCI HAR Dataset/activity_labels.txt': Links the class labels with their activity name. Same for both the test and train data sets.

- 'UCI HAR Dataset/train/X_train.txt': Training set.

- 'UCI HAR Dataset/train/y_train.txt': Training labels.

- 'UCI HAR Dataset/train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 

- 'UCI HAR Dataset/test/X_test.txt': Test set.

- 'UCI HAR Dataset/test/y_test.txt': Test labels.

- 'UCI HAR Dataset/test/subject_test.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 


## Data Transformations

All of the transformations applied to the data sets are performed inside a single function **"meanMeasurements()"** contained inside the source file *"run_analysis.R"*. Note: the function relies on the **'dplyr'** and **'tidyr'** R packages.

The following is a description of the flow and transformations performed inside the function with references to the course project objectives:

- **Assignment task 1: Merge the test and train data sets**

1. Loads the features names, i.e. the *'UCI HAR Dataset/features.txt'* file. These will be later used as the variable/column names when reading in the test and train data sets. Note: when the features names are later used as column names, some characters within the names will be replaced with dots due to those characters not being acceptable in column names, e.g. "-","(",")". For example, *'tBodyAcc-max()-X'* will become *'tBodyAcc.max...X'*.
2. Loads the subject list for the test data set, i.e. the *'UCI HAR Dataset/test/subject_test.txt'* file.
3. Loads the activities for the test data set, i.e. the *'UCI HAR Dataset/test/y_test.txt'* file.
4. Loads the test data set, i.e. the *'UCI HAR Dataset/test/X_test.txt'* file and specifies the feature names set as the column names.
5. Merges the subject, activities and test data set into one data frame named **df_test**.
6. Loads the subject list for the train data set, i.e. the *'UCI HAR Dataset/train/subject_train.txt'* file.
7. Loads the activities for the train data set, i.e. the *'UCI HAR Dataset/train/y_train.txt'* file.
8. Loads the train data set, i.e. the *'UCI HAR Dataset/train/X_train.txt'* file and specifies the feature names set as the column names.
9. Merges the subject, activities and train data set into one data frame named **df_train**.
10. Merges the **df_test** and **df_train** data frames by combining their rows into one data frame named **df_merged**.

- **Assignment task 2: Extract only "mean" and "std" variables**

11. Extracts the *'subject'*, *'activity'* together with all *'mean'* and *'std'* variables and puts the result back into the **df_merged** data frame.

- **Assignment task 3: Use descriptive names for activities**

12. Loads the activity names, i.e. the *'UCI HAR Dataset/activity_labels.txt'* file.
13. Replaces all activities in the **df_merged** data frame with their respective names.

- **Assignment task 4: Set appropritate names for the variables**

14. Converts all variable names to lower case, e.g. *'tBodyAcc.max...X'* will become *'tbodyacc.max...x'*.
15. Replaces double dots in the variable names with an empty string, e.g. *'tbodyacc.max...x'* will become *'tbodyacc.max.x'*.
16. Replaces a leading *'t'* or *'f'* with a *'t.'* or *'f.*' respecitvely, e.g. *'tbodyacc.max.x'* will become *'t.bodyacc.max.x'*.

- **Assignment task 5.1: Calculate means per subject and activity**

17. Groups the **df_merged** data frame by *'subject'* and *'activity'*.
18. Calculates the mean of each variable/column with the exception of the *'subject'* and *'activity'* variables.

- **Assignment task 5.2: Create a tidy data set for the output**

19. Turns all variables/columns/measurements with the exception of *'subject'* and *'activity'* into rows by "gathering" the variables and places the result into the **df_tidy** data frame.
20. Splits the newly created variable/column in step 1 into 4 separate variables/columns with the separator being the dot, e.g. the one column containing *'tbodyacc.max.x'* will become 4 separate columns containing *'t'*, *'bodyacc'*, *'max'* and *'x'* respectively.
21. Sorts the resulting data frame.
22. Saves the resulting data frame as a CSV file.
23. Returns the resulting data frame as the function's return value.

## Resulting tidy data set variable description

The final tidy data set variables are as follows:

1. **subject** : int - subject/person that the measurement was taken for.
2. **activity** : chr - description of activity that the subject was performing when measurement was taken.
3. **domain** : chr - either *'t'* for *'time'* domain or *'f'* for *'frequency'* domain.
4. **feature** : chr - name of measurement.
5. **measure.type** : chr - type of measurement - either *'mean'* for *'mean value'* or *'std'* for *'standard deviation'*.
6. **axis** : chr - axis that the measurement is for, i.e. *'x'*, *'y'*, *'z'*. Note: for some measurements the axis is not applicable. These measurements will have *'NA'* as their *'axis'* value.
7. **value** : num - the normalised measurement value.

