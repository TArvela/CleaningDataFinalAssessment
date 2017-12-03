# CleaningDataFinalAssessment (Coursera "Getting and Cleaning Data" Course Project)

## <u>The R Script will</u>


* 1. Download the Dataset Zip file (https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip)
* 2. Unzip the zip file
* 3. Execute several operations to format the data as needed for the Assignment.

## <u>Operations</u>
Each Operation is commented more in details in the R script

### Read and Import Data
Every file is read and assigned to a variable

### Combine Data
Variables are fused using cbind and rbind operations to create a single variable containing all data from all files

### Columns names of total variable are defined
Columns are named according to data contained in "features.txt" file

### Data and activity labels are merged according to their values
Each activity id is assigned to a particular activity

### Means and Std values are isolated 
Assign values which colnames contains either "mean" or "std" to an other variable (totMeanStd)

### Tidy variable is created and populated
Tidy variable containing tidy average data as required for the exercise is created using an aggregate function by "SubjectID" and "V2" (corresponding to activity) variables 

### Write tidy results in separated file
A "Write.table" function is used to write a "tidy_mean.txt" file in the working directory

