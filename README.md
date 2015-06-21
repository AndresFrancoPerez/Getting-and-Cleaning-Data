#Getting and Cleaning Data
## Course Project
---------------------------------------------
###Project instructions:
You should create one R script called run_analysis.R that does the following. 
 1. Merges the training and the test sets to create one data set.
 2. Extracts only the measurements on the mean and standard deviation for each measurement. 
 3. Uses descriptive activity names to name the activities in the data set
 4. Appropriately labels the data set with descriptive variable names. 
 5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each      activity and each subject.

###This project contains...
* A script in R language, with the codes to storage, process and obtain tidy data.
* A code book, including the description of the variables (The ones that came in the raw data source and the ones calculated and used in the tidy data contruction).
* A README file with the summary of the project.

###Script logic (in the run_analysis.R file)
 1. Load, and intall if necessary, the libraries to call functions to process the data.
 2. Read the raw files, from the local directory, for all the measurments and  variables necessary.
 3. Extract, process and bind the different sources of data into one tidy file.
 4. Export the tidy data file into a text file (.txt)
