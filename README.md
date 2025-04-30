# Business_Performance_Analysis


## Problem Statement

This Power BI dashboard enables Plant Co. to monitor and analyze sales,Gross Profit, Quantity and profitability performance across different countries, time periods, and product types. It is designed to support strategic decisions by identifying underperforming regions, assessing product performance trends, and evaluating account-level profitability through key metrics like YTD Sales, PYTD Sales, GP%, and Segment-wise Contributions.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.

- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

- Step 3 : Remove duplicates and filter null values that could affect analysis.

- Step 4 : Built a star schema of Fact table Sales, DimAccount, DimProduct.

- Step 5 : Created Calender table as DimDate.

- Step 6 : Created _Measures table where seveal reguired in one table that are:
     ##### Base Measures
        Sales = SUM(Fact_Sales[Sales_USD])
  
        Quantity = SUM(Fact_Sales[quantity]
  
        Gross_Profit = [Sales]-[COGs]
  
        COGs = SUM(Fact_Sales[COGS_USD])

        GP% = DIVIDE([Gross_Profit],[Sales])

- Step 7 : Created previous year time to date measures for each values in one table that are:
     ##### PYTD Measures
           Same is done for year to date (YTD) measures.
           PYTD_Sales = 
                  CALCULATE(
                      [Sales],
                      SAMEPERIODLASTYEAR(Dim_Date[Date]),
                      Dim_Date[Inpast] = TRUE
                  )

          PYTD_Quantity = 
                  CALCULATE(
                      [Quantity],
                      SAMEPERIODLASTYEAR(Dim_Date[Date]),
                      Dim_Date[Inpast] = TRUE
                  )

         PYTD_GrossProfit = 
                  CALCULATE(
                      [Gross_Profit],
                      SAMEPERIODLASTYEAR(Dim_Date[Date]),
                      Dim_Date[Inpast] = TRUE
                  )


- Step 8 : Created Switch table for measures like:
  
                    S_PYTD = 
                          VAR selected_value = SELECTEDVALUE(Slc_Values[Values])
                          VAR result = SWITCH(selected_value,
                              "Sales", [PYTD_Sales],
                              "Quantity", [PYTD_Quantity],
                              "Gross Profit", [PYTD_GrossProfit],
                              BLANK()
                          )
                              RETURN
                              result

                    S_YTD = 
                        VAR selected_value = SELECTEDVALUE(Slc_Values[Values])
                        VAR result = SWITCH(selected_value,
                            "Sales", [YTD_Sales],
                            "Quantity", [YTD_Quantity],
                            "Gross Profit", [YTD_GrossProfit],
                            BLANK()
                        )
                            RETURN
                            result

                  YTD vs PYTD = [S_YTD]-[S_PYTD]

  

- Step 9 : Created table of slicer values Profit, Gross Profit, Quantity.
  
  ![Image](https://github.com/user-attachments/assets/d7e7d9c9-db5e-4702-8d89-d4d92e0d7424)

  

- Step 10 : A "Tree Map' for Bottom 10 YTD vs PYTD by Country.
  
    ![Image](https://github.com/user-attachments/assets/01707f4d-012e-4461-bfb4-5e6a0f32f092)






  
- Step 11 : A "Waterfall chart" is created for YTD vs PYTD | Month-country-Product for slicer values.

   ![Image](https://github.com/user-attachments/assets/dab0c346-dba2-4364-9151-9dfa9acd9637)



- Step 12 : Created A stacked column chart for monthly YTD & PYTD with respect to slicer values.
  


- Step 13 : A Scatter plot is created showcasing account profitability segmentation by GP% & slicer values.

  ![Image](https://github.com/user-attachments/assets/2d24042e-29c5-43bc-b130-a8b18174ce66)



- Step 14 : Created key KPI's that are:

  
   ![Image](https://github.com/user-attachments/assets/940f40e8-05ef-44af-af52-787b81f6b5e0)

        
- Step 15 : Conditional formatted the KPI's and overrall formatted the dashboard for better visualization.

 Snap of dashboard
 
  ![Image](https://github.com/user-attachments/assets/dd976b0e-a359-477d-8a7b-c62075cc90a4)

 


# Insights

A single page report was created on Power BI.

Following inferences can be drawn from the dashboard;

### [1] Sales Trend

    a) YTD Sales are $512K lower than PYTD.
    b) Strong performance in April–June, but steep drops in August and December..
    

           
### [2] Country Performance

    a) China had the largest negative YTD vs PYTD delta (~$760K).
    b) Most bottom contributors were from Europe & Asia (Sweden, France, Norway,etc.)
   
   
  
### [3] Product Type Analysis
  
    a) Indoor and Landscape products consistently contributed to high monthly sales.
    b) Monthly peaks observed in March, April, and October.
    
### [3] Customer Analysis 
  
    a) It is almost same as Sales for Quantity and Gross Profit for customers.
    b) Most customers are above 40% GP%.




     
 
 
