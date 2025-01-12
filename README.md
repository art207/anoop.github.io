# Power BI Reports

## [Emergency Service Analysis](https://app.powerbi.com/view?r=eyJrIjoiMDFmNzY0OTgtMTM0NC00ODU1LThlY2YtNWM0ZGI0YzAyMjI4IiwidCI6ImJjMjQxODZjLTc0NzUtNGM2ZS05NThhLTg4MmMzYTZiOWIwYSIsImMiOjJ9)

This is a completely random and anonymised data set

Analysis done through this dashboard 

* No of calls

* Time between time of call and ambulance departure.

* Time taken for ambulance to arrive to patient.

* Time taken from patient house to hospital.

* No of jobs between specific period i.e over lunch times 12:00-14:00

* Does the despatch code affect the timings?

* Does the call handler have any impact?

* Do certain hospitals have issues in particular aspect

* What does the data say based upon the ambulance station?

* Does patient Sex affect handover times?

<details>
  <summary>Report Snapshots</summary>
  
![Emergeny Service Analysis Img1.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/80b089d2-82b3-4289-9c43-0d5206752cea)
![Emergeny Service Analysis Img2.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/3964287a-082d-4e2b-a266-bea52254cb13)
![Emergeny Service Analysis Img3.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/966c197d-a20a-4535-88aa-9d6806291bab)
![Emergeny Service Analysis Img4.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/a661b4d3-ea44-4bfb-9301-a650f3741f30)

</details>

<details>
  <summary>Data Model</summary>

![Emergency Service Analysis data model.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/feb5df30-4a97-4def-879e-6e6a4721b87a)

</details>

<details>
  <summary>Calculations</summary>
  
  | MEASURE_NAME                          | EXPRESSION                                                 |
|---------------------------------------|------------------------------------------------------------|
| Hospital Capacity                     | SUM ( dimHospital[Capacity] )                              |
| No of Calls                           | COUNTROWS ( CallTimings )                                  |
| Hospital Name                         | SELECTEDVALUE ( dimHospital[Hospital Name] )               |
| Min Call Time                         | MIN (CallTimings[Length of Call (Mins)] )                  |
| Max Call Time                         | MAX( (CallTimings[Length of Call (Mins)] ))                |
| Average Dispatch Time (ADT)           | AVERAGE ( CallTimings[Average Dispatch Time] )             |
| Min Date                              | FORMAT ( MIN ( DateTable[Date] ), "dd/mm/yyyy" )           |
| Max Date                              | FORMAT ( MAX ( DateTable[Date] ), "dd/mm/yyyy" )           |
| Female Calls                          | CALCULATE ( [No of Calls], dimPatient[Gender] = "Female" ) |
| Male Calls                            | CALCULATE ( [No of Calls], dimPatient[Gender] = "Male" )   |
| Average Ambulance Arrival Time (AAAT) | AVERAGE ( CallTimings[Average Ambulance Arrival Time] )    |
| Average Hospital Arrival Time (AHAT)  | AVERAGE ( CallTimings[Average Hospital Arrival Time] )     |
| Patient Handover Time (PHT)           | AVERAGE ( CallTimings[Average Hospital Handover Time] )    |
| Average Handling Time (AHT)           | Average ( CallTimings[Length of Call (Mins)] )             |

</details>


## [Hotel Revenue](https://app.powerbi.com/view?r=eyJrIjoiZmE4N2Q0Y2ItMmE0Yi00YTBiLTg0ZjItOTA1N2YzYThkZDcxIiwidCI6ImJjMjQxODZjLTc0NzUtNGM2ZS05NThhLTg4MmMzYTZiOWIwYSIsImMiOjJ9)

This is a completely random and anonymised data set

Analysis done through this dashboard 

* Time analysis exploration (Seasonality, Festive periods, weekday vs weekend etc)

* Agent’s performance, overview.

* Other insights providing further information on Customers type (family with children, single or couples visitors) etc.

<details>
  <summary>Report Snapshots</summary>
  
![Hotel Revenue img1.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/4e885ccd-c36b-456e-b116-582950eefdb2)![Hotel Revenue img2.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/c9228710-ed83-4b79-bb04-4514a0b8ccc4)![Hotel Revenue img3.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/4e560ae1-f84b-45fd-95aa-ef000b3c7414)![Hotel Revenue img4.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/37b84f44-d6e9-4d6c-98d4-d9a5a3fc6f75)  

