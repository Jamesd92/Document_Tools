# SQL Information

This document is a quick guide for how to navigate MSSQL.

## Table of Contents

1. [Database Configuration]
2. [SQL Queries]
3. [Connection Strings]
4. [CDC]

## Database Configuration

This section covers common initialisation issues that occur when building an "MSSQL" server.

### SQL Server Configuration Manager

To allow remote clients to access the MSSQL server the server must be configured to accept TCP/IP connection requests. This need to be turn on in the "SQL Server Configuration Manager" under the SQL Server Network Configuration section and setting the "TCP/IP" status true.

## SQL Queries

## Connection Strings

- JDBC (java connection driver)
- OLE (historical microsoft driver)
- ODBC (Current microsoft driver)

### JDBC

java Driver most common

### OLE

Historical driver used for Access or internal database connections on the same machines.

### ODBC

Current microsoft drivers used for cross network interfacing.

## CDC

The Change Data Capture (CDC) is utilised to capture any Data Manipulation Language (DML) it does not "capture" DQL actions.

It is important to state that if a table is modified that then the added table will not be tracked, to add this table a new CDC "capture_group" needs to be made which includes the new column, then the old CDC capture group needs to be disabled. Only two capture groups can be added to a table.

DML

1. Insert
2. Update
3. Delete

### Commands

This query is used to pull the tables in database that are user tables and can be defined by Schema (dbo,dev,app)

`SELECT [name], is_tracked_by_cdc FROM sys.tables AS B LEFT JOIN INFORMATION_SCHEMA.TABLES AS A ON a.TABLE_NAME = b.[name] WHERE A.Table_Schema LIKE 'dbo' AND A.TABLE_TYPE LIKE 'BASE TABLE'`

---

Checks to see if the Database has the CDC enabled

SELECT [name], is_cdc_enabled From sys.databases

Enables CDC for the database

EXEC [database].sys.sp_cdc_enable_db

Disable CDC for the database
EXEC [database].sys.sp_cdc_disable_db

---

Check to see what tables have CDC enabled

SELECT [name], is_tracked_by_cdc from sys.tables

Enabling a table for CDC
{
EXEC sys.sp_cdc_enable_table  
 @source_schema = N'dbo',  
 @source_name = N'Employee_Main',  
 @role_name = NULL,  
 @filegroup_name = NULL,  
 @supports_net_changes = 0

}
Disabling a table with CDC
{
EXEC sys.sp_cdc_disable_table
@source_schema = N'dbo',
@souce_name = N'Employee_Main',
@capture_instance = N'dbo_Employee_Main'
}

To determine Information about the cdc group data run the below command
EXEC sys.sp_cdc_help_change_data_capture

---

Auditing DML changes

SELECT \* FROM cdc.[dbo_Employee_Main_CT]
Main Columns

- \_\_$start_lsn: Log sequence number (LSN) associated with the commit transaction for the change.
- \_\_$end_lsn: No longer used
- \_\_$seqval: sequence number to order the rows for each DML action
- \_\_$operation: Identifier of DML action - 1 = delete - 2 = insert - 3 = update (old values) - 4 = update (new values)
- \_\_$update_mask: bit mask to identify the changed columns
- \_\_$command_id: Tracks the order of the operations within a transaction.

---

useful links:

- https://www.mssqltips.com/sqlservertip/4096/understanding-how-dml-and-ddl-changes-impact-change-data-capture-in-sql-server/
- https://docs.microsoft.com/en-us/sql/relational-databases/system-tables/cdc-capture-instance-ct-transact-sql?view=sql-server-ver15
-
