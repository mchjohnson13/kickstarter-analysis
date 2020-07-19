# Kickstarting with Excel

## Overview of Project

Louise is a playwrite wanting to start a crowdfunding campaign. She has estimated a budget of over $10,000. She wants to gain an understanding of what factors make a successful campaign.

Specifically, Louise wants to understand if and how the launch dates and funding goals of past campaigns effected their outcomes.

### Purpose
The purpose of this project is to analyze and create visuals that depict the above referenced information.

## Analysis and Challenges
All analysis are available in the [Kickstarter Challenge Workbook](./Kickstarter_Challenge.xlsx).  

### Analysis of Outcomes Based on Launch Date

The Theatre campaigns based on launch month was charted to show the months with the highest number of successes. To create this graph, a pivot table was used with Category and Year filters, then filtered to the Theatre category. The "outcomes" was used in the columns and the count of outcomes was used in the values. The Date Created Conversion was used for the rows which automatically grouped by month.  
  
In order to do this, the Category, Date Created Converstion, and Year columns were created in the kickstarter tab of the workbook as follows:  
  * The Category column was created by making a copy of the Category and Subcategory column then splitting the text into two separate columns at the '/'.
  * The Date Created Converstion was calculated using `=(((J4051/60)/60)/24)+DATE(1970,1,1)` which converts the date/time number in the launched_at column to a value that excel can recognize as a date.
  * The "Years" column was created using the `YEARS()` function referencing the Date Created Converstion column.  
  
![Outcomes Based on Launch Date](./Theatre_Outcomes_vs_Launch.png)

### Analysis of Outcomes Based on Goals

To visualize the effect of goal amounts on the outcomes of Play campaigns, set ranges of goal amounts were plotted against the percentage of successful and failed campaigns. The data table was created as follows: 
- The `COUNTIFS()` function was used to count the number of campaigns based on the outcomes in each of the goal amount ranges.  
  * Min and Max columns were created as refernce for the `COUNTIFS()` function.
  * The Goal column was created based on the challenge instructions.
  * For the Number Successful column the following formula was used:  
    `=COUNTIFS(Kickstarter!$R:$R,"plays",Kickstarter!$D:$D,CONCATENATE(">",$A2),Kickstarter!$D:$D,CONCATENATE("<",$B2),Kickstarter!$F:$F,"successful")`
      * Subcategory: "plays"
      * Goal: > Min value
      * Goal: < Max value
      * Outcome: "successful"
  * For Number Failed and Number Canceled columns, "successful" was changed to "failed" and "canceled" respectiviely.
- The `SUM()` function was used to add the Number Successful, Number Failed, and Number Canceled columns to create a Total Projects column.
- To calculate the Percentage Successful column, the Number Successful was divided by the Total Projects. This was repeated for the Percentage Failed and Percentage Canceled columns using the respective Number columns.
  
![Outcomes vs. Goals](./Outcomes_vs_Goals.png)
### Challenges and Difficulties Encountered
- The only issues were in learning how GitHub works and using the markdown language.
  * The most challenging was figuring out how to include the images.  
- Data analysis in Excel is straightforward. Some possible challenges include:
  * Using and understanding formulas. New users might have trouble using formulas withough guidance.
  * Understanding pivot tables, which takes some experimentation.  
## Results
- What are two conclusions you can draw about the Outcomes based on Launch Date?
  1. There is a spike in successful outcomes within the Theatre category where the campaigns were started in the month of May. This corresponds to the higher numbers of campaigns started in that month.
  2. The launch month with the least number of successful outcomes is December which also corresponds to the lowest number of campaign starts.
  
- What can you conclude about the Outcomes based on Goals?
  * The campaigns in the "play" subcategory that had goals of less than $5,000 were more likely to have a successful outcome.
  * None of the campaigns in the "play" category were canceled.
  * Overall about one-third of the campaigns in the play subcatagory failed.
  
- What are some limitations of this dataset?
  * This data is only from the Kickstarter platform. There are other platforms some of which may have more or less data in the Theatre category and the Play subcategory.
    - Comparing the outcomes on different platforms could show if there is a better platform to launch on.
    - Pulling the launch date from all of the platforms would give an even better idea if there is a trend in successful outcomes. If different platforms have different successful months, the required launch date could also suggest what platform to use.
  * Information on how each of the campaigns were marketed would give an idea of where to focus efforts.
  * The outcome vs. goal does not take into account the different currency rates. Normalizing to a single currency might shift the data slightly. Looking at the numbers from a single country of interest might also shift the data.
  * There is no information on fees and how much this will effect the total funds raised.
  
- What are some other possible tables and/or graphs that we could create?
  * Plotting outcomes based on the length of the campaign would give an idea if there is a more ideal duration of a campaign.
  * With a quick glance at the outcomes against the "spotlight" column, it looks like campaigns that used the "spotlight" function generally had successful outcomes. It might be worth it to analyze the campaigns that used "spotlight".