</details>

<details>
  <summary>Data Model</summary>
  
![Hotel Revenue Datamodel.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/8c188e20-56ba-43e4-ad3c-6ad44db9c38a)

</details>

<details>
  <summary>Calculations</summary>
  
| Name                        | Expression                                                                                                                                                                                                                               |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Record Count                | COUNTROWS( 'fct_Hotel Revenue' )                                                                                                                                                                                                         |
| Min Date                    | MIN( 'fct_Hotel Revenue'[Reservation Status Date] )                                                                                                                                                                                      |
| Max Date                    | MAX( 'fct_Hotel Revenue'[Reservation Status Date] )                                                                                                                                                                                      |
| Rev Rooms (Expected)        | SUMX( 'fct_Hotel Revenue', 'fct_Hotel Revenue'[AVG Daily Rate] * 'fct_Hotel Revenue'[Nights (Tot)])                                                                                                                                      |
| Rev Meals (Expected)        | SUMX( 'fct_Hotel Revenue', 'fct_Hotel Revenue'[Meal Cost])                                                                                                                                                                               |
| Total Revenue               | [Rev Meals (Actual)] + [Rev Rooms (Actual)]                                                                                                                                                                                              |
| Total Nights Booked         | sumx( 'fct_Hotel Revenue', 'fct_Hotel Revenue'[Nights (Tot)])                                                                                                                                                                            |
| Total Nights Stayed         | CALCULATE( [Total Nights Booked] , FILTER( 'dim_Reservation Status', 'dim_Reservation Status'[Reservation Satus] = "Check-Out"))                                                                                                         |
| % Cancellations/No Shows    | ( [Total Nights Booked] - [Total Nights Stayed] ) / [Total Nights Booked]                                                                                                                                                                |
| Rev Rooms (Actual)          | CALCULATE( [Rev Rooms (Expected)] , FILTER( 'fct_Hotel Revenue', OR( 'fct_Hotel Revenue'[Reservation Status Key] = 2 , 'fct_Hotel Revenue'[Deposit Type Key] = 2 )))                                                                     |
| Rev Meals (Actual)          | CALCULATE( [Rev Meals (Expected)] , FILTER( 'fct_Hotel Revenue', OR( 'fct_Hotel Revenue'[Reservation Status Key] = 2 , 'fct_Hotel Revenue'[Deposit Type Key] = 2 )))                                                                     |
| Total Expected Revenue      | [Rev Meals (Expected)] + [Rev Rooms (Expected)]                                                                                                                                                                                          |
| % Revenue Actual/Expected   | [Total Revenue] / [Total Expected Revenue]                                                                                                                                                                                               |
| Revenue Wkly Moving Avg     | VAR LastWeek =      MAX( )                                                                                                                                                                                                               |
| Check-Ins                   | CALCULATE( [Record Count] , FILTER( 'dim_Reservation Status', 'dim_Reservation Status'[Reservation Satus] = "Check-Out"))                                                                                                                |
| Total Guests                | CALCULATE( SUMX('fct_Hotel Revenue', 'fct_Hotel Revenue'[Adults] + 'fct_Hotel Revenue'[Babies] + 'fct_Hotel Revenue'[Children] ), FILTER( 'dim_Reservation Status', 'dim_Reservation Status'[Reservation Satus] = "Check-Out"))          |
| Average Daily Rate          | DIVIDE(      SUMX( 'fct_Hotel Revenue', 'fct_Hotel Revenue'[AVG Daily Rate] * 'fct_Hotel Revenue'[Nights (Tot)] ) ,     sumx( 'fct_Hotel Revenue', 'fct_Hotel Revenue'[Nights (Tot)] ) )                                                 |
| % Rev from Meals            | DIVIDE( [Rev Meals (Actual)] , [Total Revenue])                                                                                                                                                                                          |
| Revenue 1W Moving Avg       | AVERAGEX( DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -7, DAY), [Total Revenue])                                                                                                                                                |
| Cancellations 1W Moving Avg | averageX(DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -7, DAY), ( [Total Nights Booked] - [Total Nights Stayed] ) / [Total Nights Booked] )                                                                                      |
| Bookings 1Wk Moving Tot     | SUMX(     DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -7, DAY),      [Total Nights Booked]     )                                                                                                                                |
| Cancellations 1M Moving Avg | VAR tot = sumX(DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -1, MONTH), [Total Nights Booked] ) VAR stay = SUMX( DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -1, MONTH), [Total Nights Stayed] )  RETURN (tot-stay)/tot |
| Check-Ins 1W Moving Avg     | AVERAGEX( DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -7, DAY), [Check-Ins])                                                                                                                                                    |
| Guests 1W Moving Avg        | AVERAGEX( DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -7, DAY), [Total Guests])                                                                                                                                                 |
| Daily Rate 1W Moving Avg    | averageX(DATESINPERIOD( Dates[Date], LASTDATE( Dates[Date] ), -7, DAY), [Average Daily Rate] )                                                                                                                                           |

