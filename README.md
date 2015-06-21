##Description for the behaviour of the run_analysis.R Code:

#Set the libraries to get some functions that will be executed 
library(data.table) ## if it's not intalled then run install.packages("data.table")
library(reshape2) ## if it's not intalled then run install.packages("reshape2")

---------------------------------------------------------------------------------------------------
#In this part we'll be working with the Tests files, set in them into tidy data

#Read the raw files 
act_lab <- read.table("./UCI HAR Dataset/activity_labels.txt")[,2] ##Get the Activity Labels text file and storage it in act_lab variable
feat <- read.table("./UCI HAR Dataset/features.txt")[,2] ##Get the Features text file and storage it in feat variable
x_test <- read.table("./UCI HAR Dataset/test/X_test.txt") ##Get the X-Test file and storage it in x_test variable
y_test <- read.table("./UCI HAR Dataset/test/y_test.txt") ##Get the Y-Test file and storage it in y_test variable
subj_test <- read.table("./UCI HAR Dataset/test/subject_test.txt") ##Get the Subject-test file and storage it in subj_test variable

 Extract only the measurements on the mean and standard deviation for each measurement.
extract_features <- grepl("mean|std", features)

 Load and process X_test & y_test data.

#Extracts, from the raw files, the information we need to make the tidy data:

x_test = X_test[,extract_features] ##Extracts the measurements for the mean an standard deviation only


names(X_test) = features


 Load activity labels
y_test[,2] = activity_labels[y_test[,1]]
names(y_test) = c("Activity_ID", "Activity_Label")
names(subject_test) = "subject"

 Bind data
test_data <- cbind(as.data.table(subject_test), y_test, X_test)

 Load and process X_train & y_train data.
X_train <- read.table("./UCI HAR Dataset/train/X_train.txt")
y_train <- read.table("./UCI HAR Dataset/train/y_train.txt")

subject_train <- read.table("./UCI HAR Dataset/train/subject_train.txt")

names(X_train) = features

 Extract only the measurements on the mean and standard deviation for each measurement.
X_train = X_train[,extract_features]

 Load activity data
y_train[,2] = activity_labels[y_train[,1]]
names(y_train) = c("Activity_ID", "Activity_Label")
names(subject_train) = "subject"

 Bind data
train_data <- cbind(as.data.table(subject_train), y_train, X_train)

 Merge test and train data
data = rbind(test_data, train_data)

id_labels   = c("subject", "Activity_ID", "Activity_Label")
data_labels = setdiff(colnames(data), id_labels)
melt_data      = melt(data, id = id_labels, measure.vars = data_labels)

 Apply mean function to dataset using dcast function
tidy_data   = dcast(melt_data, subject + Activity_Label ~ variable, mean)

write.table(tidy_data, file = "./tidy_data.txt")
