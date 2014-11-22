Code Book for `run_analysis.R`
===========

This code book explains how all of the scripts work and how they are connected to clean and tidy the data for the project. Following is what is inside `run_analysis.R`.

## Variables

  - X_test: table content from `test/X_test.txt`
  - y_test: table content from `test/y_test.txt`
  - subject_test: table content from `test/subject_test.txt`
  - X_train: table content from `train/X_train.txt`
  - y_train: table content from `train/y_train.txt`
  - subject_train: table content from `train/subject_train.txt`
  - features: table content from `features.txt`, descriptive variable names but some symbols need to be removed.
  - activities: table content from `activity_labels.txt`, descriptive activity names that can be used to replace the activity ids.
  - tdAll: data content after the step 4, with descriptive variable names and activity labes.
  - tdMeanGroup: the second data content after the step 5, with the mean values of all the variables for different objects and activities.

## Data Analysis Process  
  Set up the work directory:

  ```r
  setwd("~/UCI HAR Dataset")
  ```
  0. read in data
  
  ```r
  X_test <- read.table("test/X_test.txt")
  y_test <- read.table("test/y_test.txt")
  subject_test <- read.table("test/subject_test.txt")
  X_train <- read.table("train/X_train.txt")
  y_train <- read.table("train/y_train.txt")
  subject_train <- read.table("train/subject_train.txt")
  features <- read.table("features.txt", as.is=TRUE)
  activities <- read.table("activity_labels.txt", as.is=TRUE)
  ```
  1. Merge the training and the test sets to create one data set.
  
  ```r
    dtAll <- rbind(cbind(subject_train, y_train, X_train), cbind(subject_test, y_test, X_test))
    rm(X_test, y_test, subject_test, X_train, y_train, subject_train)
  ```
  2. Appropriately label the data set with descriptive variable names.
  
  ```r
    features$V2 <- gsub("\\(\\)", "_", features$V2)
    features$V2 <- gsub("\\-", "_", features$V2)
    names(dtAll) <- c("Subject", "Activity", features$V2)
  ```
  3. Extract only the measurements on the mean and standard deviation for each measurement.
  
  ```r  
    library(dplyr)
    tdAll <- tbl_df(dtAll)
    tdAll <- tdAll[grepl("Subject|Activity|_mean_|_std_", names(tdAll))]
  ``` 
  4. Apply descriptive activity names to name the activities in the data set
  
  ```r  
    tdAll <- mutate(tdAll, Activity = activities$V2[Activity])
  ```  
  5. Creates a second, independent tidy data set with the average of each variable for each activity and each subject.
  
  ```r  
    tdGroups <- group_by(tdAll, Subject, Activity)
    cols <- names(tdAll)[-(1:2)]
    dots <- sapply(cols ,function(x) substitute(mean(x), list(x=as.name(x))))
    tdMeanGroup <- do.call(summarise, c(list(.data=tdGroups), dots))
  ```  
  6. Write into a text file.
  
  ```r
    write.table(tdMeanGroup, "tidyMeanData.txt", row.names=F, quote = F)
  ```
## Comments
The data may be further broken down to shorter and more readable variable names, however, the data would become very complicated with different measures on the same devices, so we will end up here. 
