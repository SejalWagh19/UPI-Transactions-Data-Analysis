# UPI Transactions Data Analysis
### Dashboard Link : https://app.powerbi.com/links/ABMZYiQeEg?ctid=5a5d61c5-3c5e-430a-bc70-0208cda85604&pbi_source=linkShare&bookmarkGuid=8fe0db16-70e1-46c0-a173-b9aaa503cf58

## Problem Statement
This report helps to understand customer transaction behaviour on the UPI platform. It helps them see how transaction volumes and amounts change each month and how they differ across various cities and currencies. Through different filters, they can identify specific spending habits and popular services, allowing them to pinpoint areas for growth and targeted marketing.

Since transaction amounts show significant dips in certain time periods, while some geographical areas show consistently high-value transactions, businesses must investigate the reasons for these fluctuations. By using this report, they can identify these patterns and work on strategies to stabilize transaction volumes or launch targeted campaigns in high-performing regions to maximize engagement.

### Steps followed 

- Step 1 : Import the data into Power BI Desktop and transform; dataset is a excel file.
- Step 2 : Open the power query editor and in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options for entire dataset.
- Step 3 : Split the Transaction Time column by a delimiter (space) to separate it into Date and Time. 
  Remove the redundant Time column, as this information is already captured.
- Step 4 : Change the data type for CustomerAccountNumber and MerchantAccountNumber columns from exponent to text. Close and Apply Changes to the Power Query Editor.
- Step 5 : Add a slicer and set its Height=80px and Width=232px. Maintain a 20px distance between adjacent slicers for a clean layout.
- Step 6 : Create Calculated Column 'Age Group' Column. DAX formula to create the Age Group column: <br>
```
  Age Groups = 
  IF(
      'UPI Transactions'[CustomerAge]<=25, "A1", 
      IF(
          'UPI Transactions'[CustomerAge]<=35, "A2", 
          "A3"
      )
  )
```
- Step 7 : Add 10 slicers to the report page. Assign a different categorical column from the dataset to each slicer (BankNameSent, BankNameReceived, City, DeviceType, Age Groups, MerchantName, PaymentMethod, Purpose, TransactionType).
- Step 8 : Duplicate Page: Right-click on the report page tab and select Duplicate Page.
- Step 9 : On Page 1, Add a Line Chart:
  - X-axis: Drag the Transaction Date column.
  - Y-axis: Drag the Amount column.
  - Title the chart: Transaction by Month [Line] (Year 2024).

- Step 10 : The transaction data includes multiple currencies like Rupees, Dollars, and Euros, simply adding all the amounts together would give a misleading and incorrect total.
  - To solve this, drag and drop the currency column to filter on all pages under Filters pane.
  - This allows you to select just one currency at a time, for example, "INR". When you do that, all the charts and tables in the report will instantly update to show only the transactions that happened in Indian Rupees. This ensures the numbers you are seeing are accurate and make sense.
  - Furthermore, this currency filter works across both views of your report at the same time. This means if you select "USD" on the first view with the charts, the second view with the detailed table will automatically be filtered for US Dollars as well, so you don't have to apply the same filter twice.

- Step 11 : Adding a Matrix Visual. Configure the matrix to analyze transaction details: <br>
  - `Rows: Month, City` <br>
  - `Columns: Currency` <br>
  - `Values: Sum of Amount, Sum of Remaining Balance`

- Step 12 : To make the slicer(s) option when chosen apply to all pages, select the slicer, go to the View tab, and click Sync slicers. The Sync slicers pane will appear.
  - For each of the 10 slicers on Page 1, ensure the checkbox under the "sync" icon is checked for both Page 1 and Page 2.
  - This ensures that any filter selection made on one page is automatically applied to the corresponding slicer on the other page.

- Step 13 : Conditional Formatting <br>
  - Select the Matrix visual. The amounts represented on the matrix visual, we want to represent the background color for different amounts.
  - The higher amounts should be represented by a darker background color and lower amounts by a lighter color.
  - From format visual under cell elements apply background color for the columns.

- Step 14 : Implementing Bookmarks for Chart Switching <br>
  - On Page 1, create a 2nd - column chart: Copy and paste the existing line chart.
  - Place the copy directly on top of the original.
  - With the new chart selected, change its type to a column chart.

- Step 15 : Configure Bookmarks <br>
  - Go to the View tab and open the Bookmarks and Selection panes. <br>
  - In the Selection pane, hide the column chart and show the line chart. <br>
  - In the Bookmarks pane, click Add and rename the bookmark to Line Chart Amounts. Click the three dots and ensure Data is unchecked, then click Update.

- Step 16 : Now, hide the line chart and show the column chart. Add another bookmark, rename it to Column Chart Amounts, uncheck Data, and click Update.

- Step 17 : Add Bookmark Navigator:
  - Go to the Insert tab. Click Buttons > Navigator > Bookmark Navigator.
  - This will add buttons to the canvas that allow users to easily switch between the Line Chart View and Column Chart View.

- Step 18 : Repeat the same steps for the RemainingBalance column.
  - Create a new set of charts (Line & Column) on Page 1 and place it on the top of the existing ones.
  - Create new bookmarks, rename it, uncheck data and click update.  
  - This helps to visualize how the remaining balance changes over time.