</details>

## [Executive Sales Report](https://app.powerbi.com/view?r=eyJrIjoiOWY2NDY1YmYtODkzMS00MzE1LWFlMjQtOGUxNzI1MzlmODRlIiwidCI6ImJjMjQxODZjLTc0NzUtNGM2ZS05NThhLTg4MmMzYTZiOWIwYSIsImMiOjJ9)

This is a completely random and anonymised data set

Analysis done through this dashboard 

* Sales trends
* Cumulative Sales
* 7 day Moving Average
* Sales by Channel
* Sales by Sales teams
* Sales by Region and State

<details>
  <summary>Report Snapshots</summary>
  
  ![Executive Sales Report img1.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/be2a3f0c-3f81-4ecb-a480-555dad503446)![Executive Sales Report img2.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/985e4b43-cf76-44ab-bed4-2436ab8b8bcf)![Executive Sales Report img3.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/aafccd70-6060-4d18-9148-1273b973eb4e)
  
</details>

<details>
  <summary>Data Model</summary>
  
![Executive Sales Report Data Model.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/5fe4bcf0-23c3-4a33-ab86-d99c50c0b509)

</details>

<details>
  <summary>Calculations</summary>
  
 | MEASURE_NAME               | EXPRESSION                                                                                                                       |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| Total Sales                | SUMX( Sales , Sales[Unit Price] * Sales[Order Quantity] )                                                                        |
| Total Quantity Sold        | SUM( Sales[Order Quantity] )                                                                                                     |
| Total Products Bought      | DISTINCTCOUNT(Sales[Product Index])                                                                                              |
| Total Costs                | SUMX( Sales , Sales[Unit Cost] * Sales[Order Quantity] )                                                                         |
| Average Costs              | AVERAGEX( Sales , Sales[Unit Cost] * Sales[Order Quantity] )                                                                     |
| Average Sales              | AVERAGEX( Sales , Sales[Unit Price] * Sales[Order Quantity] )                                                                    |
| Total Profits              | [Total Sales] - [Total Costs]                                                                                                    |
| Profit Margin              | DIVIDE( [Total Profits] , [Total Sales] , 0 )                                                                                    |
| Total Transactions         | COUNTROWS( Sales )                                                                                                               |
| Top 10 Cities by Profit    | CALCULATE( [Total Profits] ,         FILTER( 'Store Locations' ,                  'Store Locations'[Top N Cities] = "Top 10" ) ) |
| Prev. Month Sales          | CALCULATE( [Total Sales] , DATEADD( Dates[Date] , -1 , MONTH ) )                                                                 |
| Prev. Month Qty. Sold      | CALCULATE( [Total Quantity Sold] , DATEADD( Dates[Date] , -1 , MONTH ) )                                                         |
| Sales Target               | [Prev. Month Sales] * 1.1                                                                                                        |
| Quantity Sold Target       | [Prev. Month Qty. Sold] * 1.1                                                                                                    |
| Avg. Retail Price          | AVERAGE( Sales[Unit Price] )                                                                                                     |
| Adjusted Retail Price      | [Avg. Retail Price] * (1 + 'Price Adjustment (%)'[Price Adjustment (%) Value] )                                                  |
| Adjusted Sales             | SUMX( Sales , [Adjusted Retail Price] * Sales[Order Quantity] )                                                                  |
| Adjusted Profit            | [Adjusted Sales] - [Total Costs]                                                                                                 |
| % of Total Sales           | DIVIDE( [Total Sales] ,          CALCULATE( [Total Sales] , ALL( Products[Product Name] ) ), 0 )                                 |
| Price Adjustment (%) Value | SELECTEDVALUE('Price Adjustment (%)'[Price Adjustment (%)], 0)                                                                   |
  
 </details>

