Getting and Cleaning Data - Course Project
=========
## Background
The purpose of this project is to collect, work with, and clean a data set. The goal is to prepare tidy data that 
can be used for later analysis.
This repo contains:
1. the script,`run_analysis.R`, for performing the analysis
2. a code book, `CodeBook.md`, that describes the variables, the data, and any transformations or work that you performed to clean up the data. 
3. this `README.md` explains how all of the scripts work and how they are connected. 

One of the most exciting areas in all of data science right now is wearable computing.
Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. 
The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S 
smartphone. 

A full description is available at the site where the data was obtained:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Here are the data for the project:
https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

## The Code
The R script, `run_analysis.R`, does the following. 
- Merges the training and the test sets to create one data set.
- Extracts only the measurements on the mean and standard deviation for each measurement. 
- Uses descriptive activity names to name the activities in the data set
- Appropriately labels the data set with descriptive variable names. 
- From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.
