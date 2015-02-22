#Notation of variables:
    ··* column 1: The subject who was in either the train set or test set was labeled with
            "train" or "test", correspondingly.
    ··* column 2: The identification number for the subject
    ··* column 3: The activity that a subject was taking
    ··* column 4-69:
             ···The prefix "t" denotes the time domain signals, which were measured at a frequency
                of 50Hz.
             ···The prefix "f" denotes the frequency domain signals.
             
             ···"Body" denotes that the values are measured for the movement of subject body.
             ···"Gravity" denotes that the values are gravity signals.
             
             ···"Acc" denotes linear acceleration, and "Gyro" denotes the angular velocity values.
             
             ···"Jerk" means that the value are Jerk signals derived in time.
             ···"Mag" means that the value are the magnitude of corresponding raw signals or Jerk signals, calculated using the Euclidean norm 
             
             ···"X","Y","Z" denotes the values for the three dimension in Euclidean space.
             
             ···"mean" and "std" denote the mean and standard deviation for the measured value, correspondingly.


#data
···This is the [link](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip) of raw data provided on the course website

···See the [detailed description](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones) of the data at:          

···The mean and standard deviation for the measurement were selected to be presented in the final tidy data set.

···The data in the final tidy data set is grouped by "train" or "test" group, and the variables are presented for each activity that a subject was taking


#Data processing procedure
   ··1. Load the "train" and "test" data set into R, separately.
   ··2. Create new variables for labelling each observation, using "subject" and "activity" labels.
   ··3. Mark the "train" and "test" group with corresponding tag.
   ··4. Combine the "train" and "test" data and subset the data set to extract the mean and standard deviation values.
   ··5. Group the subsetted data set by "group", "subject" and "activity", then apply mean function to obtain the mean values,
        this results in the final tidy data set.
   ··6. Export the final data set to a .txt file.