# LSEG
LSEG assignment

For this assignment I have created two functions, which I will explain further, individually:

1. "datapoints" function
   - has an input parameter which is the path + filename of the CSV file
   - it reads the CSV file into a dataframe
   - then it creates a list with all the values from column Timestamp
   - I am using this list to check first if all the Dates are in the correct dateformat with exception handling
   - then I create another list where I put only a subset of data from the Timestamp list, in order to take all the values, except the last 29 which are not a candidate for the random timestamp selection
   - from the new list I choose a random timestamp
   - I create another dataframe which it will be used as output
   - In order to select only 30 consecutive rows from the first dataframe, starting with a random timestamp, I need to set a starting index
   - looping in the first dataframe from start_index, I put all the read values in the output dataframe until it reaches length 30
   - return output_set as this will be the input for the second function
  
2.  "generate_outliers" function
   - receives the output dataframe from previous functiuon as an input parameter and first thing, checks if the dataframe is empty with error handling
   - I create a list with all the values from Stock-Price column and then calculate the Mean and Standard Deviation using dedicated NumPy functions. Also check if a division to zero could occur.
   - starting the outliers detection with setting the threshold value and calculate the z-score for each Stock-Price. I am choosing as an outlier all the values that are with 2 std deviations above or below the mean and put them into a new list
   - In the dataframe I create 3 new columns and assign the logic to them: "Mean", "Stock Price - Mean" and "% deviaion". The last column, for me has the following logic: it shows with how many percentages the Stock-Price is above of below the Mean.
   - in a new dataframe, "outliers_datapoints" I select all the rows from main dataframe that are considered outliers based on the above logic and return it

The "main" program:
  - starts with setting up the path of the CSV files folder,
  - searches for all the CSV files in that folder,
  - checks if there are any CSV files in that location, with the specified name format
  - and if so, for each file detected it calls the above functions. The output is saved into a pandas dataframe and a new CSV file is created. The new file has "_Outliers" as a name suffix.

For running the entire thing, you only need to set up the Path variable, where the CSV files for each stock market are.
