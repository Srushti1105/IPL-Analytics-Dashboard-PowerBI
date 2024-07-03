# IPL-Analytics-Dashboard-PowerBI

Data Walkthrough
	DATA CLEANING
     Select Teams and update rising pune supergiants and rising pune supergiant and city 

	DATA PROCESSING
Do some calculations in data.
Date table: when we want to create time intelligence functions we need to use date tables
Create a new table and using calender function along with MIN and MAX take out the starting and ending dates from 2008 to 2022
Now from this column extract the year of all the dates 

	DATA MODELLING
Create relationship with the newly formed table 

	Add canvas Background 
Add title

	KPI: select KPI Card

Title winner: winner of that particular season 
                        Need to create filter of season
                         Add a slicer and add year field from calender table
We’ll use DAX query to determine this: 
Title Winner = VAR max_date= CALCULATE(MAX('Calender Table'[Date]), ALLSELECTED(ipl_matches_2008_2022), VALUES(ipl_matches_2008_2022))
var title_winner = CALCULATE(SELECTEDVALUE(ipl_matches_2008_2022[winning_team]), 'Calender Table'[Date]= max_date)
return title_winner

We know the final match is played on the last date of that season and we need to find winner of that season so we first need to find the max date of that season by using CALCULATE and the time intelligence function and we don’t want the table to be filtered so we’ve used ALLSELECTED and using VALUES we’re getting the distinct values.

One more variable is used named title_winner which is selecting only the winning team name where the date should be maximum and then we’re returning this variable.

Orange Cap and Purple cap will take bowler and batter resp. as fields
Tournament 6’s and 4’s: We’ll use count of batsman’s runs as field and will apply the filter of only boundaries of 6 and 4 runs respectively

Now we need to add Player’s Stats 
When we make a slicer which will have batter as field 
** this slicer will affect the whole KPIs so in order to keep all of them unaffected we need to edit the interaction of this particular visual
We now need to find out total runs:  i.e. just take sum of batsman’s runs
No of 6s and 4s hit by batsman:  count of batsman runs as zero in the fields and then apply basic filters on the sum of batsman’s run and select 6 and 4 resp. along with selecting non boundary as 0

Strike Rate: (Total number of runs in an innings / number of deliveries faces by batsman )* 100
Create New Measure for this: 
Strike rate for batsman = (SUM(ipl_ball_by_ball_2008_2022[batsman_run])/COUNT(ipl_ball_by_ball_2008_2022[ball_number]))*100




