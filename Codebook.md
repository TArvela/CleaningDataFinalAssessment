#Data Acquisition
Dataset download and unzip
<pre>
zipname <- "getdata_dataset.zip"

if (!file.exists(zipname)){
  url <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
  download.file(url, zipname)
}  
if (!file.exists("UCI HAR Dataset")) { 
  unzip(zipname) 
}
</pre>


#Data reading
<pre>
## Read and import labels and features
labels <- read.table("UCI HAR Dataset/activity_labels.txt")
features <- read.table("UCI HAR Dataset/features.txt") 
  
## Read and import x and y test data
xtest <- read.table("UCI HAR Dataset/test/X_test.txt")
ytest <- read.table("UCI HAR Dataset/test/y_test.txt")

## Read and import x and y train data
xtrain <- read.table("UCI HAR Dataset/train/X_train.txt")
ytrain <- read.table("UCI HAR Dataset/train/Y_train.txt")

## Read and import subject train and test data
subtrain <- read.table("UCI HAR Dataset/train/subject_train.txt")
subtest <- read.table("UCI HAR Dataset/test/subject_test.txt")

</pre>


#Merging of data to a single variable
<pre>
## Fuse all x data
x <- rbind(xtest,xtrain)

## Fuse all y data
y <- rbind(ytest,ytrain)

## Fuse all subject data (subject id)
sub <- rbind(subtest,subtrain)
names(sub) <- "SubjectID"

## Create new variable with x data and y data (y was entered as a new column)
tot <- cbind(x,y)

## Create new column about subject ID (result to requirement 1.)
tot <- cbind(tot,sub)
</pre>

#Define column names and merge data to obtain activity name for each row
<pre>
## Define names for columns (result to requirement 4.)
colnames(tot)<-c(as.character(features[,2]),c("activity","SubjectID"))

## Define descriptive activity names (result to requirement 3.)
totMergedActivity <-merge(x=tot,y=labels, by.x="activity", by.y="V1")
</pre>

#Create variable containing only Mean or Std columns
<pre>
## Define which columns are either means or std (requirement 2.)
meanStdCol <- grep("mean|std", names(totMergedActivity))
totMeanStd <- totMergedActivity[,meanStdCol]
</pre>

#Tidy data, grouped by SubjectID and activity
<pre>
## Create tidy data by grouping data by id and activity and averaging it (requirement .5)
tidy <- aggregate(.~SubjectID+V2, totMergedActivity, mean)

</pre>

#Write Tidy data into file
<pre>
## Write tidy data into file 
write.table(tidy, file="tidy_mean.txt", row.names = FALSE)
</pre>


