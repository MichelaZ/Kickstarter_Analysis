### Analysis of Theater Kickstarter Outcomes:

## Project Purpose:
In this project I used excel to analyze Kickstarter data for a client so they could see how their campaign's launch date and funding goals compared to similar campaigns. The brief stated:
> Louise’s play Fever came close to its fundraising goal in a short amount of time. Now, she wants to know how different campaigns fared in relation to their launch dates and their funding goals. Using the Kickstarter dataset that you’ve already combed through, you’ll visualize campaign outcomes based on their launch dates and their funding goals. You’ll then submit a written report based on your analysis and the visualizations you create.

## Deliverable 1:

##### Deliverable 1: Purpose
Deliverable 1 was a 
> Use your knowledge of pivot tables and graphing in Excel to visualize campaign outcomes ("successful," "failed," and "canceled") based on launch date.

1. To filter data by year in the pivot table I used the YEARS function on the "Date Created Conversion" column which I made from converting Unix timestamps into a date excel can read using the formula below:
```
=(((I2/60)/60)/24)+DATE(1970,1,1)
=YEAR([@[Date Created Conversion]])
```
2. Then I created the Pivot table with the following fields: 
	- Filters: "Years" & "Parent Category"
		- I filtered the "Parent Category" to "Theater"
	- Columns: "Outcomes"
	- Rows: "Date Created Conversion"
		- To show the Dates as months I clicked the field "Date Created Conversion", "Feild Settings", "Number Format", selected "Date" and "M."
	- Values: Count of "Outcomes"
![Theater outcomes by launch date pivot table.](/assets/images/pivot1.png)
3.  Then I created a line graph based of the pivot table called: Theater_Outcomes_vs_Launch.png

