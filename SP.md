## Stored Procedure

```sql

USE [LEGAL-DEV]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

 


-- =============================================
-- Author:        Ahmed Al Salih
-- Create date: 05-11-2021
-- Description:    Get the list of Item by SysRef number
-- =============================================
ALTER  PROCEDURE [dbo].[COMPLMGMT_RBS_sp_FileNet-07-DB] 
    -- Add the parameters for the stored procedure here
    @sYsRef_Num as varchar(11) = Null
    
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;

    DECLARE @SQL nvarchar (256)
	DECLARE @OpnQryStart varchar(50)
	DECLARE @sSelect varchar(2450)
	DECLARE @sWhere varchar(2450)
	DECLARE @OpnQryEnd varchar(50)
	DECLARE @sSQL as varchar(5000)

	--SET @SQL = 'SELECT * FROM OPENQUERY (LEGAL_FILENET7, ''SELECT CMPY, SUPP, SYSREF, TRAN_REF, TRAN_DATE FROM XPD1.POLAG.TGBTRAN WHERE TRAN_REF= '''''+ @Tran_Ref  +''''''')'
	--Broke the OpenQuery statement into 4 parts to make it easier to make changes
	SET @OpnQryStart = 'SELECT * FROM OPENQUERY
	(
	ORACLE_FILENET7,
	''	'

	SET @sSelect = '
	SELECT F_DOCNUMBER AS DOC_ID, F_DOCCLASSNUMBER AS DOCCLASS, A80 AS CORP, A81 AS CMPY, A83 AS GL_DEPT, A82 AS JE_NUM, A84 AS PD_YR, A34 AS SYS_REF, A46 AS DEPT, A32 AS BATCH, A35 AS AP_SUPP, A52 AS PO_SUPP, A36 AS PO_NUM, A49 AS INV_DATE, A33 AS INV_NUM, A40 AS INV_TOTAL, A43 AS LOCN, A45 AS PMA, A53 AS RECEIVING_DATE, A72 AS RECEIPT_DATE, A74 AS CHECK_NUM FROM F_SW.DOCTABA '
   --Print @SQL
   SET @sWhere = 'WHERE 
   A34 = ''''' + @sYsRef_Num + ''''' '

   SET @OpnQryEnd = ' 
	
	''
	)'
	
	--Build the complete statement
	SET @sSQL = @OpnQryStart + @sSelect + @sWhere + @OpnQryEnd

	EXEC (@sSQL)
   -- EXECUTE sp_executesql @SQL
	
END
```
