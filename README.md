# Debtors Dashboard
### Problem Statement
This dashboard is designed to track and manage outstanding invoices and collections effectively. It provides insights into the outstanding amounts, days overdue, and overall collection efficiency. The goal is to optimize the debt recovery process and maintain healthy cash flow by closely monitoring these key metrics.

### Data Used:-
The project involves the following tables:

* Collection Table: Includes columns like Amount, Client Name, Collection Date, COLLECTION DAYS, Invoice Date, Invoice No., Receipt No., Sectors.
* Invoices Table: Contains columns such as Amount, Client Name, Invoice Date, Invoice No., Sectors, State.
* Currency Table(Created by writing DAX): Includes Conversion Factor, Sort Order, Unit, and Unit Format.
* Outstanding Amount: Derived table with fields such as Amount, Client Name, Collection/Credit Note Amount, Invoice Date, Invoice No., Outstanding Amount, Sectors, State, years in bins.
* TOPN 10 RECORDS(Created by writing DAX): Focuses on Amount, Client Name, Collection/Credit Note Amount, Invoice Date, Invoice No., Sectors, State, years in bins.
* Financial Calendar(Created by writing DAX): Contains Financial Month, Financial QTR, Financial Year, Invoice Date, and MONTH.
### Steps :-

#### Step 1: Data Preparation and Extraction
I began by opening Power BI Desktop and imported the relevant data tables from an Excel sheet. Specifically, I extracted the Invoice and Collection tables into the Power BI Query Editor.

#### Step 2: Data Modeling and Relationships
* I edited the data model by renaming fields to ensure consistency:

     * In the Collection Table: Renamed ‘Against Invoice No’ to ‘Invoice No’ and ‘Collection YTD’ to ‘Amount’.
     * In the Invoice Table: Renamed ‘Billing YTD’ to ‘Amount’.
* As Power BI didn’t automatically build relationships between tables, I used the Power Query Editor to manually establish the necessary relationships.

#### Step 3: Credit Note Table Creation
* To manage credit notes, I duplicated the Invoice table and renamed the duplicate as the Credit Note Table. I then:

    * Added a condition in the Amount field where Amount is less than 0.
    * Converted the negative Amount values to positive by multiplying the column by -1.
#### Step 4: Invoice Table Adjustment
* I filtered the Invoice Table to retain only positive amounts, representing actual sales.

#### Step 5: Merging Tables
* I concatenated (appended) the Collection table with the Credit Note Table. I renamed the resulting table as ‘Union Collection and Credit Note,’ which allowed me to aggregate collection and credit note amounts for further analysis.

#### Step 6: Grouping and Aggregation
* In the Union Collection and Credit Note Table, I applied a 'Group By' operation on the Invoice No. field to sum up the collection and credit note amounts. This provided a comprehensive view of total collections against each invoice.

#### Step 7: Final Table and Calculations
* I performed a left join between the Invoice Table and the Union Collection and Credit Note on Invoice No. After the join, I replaced any null values in the Collection/Credit Note Amount field with 0. I then added a new column named Outstanding Amount, calculated by subtracting the Collection/Credit Note Amount from the Sales Amount.

#### Data visualizations
Outstanding Amount Calculation: Visualized the total outstanding amounts across different clients and invoices.
Bucketing Invoices: Categorized invoices based on the number of days they have been outstanding.
Invoices vs. Collections: Analyzed the invoices raised within a selected period against the collections made during that period etc.# Debtors-Power-BI-Dashboard
