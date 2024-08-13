The `run_analysis.R` script downloads the data set, prepares it for the analysis and executes the 5 steps in the instructions of the course project.

0.1.  Download the data set
		- Data set is downloaded and extracted to the folder called `UCI HAR Dataset`.

0.2.  Assign each data set to a variable
		- `features` <- `features.txt` (561 rows by 2 columns). This data set contains the list of features.
		- `activity_labels` <- `activity_labels.txt` (6 rows by 2 columns). This data set contains the list of activities.
		- `subject_test` <- `test/subject_test.txt` (2947 rows by 1 column). This data set lists the 9/30 volunteer test subjects.
		- `x_test` <- `test/X_test.txt` (2947 rows by 561 columns). This data set contains the results of the volunteer test subjects.
		- `y_test` <- `test/y_test.txt` (2947 rows by 1 columns). This data set identifies the activities of the results of the test subjects.
		- `subject_train` <- `train/subject_train.txt` (7352 rows by 1 column). This data set lists the 21/30 volunteer train subjects.
		- `x_train` <- `train/X_train.txt` (7352 rows by 561 columns). This data set contains the results of the volunteer train subjects.
		- `y_train` <- `train/y_train.txt` (7352 rows by 1 columns). This data set identifies the activities of the results of the train subjects.

1.  Merges the training and the test sets to create one data set
		- `x` (10299 rows by 561 columns) is created as `x_test` merged with `x_train` using `rbind()` function.
		- `y` (10299 rows by 1 column) is created as `y_test` merged with `y_train` using `rbind()` function.
		- `subject` (10299 rows by 1 column) is created as `subject_test` merged with `subject_train` using `rbind()` function.
		- `Merged_Data` (10299 rows by 563 column) is created by merging `subject`, `y` and `x` using `cbind()` function.

2.  Extracts only the measurements on the mean and standard deviation for each measurement
		- `ExtractData` (10299 rows by 88 columns) is created as a subset of `Merged_Data`, with only columns: `subject`, `code`, and the `mean` and standard deviation (`std`) of each measurement.

3.  Uses descriptive activity names to name the activities in the data set
		- The activity `code` column of the data set `ExtractData` is replaced with corresponding label using the second column of the `activity_labels` variable.

4.  Appropriately labels the data set with descriptive variable names
		- `code` column in `ExtractData` renamed to `activity`
		- All `Acc` in column’s names are replaced by `Accelerometer`
		- All `Gyro` in column’s name are replaced by `Gyroscope`
		- All `BodyBody` in column’s name are replaced by `Body`
		- All `Mag` in column’s name are replaced by `Magnitude`
		- All leading `t` in column’s name are replaced by `Time`
		- All leading `f` in column’s name are replaced by `Frequency`
		- All `tBody` in column’s name are replaced by `TimeBody`
		- All `-mean()` in column’s name are replaced by `Mean`
		- All `-std()` in column’s name are replaced by `STD`
		- All `-freq()` in column’s name are replaced by `Frequency`
		- All `angle` in column’s name are replaced by `Angle`
		- All `gravity` in column’s name are replaced by `Gravity`

5.  From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject
		- `FinalData` (180 rows by 88 columns) is created as the summary of `ExtractData` as per the instructions.
		- Export `FinalData` into the `FinalData.txt` file.