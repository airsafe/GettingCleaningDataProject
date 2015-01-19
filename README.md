# Getting Cleaning Data Project README file
## Course Project from Coursera Course 'Getting and Cleaning Data'
## January 2015
## Todd Curtis

# PROJCECT OBJECTIVE
This objective of the  project was to create an R script called 
run_analysis.R that does the following: 
1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names. 
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

## HOW THE CODE WORKS
Below is an overview of how the code, which is in the file run_analysis.md, processes the raw data to create the output database in objective five.

The overview includes key lines of code, but not the entire code, for this project. For that, please refer to the R script file.

* Objective is merge training and test sets, add appropriate headings, and eliminate data columns that that do not involve the measurement of a mean or standard deviation.
* Two tidy data sets will be created, one with all of the observations, but limited to columns involving measurements of the mean or standard deviation,  and the second which has the means for each data column for each unique  combination of Subject and Activity

*  Working directory was "/Users/airsafe/gitdev/GettingCleaningData/project"

### The first step was to read and merge training and test data, combining several separate text files:
1. Test and training data in X_train.txt and X_test.txt
2. Subject identification codes in subject_train.txt and subject_test.txt
3. Activity codes from y_train.txt and y_test.txt
4. Data column names from features.txt
5. Titles associated with the Activity codes from activity_labels.txt

### The next step was to review the assembled database to confirm a correct assembly, including an additional column with the title associated with the Activity codes

### Next, a revised database was created that included only data associated with mean or standard deviation measurements of the data

From reviewing features_info.txt, and the variable names in featrures.txt in TextWranger, the variables descriging a mean of a signal has the character string 'mean' within the approriate data column name, and the string 'std' for a column with standard deviations.
 
Used the R function 'grep' to find columns without either 'mean' or 'std' and to create data table with only mean and standard deviation values.

Looking at features.txt in TextWranger, should be 33 columns with 'std', and 53 with mean.

From results from running 'grep' twice for "std" and "mean", no variable name has both "std" and "mean", though three included "mean" twice

### Created a revised data frame (bigtable_revised), which is a tidy data frame with only mean and standard deviaiton data columns

### Next objective is to create  a second tidy data frame where each row (observiation) has the means of each of the data columns for each combination of Subject and Activty.

First step is to identify and sort the unique comabinations of Subject (column 1) and Activity (using Activity_ID in column 3)

The program extracted every combination of Subject and Activty_ID, perform a mean of all the data columns,  and rbind it to build a tidy database of the means of the mean and standard deviations

Ensured all numeric columns are of type numeric, and have eight digits to the right of the decimal point, just like the input data

### Export the data frame tidy_means to the working directory to a  tab-delimited text file in the working directory

This completes this project. Two tidy data sets have been created:
1. bigtable_revised which has all the data columns involving a mean  or stndard deviation
2. tidy_means which has the means of all the data columns of  bigtable_revised with each row representing a unique combination of a subject and activity.


## DATA DESCRIPTION AND SOURCE
A full description of the data used in the project is at the site where the data was obtained, and this description is available at:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones 

Here are the data for the project is at: 

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

The data for the project consisted of 10,299 observations in a training set and data set. Each observation was associated with one of 30 subjects, each of whom performed six separate activities. Each of these 180 subject and activity combination were performed and measured at least once.

Of the 561 time and frequency domain variables in the original database, based on the variable names, only 33 were associated with standard deviations and 53 were associated with mean of each measurement. There were also additional data that was not associated with the time and frequency domain variables, and since none of these involved a mean or standard deviation measurement, they were not relevant for this project and were ignored. 

In addition to these 86 columns of mean and standard deviation data, all of which were normalized and bounded within [-1,1],  there were three additional columns. Two were integer values identifying the subject and activity associated with each observation, and the third was a 
descriptive label for the activity code associated with each observation. This last column had character string values, and all the other columns consisted of mean and standard deviation data 

The 10,299 original observations, which were part of the first tidy data set that was the fourth objective of the project,
was the input for the tidy data set that was the fifth project objective.

## NOTES FROM THE ORIGINAL DATA
The README from the original dataset is in the following section. The key differences in the data used in this project and the data from the original data set is that only 86 of the original 561. Also, the files associated
with inertial signals were not relevant to the project and were not processed by the R script.

===============================================================
Human Activity Recognition Using Smartphones Dataset
Version 1.0
==================================================================
Jorge L. Reyes-Ortiz, Davide Anguita, Alessandro Ghio, Luca Oneto.
Smartlab - Non Linear Complex Systems Laboratory
DITEN - Universit‡ degli Studi di Genova.
Via Opera Pia 11A, I-16145, Genoa, Italy.
activityrecognition@smartlab.ws
www.smartlab.ws

-----------------------------------
The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details. 

For each record it is provided:
======================================

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

The dataset includes the following files:
=========================================

- 'README.txt'

- 'features_info.txt': Shows information about the variables used on the feature vector.

* 'features.txt': List of all features.

* 'activity_labels.txt': Links the class labels with their activity name.

* 'train/X_train.txt': Training set.

* 'train/y_train.txt': Training labels.

* 'test/X_test.txt': Test set.

* 'test/y_test.txt': Test labels.

The following files are available for the train and test data. Their descriptions are equivalent. 

* 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 

* 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer X axis in standard gravity units 'g'. Every row shows a 128 element vector. The same description applies for the 'total_acc_x_train.txt' and 'total_acc_z_train.txt' files for the Y and Z axis. 

* 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting the gravity from the total acceleration. 

* 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope for each window sample. The units are radians/second. 

Notes: 
======
* Features are normalized and bounded within [-1,1].
* Each feature vector is a row on the text file.

For more information about this dataset contact: activityrecognition@smartlab.ws

License:
========
Use of this dataset in publications must be acknowledged by referencing the following publication [1] 

[1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012). Vitoria-Gasteiz, Spain. Dec 2012

This dataset is distributed AS-IS and no responsibility implied or explicit can be addressed to the authors or their institutions for its use or misuse. Any commercial use is prohibited.

Jorge L. Reyes-Ortiz, Alessandro Ghio, Luca Oneto, Davide Anguita. November 2012.
