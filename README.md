# sql-utils

**Date/Time format yyy/mm/dd hh:mm**

CAST(CONVERT(CHAR(17),DataCadastro,113) AS datetime)

**GET current PK inserted**

SELECT CONVERT(INT, @@IDENTITY)

**Find collumn**

SELECT t.name AS table_name, SCHEMA_NAME(schema_id) AS schema_name, c.name AS column_name FROM sys.tables AS t INNER JOIN sys.columns c ON t.OBJECT_ID = c.OBJECT_ID WHERE c.name LIKE '%FLAG%' ORDER BY schema_name, table_name;

**Reset PK**

DBCC CHECKIDENT ('PlanoConta', RESEED, 0)

**SELECT / INSERT

INSERT INTO TABELA1 SELECT * FROM TABELA2

**Unable referential integrity**

EXEC sp_MSForEachTable 'ALTER TABLE ? NOCHECK CONSTRAINT ALL'

**Enable referential integrity**

EXEC sp_MSForEachTable 'ALTER TABLE ? CHECK CONSTRAINT ALL'

**Find objects**

SELECT * FROM sysobjects WHERE type = 'U'

**KILL transaction**

SELECT trans.session_id as [Session ID], trans.transaction_id as [Transaction ID], tas.name as [Transaction Name], tds.database_id as [Database ID]
FROM sys.dm_tran_active_transactions tas INNER JOIN sys.dm_tran_database_transactions tds ON (tas.transaction_id = tds.transaction_id ) INNER JOIN sys.dm_tran_session_transactions trans ON (trans.transaction_id=tas.transaction_id)
WHERE trans.is_user_transaction = 1 -- user AND tas.transaction_state = 2-- active AND tds.database_transaction_begin_time IS NOT NULL

KILL [Session_ID]

**Enable case sensitive**

ALTER TABLE usuario ALTER COLUMN senha VARCHAR (50) COLLATE SQL_Latin1_General_CP1_CS_AS NOT NULL

**Script for creating ASP.NET Session DB using SQL**

DB ASPState

https://github.com/khaueviana/sql-utils/blob/master/DB-ASP-State.sql

Temp tables

https://github.com/khaueviana/sql-utils/blob/master/ASPState-tempdb.sql
