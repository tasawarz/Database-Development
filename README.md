# Database-Development-SSIS-SQL
**Prototype Development of Home Office Payments Data Warehouse**

**Project Overview:**
This project involves the prototype development of a data warehouse using Home Office payments data. The goal is to create a robust database that facilitates easy analysis and visualization of spending patterns. The tools utilized for this project are Visual Paradigm for designing the star schema, SQL Server Integration Services (SSIS) for Extract, Transform, Load (ETL) operations, and Tableau for data visualization.

**Data Source:**
The dataset used for this project is sourced from the Home Office official website. It contains payment information made to suppliers during the financial year from April 2017 to March 2018. The data includes attributes like Department, Entity, Date, Expense Type, Expense Area, Supplier Name, Transaction Number, and Spend (with refunds represented as negative payments).

**Data Preparation:**
The dataset was downloaded as 12 separate files, one for each month from April 2017 to March 2018. The key attributes include Department, Entity, Date, Expense Type, Expense Area, Supplier Name, Transaction Number, and Spend. The Department contains only one entry, which is "Home Office." The Entity is divided into "DBS - Disclosure & Barring Service" and "Home Office," each having separate expense areas, types, and suppliers.

**Star Schema:**
The star schema designed for the dataset consists of five dimensions: Date, Department, Entity, Expense Type, and Supplier. The Fact table named "Spending" sits at the center and contains six measures: Spend and Foreign Key IDs for all dimensions. Additional attributes like Month and Quarter were added to the Date dimension to support specific analysis tasks.

![image](https://github.com/tasawarz/Database-Development/assets/119436229/dec3c28b-ab21-4b0b-86d0-1472701201bf)


**Data Loading (ETL):**
SQL Server Integration Services (SSIS) was employed for the ETL process. A "Foreach Loop Container" was utilized to load all 12 separate files simultaneously. A "Script Task" was added within the loop to display the name of the loaded file. The data was then transformed using a "Data Flow Task" named "Merging," which involved importing data from spreadsheets into tables. The Excel Source was connected to the OLE DB Destination with the help of an Excel Connection Manager.

![image](https://github.com/tasawarz/Database-Development/assets/119436229/0a02a49d-e494-44cc-9822-afd43d9df01b)


**Dimensions:**
In the dimension data flow, the "OLE DB Source" retrieves data, which is then passed through the "Multicast" transformation to create logical copies. These copies are used to apply various transformations for creating each dimension. The derived column transformation was used to extract Month and Quarter attributes in the Date dimension. Surrogate Keys were added to each destination table to uniquely identify dimension records.

![image](https://github.com/tasawarz/Database-Development/assets/119436229/f1912961-096f-41bb-ac81-8babe66165ea)

**Fact Table:**
In the fact table data flow, the "OLE DB Source" retrieves data from the existing dimension tables, and the "Lookup" transformation is used to map surrogate keys to each dimension. The data is then loaded into the Fact table using the "OLE DB Destination."

![image](https://github.com/tasawarz/Database-Development/assets/119436229/369b5455-9369-45d1-80e7-672a0deb8387)

**Analysis:**
Several SQL queries were formulated to answer specific questions related to the dataset. These queries include finding top payment types, expense areas, suppliers, and spending patterns over various quarters and months for both entities.

Query 1:

![image](https://github.com/tasawarz/Database-Development/assets/119436229/63f1e2c2-30b5-4597-8c8c-838fc16294fc)

Query 1 Output:

![image](https://github.com/tasawarz/Database-Development/assets/119436229/daa114d7-ded8-45fb-a38b-108a6a5aa5e8)

Query 2:

![image](https://github.com/tasawarz/Database-Development/assets/119436229/14476b51-ca8b-4cd9-bdb2-b6a268a1623b)

Query 2 Output:

![image](https://github.com/tasawarz/Database-Development/assets/119436229/0ab5924e-7dfd-4a5b-b898-e8bdb6ce44c3)

Query 3:

![image](https://github.com/tasawarz/Database-Development/assets/119436229/9a589b51-0e84-4252-a2fc-948609b44e81)

Query 3 Output:

![image](https://github.com/tasawarz/Database-Development/assets/119436229/5c71c63f-05bd-4425-a3cc-39a7a4ffcb44)

**Visualization:**
Tableau was used to visualize the results of the SQL queries. Dashboards and graphs were created to provide clear insights into spending trends and patterns. The visualizations include top expense types per quarter, top suppliers per quarter, top expense areas by year and half years, and total spend by entity over each month and quarter.

![image](https://github.com/tasawarz/Database-Development/assets/119436229/c13a1298-b95d-4cd3-9460-7a756f7b78b0)

The first graph i.e., Top 3 Expense Type per Quarter gives us insights about the three most demanding expense types. For Q1 Grant, IT, Telecomms Run Cost, and FM Services are the top 3 expense types. The filter below the graph can be used to visualize the other quarters. 

The second graph i.e., Top 10 Supplier per Quarter, it is observed that for all the quarters Greater London Authority (G) is the major account that’s taken the highest expenses. The graph below includes all the quarters; however, the quarters can be visualized separately using the filter on the right.

The third graph i.e., the Top 4 ExpArea by Year and HalfYears shows four top Expense areas i.e., CPFG - Crime Policing & Fire Group, DDaT - Digital Data & Technology, UKVI - UK Visas & Immigration, HMPO - Her Majesty's Passport Office. The first half is represented by Orange color, the second half by Red, and Spendingbyyear by Blue. The amount for CPFG - Crime Policing & Fire Group goes much higher as compared to other expense areas, it goes beyond 10B per year while for the other fields, it remains under a billion. 

The fourth graph i.e., the Total Spend by Entity over each month and quarter gives us insights about the top expense type account under each entity over each month and quarter. It is seen that Home Office is spending most of the money on grants, while DBS – Disclosure and Barring Services spends most on Business Processes and Outsourcing. The filters on the right will let you choose to visualize the spending by expense type and entity over the months.


**Conclusion:**
This prototype development of the Home Office payments data warehouse successfully showcases how data can be extracted, transformed, and loaded into a star schema using SSIS. Tableau's visualization capabilities help in understanding spending patterns and making informed decisions. The resulting data warehouse serves as a powerful analytical tool for further exploration and decision-making purposes.
