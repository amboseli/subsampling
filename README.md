This code randomly subsamples the following variables on the leve of each individual year of life:
1. Rank
2. Percent cycling
3. Percent infant <3 months
4. Group size
5. N adult maternal kin

This code asks what happens if there are random days of data missing from the dataset to represent the fact that 
there are periods where we observe the baboon groups more or less often.  It however, it probably not as good at 
modelling a case where there are big gaps in observations where we don't see groups for a month or more.

For the subsampling analysis each variable has its own code but the general idea is the same.  I first make dataframe
where each row represents a measurement of that particular variable (e.g., for rank each individual has up to 12 rows 
representing the monthly rank data).  I then filter that dataframe so only individuals with the full amount of data for 
that year (e.g., all 12 months of ranks per year).  I assign a random number (which I call the 'keep' column) from 1 to y 
for each row grouped by individual and year, where y represents the maximum number of data points on that individual for 
the year of life (e.g., 12 for ranks representing 12 total ranks per year).  I subsample by only taking rows where the value in 
the 'keep' column is less than or equal to the threshold (e.g., if I'm only sampling 6 of the 12 rank data points, my keep value 
would be <=6 and any rows with the random number greater than 6 would be dropped).  I then take the average of the subsampled points
per individual per year to calculate the mean variable for that year of life.  I repeat the subsampling for a variety of different
values and then plot correlation matrices.