## [Consultancy Time and Earnings Analysis](https://app.powerbi.com/view?r=eyJrIjoiMzA0ODRhOWYtYmEwYS00NjBmLWE2NDEtOWExZWU3MDgwZjhkIiwidCI6ImJjMjQxODZjLTc0NzUtNGM2ZS05NThhLTg4MmMzYTZiOWIwYSIsImMiOjJ9)

This is a completely random and anonymised data set

Analysis done through this dashboard 

* How many productive hours doyou work in a week?

* How many should you be doing

* How many hours am I doing on a particular project

* How effective is the resource? How is it performing?

* Utilization 

<details>
  <summary>Report Snapshots</summary>
  
![Consultancy Time and Earnings Analysis img1.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/10763351-8d2f-478d-92f5-14c824178d76)![Consultancy Time and Earnings Analysis img2.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/a2fcb230-fa56-4cb9-89bb-4888502edc32)![Consultancy Time and Earnings Analysis img3.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/f5ccc624-d3df-4cb9-b790-e69fba70778c)

</details>

<details>
  <summary>Data Model</summary>
  
![Consultancy Time and Earnings Analysis Data Model.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/725c58e1-e89f-4081-8d39-fd5137ecc2aa)

</details>

<details>
  <summary>Calculations</summary>
  
