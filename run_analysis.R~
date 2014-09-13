# GETTING AND CLEANING DATA - COURSE PROJECT
# 
# The following code creates a new tidy dataset using using data that was
# given to us as part of the course project. 
#
# The new dataset is exported in both .csv and .txt format. It
# contains the average mean and standard deviation measurements for 
# each variable for each "Subject" and "Activity.
#
#
# INSTRUCTIONS:
#
# 1. You must have the plyr and reshape2 libraries installed.
#
# 2. Add the following files to your working directory.
# 		X_test.txt
# 		X_train.txt
# 		y_test.txt
# 		y_train.txt
# 		subject_test.txt
# 		subject_train.txt
# 		features.txt
# 		activity_labels.txt
#
# 3. Run the script.
#


# LOAD LIBRARIES
library(plyr)
library(reshape2)

# READ IN FILES
xtest <- read.table("X_test.txt")
xtrain <- read.table("X_train.txt")
ytest <- read.table("y_test.txt")
ytrain <- read.table("y_train.txt")
stest <- read.table("subject_test.txt")
strain <- read.table("subject_train.txt")
xfeatures <- read.table("features.txt")
yactlab <- read.table("activity_labels.txt")

# RENAME COLUMNS IN X_TEST & X_TRAIN WITH FEATURES
colnames(xtest) <- xfeatures$V2
colnames(xtrain) <- xfeatures$V2

# REPLACE NUMBERS IN Y_TEST & Y_TRAIN WITH ACTIVITY LABELS
ytest <- as.character(ytest$V1)
ytest[ytest == "1"] <- "WALKING"
ytest[ytest == "2"] <- "WALKING_UPSTAIRS"
ytest[ytest == "3"] <- "WALKING_DOWNSTAIRS"
ytest[ytest == "4"] <- "SITTING"
ytest[ytest == "5"] <- "STANDING"
ytest[ytest == "6"] <- "LAYING"
ytest <- data.frame(ytest)
ytrain <- as.character(ytrain$V1)
ytrain[ytrain == "1"] <- "WALKING"
ytrain[ytrain == "2"] <- "WALKING_UPSTAIRS"
ytrain[ytrain == "3"] <- "WALKING_DOWNSTAIRS"
ytrain[ytrain == "4"] <- "SITTING"
ytrain[ytrain == "5"] <- "STANDING"
ytrain[ytrain == "6"] <- "LAYING"
ytrain <- data.frame(ytrain)

# GIVE Y_TEST/TRAIN AND SUBJECT_TEST/TRAIN COLUMN NAMES
colnames(ytest) <- c("ACTIVITIES")
colnames(stest) <- c("SUBJECT")
colnames(ytrain) <- c("ACTIVITIES")
colnames(strain) <- c("SUBJECT")

# ADD A COLUMN TO THE LEFT OF SUBJECT TEST/TRAIN DATA TO IDENTIFY EACH AS TEST OR TRAIN 
#stest$TEST_OR_TRAIN <- rep("TEST",nrow(stest)) 
#stest <- stest[,c(2,1)]
#strain$TEST_OR_TRAIN <- rep("TRAIN",nrow(strain)) 
#strain <- strain[,c(2,1)]

# EXTRACT COLUMNS / VARIABLES FOR MEAN AND STANDARD DEVIATION (STD) FROM X_TEST AND X_TRAIN
# USED GREP TO FIND MEAN AND STD COLUMNS AND USED CBIND TO PUT THEM TOGETHER
xTestExt <- cbind(xtest[,grep("mean()", colnames(xtest), fixed=TRUE)], xtest[,grep("std()", colnames(xtrain), fixed=TRUE)] )
xTrainExt <- cbind(xtrain[,grep("mean()", colnames(xtrain), fixed=TRUE)], xtrain[,grep("std()", colnames(xtrain), fixed=TRUE)] )

# COMBINE ALL OF THE TEST DATA AND TRAIN DATA INTO NEW DATAFRAME "Data"
dataTest <- cbind(ytest, xTestExt)
dataTest <- cbind(stest, dataTest)
dataTrain <- cbind(ytrain, xTrainExt)
dataTrain <- cbind(strain, dataTrain)
Data <- rbind(dataTest, dataTrain)

# MELT "Data" 
# USE DCAST() TO CREATE THE FINAL DATASET: DataFinal
DataMelt <- melt(Data, id.vars = c("SUBJECT","ACTIVITIES"))
DataFinal <- dcast(DataMelt, SUBJECT + ACTIVITIES ~ variable, mean)

# EXPORT DataFinal TO TEXT AND CSV:
# GCD_Project_Dataset.csv
# GCD_Project_Dataset.txt
write.csv(DataFinal, file = "GCD_Project_Dataset.csv")
write.table(DataFinal, "GCD_Project_Dataset.txt", sep=",") 





