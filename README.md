# GettingAndCleaningData
This folder is for the Course Project of Coursera GettingAndCleaningData Course


The following code is for creating the tidy data set for the course project

library(dplyr)

###read "features" into R and extract feature name
feature <- read.table("features.txt")
featureName <- as.character(feature$V2)

###dealing with "Traning set"
###read "Training set", "Training labels" and "subject_test" into R
TrainSet <- read.table("train/X_train.txt")
TrainLabels <- read.table("train/y_train.txt")
subjectTrain <- read.table("train/subject_train.txt")

###add colNames/variable names to TraingSet
names(TrainSet) <- featureName

##cbind "TraningLabels" and "subjectTrain" to TrainingSet and rename the first two columns
TrainSet <- cbind(TrainLabels, TrainSet)
TrainSet <- cbind(subjectTrain, TrainSet)
names(TrainSet)[1:2] <- c("subject", "ActivityLabels")

#dealing with "test set"
#read "test set", "Test labels" and "subject_test" into R
TestSet <- read.table("test/X_test.txt")
TestLabels <- read.table("test/y_test.txt")
subjectTest <- read.table("test/subject_test.txt")

#add colNames/variable names to TestSet
names(TestSet) <- featureName

#cbind "TestLabels" and "subjectTest" to TestSet and rename the first two columns
TestSet <- cbind(TestLabels, TestSet)
TestSet <- cbind(subjectTest, TestSet)
names(TestSet)[1:2] <- c("subject", "ActivityLabels")

#merges the test/train data sets
TestTrain <- rbind(TestSet, TrainSet)

#subset the data table with mean and standard deviation
TestTrainSubset <- TestTrain[,c(1:2, sort(union(grep("mean\\(\\)", names(TestTrain)), 
                                                grep("std\\(\\)", names(TestTrain)))
                            ))]

#set activity names using descriptive word
#use factor, set values to different factor levels
factorActivity <- factor(TestTrainSubset$ActivityLabels)
levels(factorActivity) <- c("WALKING", "WALKING_UPSTAIRS", 
                            "WALKING_DOWNSTAIRS", "SITTING", "STANDING", "LAYING")
TestTrainSubset$ActivityLabels <- factorActivity

#convert TestTrainSubset to tbl, and group by subject and activity
TestTrainSubset <-tbl_df(TestTrainSubset)
TidyBy_Subject_Activity <- group_by(TestTrainSubset, subject, ActivityLabels)

#summarize/take_mean the grouped Tidy data set
TidyMean <- summarise_each(TidyBy_Subject_Activity, funs(mean))

#save TidyMean as txt file
write.table(TidyMean, file="TidyMean.txt", row.names=FALSE)