###### Deliverable 1: Challenges
- I think the extra step of adding the years column to the data is unnecessary. Instead create a pivot table then right click a value in the "row labels" column. Select group which will open the "grouping" menu. 
![Grouping Menu.](https://github.com/MichelaZ/Kickstarter_Analysis/blob/main/Submission/grouping.png)
- In the grouping menu select "Months" and "Years." This will make your fields look like this:
![Feild List 1.](/assets/images/feilds1.png)
- Move "Years" from the "Rows" to the "Filters" in the fields list. It will look like this, and your pivot table will work the same as creating a years column in your dataset. 
![Feild List 2.](/assets/images/feilds2.png)

## Deliverable 2:

##### Deliverable 2: Purpose
Deliverable 2 was a line graph showing the relationship of goals and the outcomes for play campaigns on Kickstarter. The brief stated:
>Use your Excel skills to visualize the percentage of successful, failed, and canceled plays based on the funding goal amount. You'll need to use a new function, COUNTIFS(), to collect the outcome and goal data for the “plays” subcategory.

##### Deliverable 2: Method
First, I made the data set into a table. Formatting the data as a table makes it easier to use the fill function to pull your formulas down without losing the ability to add data later, like if you used "$". To keep my data easy to manipulate I created a Kickstarter_Admin worksheet to store all my reference cells. That way if you wanted to change a filter, I only need to change it once and all the values referencing that cell are updated.
![Image of reference cells](/assets/images/Kickstarter_Admin.png)
I used CONCAT to incorporate my reference cells to the labels in the goal column. Then I used COUNTIFS, SUM, and simple division to collect the rest of the data. Please note when using logic operators in excel an ampersand needs to be inserted before the reference cell. For the most part I was able to pull the formulas down to fill in the rest of the table. I created a graph based on this, "Outcomes_vs_Goals.png," that will be discussed in the results section. Below is an example row to show how the references and table work.

_Goal:_
```
=CONCAT(Kickstarter_Admin!B2, " ", "to", " ",  Kickstarter_Admin!A3)
```
_Number Successful:_
```
=COUNTIFS(Table2[[#Data],[Subcategory]],"="  &Kickstarter_Admin!$C$2,Table2[[#Data],[outcomes]],"="  &Kickstarter_Admin!$D$2, Table2[[#Data],[goal]],">=" &Kickstarter_Admin!$B2, Table2[[#Data],[goal]],"<=" &Kickstarter_Admin!$A3)
```
_Number Failed:_
```
=COUNTIFS(Table2[[#Data],[Subcategory]],"="  &Kickstarter_Admin!$C$2,Table2[[#Data],[outcomes]],"="  &Kickstarter_Admin!$D$2, Table2[[#Data],[goal]],">=" &Kickstarter_Admin!$B2, Table2[[#Data],[goal]],"<=" &Kickstarter_Admin!$A3)
```
_Number Canceled:_
```
=COUNTIFS(Table2[[#Data],[Subcategory]],"="  &Kickstarter_Admin!$C$2,Table2[[#Data],[outcomes]],"="  &Kickstarter_Admin!$D$3, Table2[[#Data],[goal]],">=" &Kickstarter_Admin!$B2, Table2[[#Data],[goal]],"<=" &Kickstarter_Admin!$A3)
```
_Total Projects:_
```
=SUM(C4:E4)
```
_Percentage Successful:_
```
=C4/F4
```
_Percentage Failed:_
```
=D4/F4
```
_Percentage Canceled:_
```
=E4/F4
```
##### Deliverable 2: Challenges
I did find this method took quite a bit of time and it makes your chart less dynamic. Your only way to change your filters is to change the reference cells. I think a better way to do it would be to make a pivot table from the original Kickstarter data. Set the filters: parent category and  subcategory, columns: outcomes, rows: goals, values: count of outcomes. Filter the subcategory to "Plays." Then right click a value in the "row labels" column. Select group which will open the "grouping" menu.  If you input 1000 for the "starting value", 50,000 for the "ending value", 5000 as the "by" value and then click okay. Right click on a value in one of outcome columns. Hoover over "Show Value As" and select "% of Row Total." Then I made a line chart and unselected the "live" outcomes. 
![Line chart and pivot table showing percent of play outcomes by dollar amount.](/assets/images/Outcomes_vs_Goals_Pivot.png)
The values are slightly different, but the chart looks the same, it took about 30 seconds, and this way it remains dynamic. When I use excel to look at data I find my clients are usually pretty unfamiliar with pivot tables, so making a dashboard sheet and connecting all the charts with slicers and timelines make it easier for these users to navigate. Using the same data source makes linking these objects a lot easier. This also allows you to hide the field buttons on your chart which gives it a cleaner look.


## Project Results: 

##### Deliverable 1: Results
![Feild List 2.](/assets/images/Theater_Outcomes_vs_Launch.png)
__Summer Theater__
According to this data theater Kickstarters are more popular in the summer. This may be because it is typically the off season for professional theater and when Summer Theater which allows for more experimentation occurs. Successfully funded theater projects tend to increase as the summer season approaches and decrease about a month before the fall season starts in September. Britannica says:
> Summer-theatre plays are often Broadway hits of previous seasons or new plays being tested for the Broadway stage.
__Winter Break_
Another conclusion we can draw from this graph is that there tend to be less Theater Kickstarters launched in the winter months. Very few shows tend to open from December to February "winter break." Christmas week and into New Years tend to have the largest number of sales for the year at the Broadway box office. Then in January sales tend to drop off steeply until the spring season. 

##### Deliverable 2: Results
![Line chart showing percent of play outcomes by dollar amount.](/assets/images/Outcomes_vs_Goals.png)
This chart shows that the highest success rate is in projects with goals of less than 5,000 dollars. This may point out a potential issue with the dataset. If you have a smaller goal like $5000 and you are 5% away from your goal, you might ask a friend to donate the money so that you can call the project a success. If your goal is only $5000 then 5% is only $250, but if your goal is $50,000 and 5% is $2,500 this is going to be a lot harder to do.

###### Other Data Points to Analyze:
__Duration of Campaign:__
I thought the duration of campaign might be an interesting metric to look at, but I found most of them were about the same. I did some research, Kickstarter's help ![Column chart showing percent of play outcomes by duration of campaign.](/assets/images/Average_Duration.png)
FAQ recommends the following:

>Projects on Kickstarter can last anywhere from 1 - 60 days. We've done some research and found that projects lasting any longer are rarely successful.
>We recommend setting your campaign at 30 days or less. Campaigns with shorter durations have higher success rates and create a helpful sense of urgency around your project.

Without tangible results it is probably hard to maintain interest after the initial interest wears off, so if a campaign hasn't reached its goal by then it probably won't.
__Theater Outcomes by Country:__
Another data point I thought might be helpful to look at was outcomes based on countries. I found that the countries where Kickstart campaigns were most popular the United States, Great Britain, and Canada also had the most theater and play campaigns. These campaigns also tended to be slightly more successful than an average Kickstarter. I think if you are outside of these countries you may want to look into another platform to host your campaign, just because it does seem to be much more hit or miss outside of these three countries.	
	__CA__	__US__	__GB__
plays	73%	61%	76%
theater	64%	58%	72%
All	44%	54%	61%
![Column chart showing percent of play outcomes by duration of campaign.](Theater_Outcomes_by_Country.png)

##### Limitations:
- It would be nice to know when campaigns got the most donations. Do they get more donations when they first launch, in the middle or toward the end of their duration? This may help to shed some light on the issue of looking at outcomes by goals from earlier.
- This data is five years old and the internet changes very quickly, so these findings could be irrelevant.
- There is no data on stretch goals.

