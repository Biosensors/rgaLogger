# rgaLogger
RGA Logger
The RGA Logger has two features:
-	Keep track of the RGAs from between the customer’s location up to the warehouse
-	Show returns’ KPIs 
How to use it
RGA tab
When the file is opened, it loads the previous (from newest to oldest) 400 entries. All lined are blocked for editing and are only visible for viewing. In order to edit a line, the user must click on any cell within that line, then click on “Edit Row”. The status will change to “editing”, and the user can now edit all cells within that one line. As soon as the user leaves the row, all the information they have changed will be saved, and the status will change to “saved”.
“RGA Details” displays information about the line they’re currently on. Additional details include the list of all the products that are comprised with that RGA.
The “Load Data” button will allow for the user to refresh the current information. However, this is done automatically every 30 seconds.
As this display is constantly being updated, Excel’s filtering feature isn’t effective. Instead, the user may filter by clicking the “Filter” button in the top row. 
The user may click on “Now displaying [……]” in order to toggle between displaying the last 400 entries or display all the entries. As records are being kept since January 2014, displaying everything will take a lot of time, especially from remote sites, such as BBV.
Overview tab
Displays the equivalent of “RGA Details” (products, quantity, lot, etc.) for all of the RGAs listed in RGA.
Report tab
When opening this tab, some computation is done in order to generate the report. Cells B15 to G20 display a “Loading” sign while this is going on. This sign will disappear when done.
This tab is used to display KPIs based on the timing. This way, management can keep track of various timing information. The ones currently in place are:
Monthly count: number of returned created per month
Prod. Quantity per month: number or products logged per month
Open at CS: Of all the returned which are still open at CS, the month when they have been created
Open at WH:  Of all the returned which are still open at WH, the month when they have been created
Processed at WH: Of all the returned which were processed at WH, the month when they have been created
Note: when opening this tab, it generates the report based on what’s loaded in the “RGA” tab. In order to display a report for previous years, not just the last 400 entries, toggle the “Now displaying last 400” buttons in “RGA” then generate the report again.
Notes for developers
-	This file is only used to display information. All information is stored in the SQL server and is reloaded upon opening the file
-	When opening the file, only the last 400 entries are loaded, in an effort to reduce loading time, especially at BBV. This can be changed by toggling the “display” button in row 1
-	All lines are locked for editing. When clicking “edit row”, a value is set to “TRUE” in the SQL table, thus preventing any other user to edit the same row. Everytime such an operation is fired, a trigger is fired on the SQL table, which will scan for all lines having the “editing” field set to “TRUE” and looking at when was the last update on this entry. If it has been more than 30 minutes, it can be assumed that the line no longer needs to be locked and the “editing” field returns to “FALSE”. This has also been setup in order to counter some bug (it was noted in the past that when editing is done by the user, the “editing” field wouldn’t automatically bet set back to “FALSE” thus requesting the user to raise a ticket with IT – this would happen about once every three weeks).
-	The list of customers to be entered is pulled from the SQL table ZMM_SQL_CUS
Code / project source
\\mofasa.besa.bsi.corp\Shared\it\BESA\Peter's Projects\RGA Logger
