# Stock-Analysis


## Overview
The motivation of this project is to analyze stocks in the green technology sector based upon 2 important metrics: annual trading volume and annual return. To accomplish this goal we used a data set that represented the daily trading metrics of 12 green-tech stocks and then aggregated this data in order to gain insight into yearly trends. This analysis was performed for 2017 and 2018 using VBA Macros.

## Results
## Analysis of Stock Prices
From the below tables we can clearly see that 2017 was a much better year for the green tech sector than 2018, as the average return clearly shows. However, average total daily volume remains constant. If we compare the volumes across both years we see that some stocks, such as DQ or VSLR, lost value but saw an increase in trading volume. At first this seems counter intuitive but by empolying economic analysis we see that a decrease in price and an increase in quantity traded (daily volume) can be attributed to an increase of supply to the market (see graphical analysis below). Using DQ as an example, we see that this means those who bought the stock in 2017 thought the 199.4% increase meant the stock was over-valued, in response these buyers began to sell their stock; as the market corrected for this overvaluation, the additional supply from these stock owners further depressed the price leading to the large loss that DQ suffered in 2018 (-62.6%). We also notice that a large piece of the overall trading volume is due to 2 stocks: EPPH and RUN. These two stocks outperformed by over an 80% margin and this is reflected in a high demand, which translates to a higer trading volume. If we look at ENPH for example we see that it had a 129.5% increase in return followed by a 81.9% increase in 2018, outperforming the market in both years. While at first glance this may seem to suggest that it is a good buy, it is actually not. This is for two reasons: regression to the mean, and that generally it is more advantagous to buy stocks which are undervalued. When looking for stocks to buy at the end of 2018 a stock like SPWR would make more sense as it trades with high volume and over both years lost %21.5 of its value. While we would like to further research a specific company before buying, it is unlikely that a company not only failed to grow but lost 21.5% of it's real value over 2 years; thus we can assume this is an overcorrection and the price will likely go up in 2019.

![2017_Analysis](./Resources/Analysis_2017.png) ![2018_Analysis](./Resources/Analysis_2018.png)

![Supply-Shifts-Right](./Resources/Supply-to-R.png)

## Analysis of Run-Time
When we compare the run-time of the original code and the refactored code (attached below) we see a significant improvement after refactoring. These translate to saving time by a factor of about 5.8 and 5.3 for 2017 and 2018, respectively. 

### Original Run-Times
![2017-original-rt](./Resources/Original_2017.png) ![2018-original-rt](./Resources/Original_2018.png)
### Refactored Run-Times
![2017-Refactored-rt](./Resources/VBA_Challenge_2017.png) ![2018-Refactored-rt](./Resources/VBA_Challenge_2018.png)

These time savings come from the fact the the code has been restructured such that it only loops through every row of the spread sheet instead of looping through every row, for each ticker symbol. This rum-time improvement has a cost in terms of memory usage but we will investigate this more throughly in the summary section along with how the time and space complexities scale with input size.

## Summary
In this section we will be using the concept of Big-O notation in order to describe the how the refactoring changed the time and space complexity of the original algorithm and how this translates to advantages, for the formal definition of Big-O notation we refer the reader to the [wikipedia article](https://en.wikipedia.org/wiki/Big_O_notation#Formal_definition) for a formal definiton. First we note that the number of rows is actually given by `251*n` where n is the number of tickers (confirmed using excel's `=COUNTIF()`). Since we are performing big-O analysis we can remove the constant and use the number of tickers to describe the input size of the data set, from here on we let it be `n`. Let's consider how the the refactored code and original code loop through the data as these are the code blocks which determine time complexity:
 
 ### Original Code
 ```vba
 Sub AllStocksAnalysis()
  tickerLoop = 11 'this is the number of tickers (n)
  rowLoop = Cells(Rows.Count, 1).End(xlUp).Row 'number of rows in the sheet or 251*n
  For i = 0 To tickerLoop
    'store the ticker symbol and activate the worksheet
    For j = 2 To rowLoop
      'calculate total volume and total daily return for the i-th ticker symbol
    Next j
   Next i
 ```

