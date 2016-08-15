# sql-utils

**Date/Time no formato yyy/mm/dd hh:mm**

CAST(CONVERT(CHAR(17),DataCadastro,113) AS datetime)


**Obter PK inserida no insert atual**

SELECT CONVERT(INT, @@IDENTITY)

**Encontrar coluna**

SELECT t.name AS table_name, SCHEMA_NAME(schema_id) AS schema_name, c.name AS column_name FROM sys.tables AS t INNER JOIN sys.columns c ON t.OBJECT_ID = c.OBJECT_ID WHERE c.name LIKE '%FLAG%' ORDER BY schema_name, table_name;

**Zerar PK**

DBCC CHECKIDENT ('PlanoConta', RESEED, 0)

**SELECT / INSERT

INSERT INTO TABELA1 SELECT * FROM TABELA2

**Desabilitar integridade referencial**

EXEC sp_MSForEachTable 'ALTER TABLE ? NOCHECK CONSTRAINT ALL'

**Habilitar integridade referencial**

EXEC sp_MSForEachTable 'ALTER TABLE ? CHECK CONSTRAINT ALL'

**Consultar objetos do banco de dados**

SELECT * FROM sysobjects WHERE type = 'U'

**Encontrar e "matar" transação**

SELECT trans.session_id as [Session ID], trans.transaction_id as [Transaction ID], tas.name as [Transaction Name], tds.database_id as [Database ID]
FROM sys.dm_tran_active_transactions tas INNER JOIN sys.dm_tran_database_transactions tds ON (tas.transaction_id = tds.transaction_id ) INNER JOIN sys.dm_tran_session_transactions trans ON (trans.transaction_id=tas.transaction_id)
WHERE trans.is_user_transaction = 1 -- user AND tas.transaction_state = 2-- active AND tds.database_transaction_begin_time IS NOT NULL

KILL [Session_ID]

**Habilitar case sensitive**

ALTER TABLE usuario ALTER COLUMN senha VARCHAR (50) COLLATE SQL_Latin1_General_CP1_CS_AS NOT NULL

**Script para criação do DB de ASP.NET Session usando SQL**

https://github.com/khaueviana/sql-utils/blob/master/script-DB-ASP-State.sql