| MEASURE_NAME                             | EXPRESSION                                                                                                                                                                                                                                  |
|------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| __Default measure                        | 1                                                                                                                                                                                                                                           |
| Duration Daily Average                   | AVERAGEX('Date', [Duration Sum])                                                                                                                                                                                                            |
| Duration Hour Minute                     | VAR _Hour = HOUR( SELECTEDVALUE( atWorkData[Duration]) )  // Find minute as proportion of hour VAR _Minute = DIVIDE(MINUTE( SELECTEDVALUE( atWorkData[Duration] ) ), 60, 0 )  // Add together VAR _Result = _Hour + _Minute  RETURN _Result |
| Duration Sum                             | SUM(atWorkData[Duration])                                                                                                                                                                                                                   |
| Total Business Hours                     | [Business Days] * 7.5                                                                                                                                                                                                                       |
| Total Earnings                           | SUM(atWorkData[Earnings, $])                                                                                                                                                                                                                |
| Total Number of Fiscal Months            | DISTINCTCOUNT( atWorkData[Year] ) * 12                                                                                                                                                                                                      |
| Total Billed Hours                       | SUM ( atWorkData[Hours Billed] )                                                                                                                                                                                                            |
| Business Days                            | CALCULATE( COUNT( 'Date'[Date] ) , 'Date'[IsBusinessDay] = TRUE() )                                                                                                                                                                         |
| Working Days                             | DISTINCTCOUNT( atWorkData[Start] )                                                                                                                                                                                                          |
| Number of Months Worked                  | DISTINCTCOUNT( atWorkData[YYYY-MM] )                                                                                                                                                                                                        |
| Non Working Business Days                | [Business Days] - [Working Days]                                                                                                                                                                                                            |
| Total Non Working Fiscal Months          | [Total Number of Fiscal Months] - [Number of Months Worked]                                                                                                                                                                                 |
| Non Working Business Hours               | [Total Business Hours] - [Total Billed Hours]                                                                                                                                                                                               |
| Monthly Avg. Hours Billed                | AVERAGEX (      VALUES ( 'Date'[Month & Year] ),     [Total Billed Hours] )                                                                                                                                                                 |
| Monthly Avg. Business Hours              | AVERAGEX (      VALUES ( 'Date'[Month & Year] ),     [Total Business Hours] )                                                                                                                                                               |
| Project Count                            | DISTINCTCOUNT( atWorkData[Project] )                                                                                                                                                                                                        |
| Client Count                             | DISTINCTCOUNT( atWorkData[Client] )                                                                                                                                                                                                         |
| Task Count                               | DISTINCTCOUNT( atWorkData[Task] )                                                                                                                                                                                                           |
| Monthly Avg. Earnings                    | AVERAGEX (      VALUES( 'Date'[Month & Year] ),     [Total Earnings] )                                                                                                                                                                      |
| Hourly Billed Rate                       | DIVIDE( [Total Earnings] , [Total Billed Hours] )                                                                                                                                                                                           |
| Weekly Avg. Hours Billed                 | AVERAGEX(      VALUES( 'Date'[Week & Year] ),     [Total Billed Hours] )                                                                                                                                                                    |
| Total Working Hours                      | [Working Days] * 7.5                                                                                                                                                                                                                        |
| Working Hours vs Billed Hours            | [Total Billed Hours] - [Total Working Hours]                                                                                                                                                                                                |
| Weekly Avg. Working Hours                | AVERAGEX(      VALUES( 'Date'[Week & Year] ),     [Total Working Hours] )                                                                                                                                                                   |
| Working vs Business Hours                | IF( [Total Working Hours] < [Total Business Hours],     "Under Utilized Hours : " & [Total Business Hours] - [Total Working Hours],     " Over Time Hours : " & [Total Working Hours] - [Total Business Hours] )                            |
| Weekly Avg. Earnings                     | AVERAGEX (      VALUES( 'Date'[Week & Year] ),     [Total Earnings] )                                                                                                                                                                       |
| Business Days without Work %             | DIVIDE( [Non Working Business Days] , [Business Days] )                                                                                                                                                                                     |
| Months Without Work %                    | DIVIDE( [Total Non Working Fiscal Months] , [Total Number of Fiscal Months] )                                                                                                                                                               |
| Hours without Work %                     | DIVIDE( [Non Working Business Hours], [Total Business Hours] )                                                                                                                                                                              |
| Utilization %  \| Business Hours         | DIVIDE(  [Total Billed Hours] , [Total Business Hours] )                                                                                                                                                                                    |
| Monthly Avg. Utilization %               | DIVIDE ( [Monthly Avg. Hours Billed] , [Monthly Avg. Business Hours] )                                                                                                                                                                      |
| Utilization % \| Working Hours           | DIVIDE(  [Total Billed Hours] , [Total Working Hours] )                                                                                                                                                                                     |
| Weekly Avg. Utilization % (Working Days) | DIVIDE ( [Weekly Avg. Hours Billed] , [Weekly Avg. Working Hours] )                                                                                                                                                                         |
| Working Hours vs Billed Hours %          | [Working Hours vs Billed Hours] / [Total Working Hours]                                                                                                                                                                                     |
| Monthly Earning Tooltip Title            | Var SelectedFY = Selectedvalue( 'Date'[Fiscal Year] ) Return " Monthly Earnings \| For : " & SelectedFY                                                                                                                                     |
| Month & Year                             | Var SelectedMonthNYear = Selectedvalue( 'Date'[Month & Year] ) Return SelectedMonthNYear                                                                                                                                                    |
| Tooltip Target                           | Var SelectedTarget = Selectedvalue( 'Utilization Target'[Target] ) Return SelectedTarget                                                                                                                                                    |

</details>

## [Purchase Order Analysis](https://app.powerbi.com/view?r=eyJrIjoiYWI1YWU4ZDMtZTEzZS00OTZlLTg0ZGYtNjg5NDdkOTcyYmMzIiwidCI6ImJjMjQxODZjLTc0NzUtNGM2ZS05NThhLTg4MmMzYTZiOWIwYSIsImMiOjJ9)

<details>
  <summary>Report Snapshots</summary>
  
![Purchase Order Analysis img.png](https://images.zenhubusercontent.com/6345b946a9dc402ad81927d2/859fc663-1135-4c84-b983-4f8a70c2c2b3)

</details>


## [Sales Analysis](https://app.powerbi.com/view?r=eyJrIjoiOWM1YTQ4NmQtOTExNC00ZTMwLWFjZjgtZjEwNWFiNmYwYmZhIiwidCI6ImJjMjQxODZjLTc0NzUtNGM2ZS05NThhLTg4MmMzYTZiOWIwYSIsImMiOjJ9)
## [Call Center Analysis](https://app.powerbi.com/view?r=eyJrIjoiNjc0OWY2MWEtOTU4OS00MTM4LThkNTgtZmEyM2VlNWRlM2IyIiwidCI6ImJjMjQxODZjLTc0NzUtNGM2ZS05NThhLTg4MmMzYTZiOWIwYSIsImMiOjJ9)


