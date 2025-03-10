# Payment-Renewal-Automation-SQL-
Overview

This project involves updating and managing payment records for Dealing Member Firms (DMFs) and brokers. The dataset used is a sample dataset for demonstration purposes. The SQL operations performed aim to:

Track overdue payments.

Implement a late fee policy.

Calculate the total amount due for overdue payments.

Integrate email addresses to facilitate payment reminders.

SQL Operations Breakdown

Retrieve Data

SELECT * FROM [DMF and Brokers];

Fetches all records from the dataset.

Mark Overdue Payments

UPDATE [DMF and Brokers]
SET payment_status = 'Overdue'
WHERE payment_type = ('None');

Updates the payment_status column to 'Overdue' for firms with no recorded payment.

Add Late Fee Column

ALTER TABLE [DMF and Brokers]
ADD late_fee DECIMAL;

Introduces a new column late_fee to store penalty amounts.

Create Total Amount Payable Column

ALTER TABLE [DMF and Brokers]
ADD total_amount_payable DECIMAL;
UPDATE [DMF and Brokers]
SET total_amount_payable = 100000;

Adds a total_amount_payable column and sets a base registration fee of 100,000 units.

Add Email Address Column and Populate Data

ALTER TABLE [DMF and Brokers]
ADD email_address VARCHAR;

UPDATE [DMF and Brokers]
SET [DMF and Brokers].email_address = [FirmsEmails].email_address
FROM [DMF and Brokers]
INNER JOIN FirmsEmails ON [DMF and Brokers].Dealing_Member_Firms = [FirmsEmails].Dealing_Member_Firms;

Adds an email_address column and updates it by linking data from the FirmsEmails table.

Apply Late Fee for Overdue Payments

UPDATE [DMF and Brokers]
SET late_fee = total_amount_payable * 0.10
WHERE payment_status = 'Overdue';

Computes a late fee as 10% of the total amount payable for overdue firms.

Create and Update Total Amount Due Column

ALTER TABLE [DMF and Brokers]
ADD total_amount_due DECIMAL;

UPDATE [DMF and Brokers]
SET total_amount_due = total_amount_payable + late_fee;

Introduces total_amount_due to track final payable amounts, including late fees.

Retrieve Overdue Firms and Their Payment Dues

SELECT Dealing_Member_Firms, late_fee, total_amount_due
FROM [DMF and Brokers]
WHERE payment_status = 'Overdue';

Extracts details of firms with overdue payments, including their calculated late fees and total dues.

Purpose

These SQL updates and queries help automate the process of managing overdue payments, applying penalties, and sending payment reminders efficiently. By ensuring that firms' financial records remain accurate and up to date, this process streamlines financial compliance and revenue collection.

Notes

The dataset used is a sample dataset, and actual implementation may require modifications.

Ensure data integrity before executing the queries in a production environment.

Additional error handling and logging mechanisms may be incorporated for robustness.

Future Improvements

Automate payment reminders via email integration.

Implement dynamic late fee adjustments based on payment history.

Create a reporting dashboard for real-time financial monitoring.

