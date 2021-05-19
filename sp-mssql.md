-- =======================================================
-- Create Stored Procedure Template for Azure SQL Database
-- =======================================================
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
-- =============================================
-- Author:      <Author, , Name>
-- Create Date: <Create Date, , >
-- Description: <Description, , >
-- =============================================
CREATE PROCEDURE sp_getFilteredElgiblity

    -- Add the parameters for the stored procedure here
  @lEgalEntity varchar(25) = Null
 ,@lOcationCode varchar(25) = Null
 ,@eMployeeStatus varchar(25) = Null
 ,@eMployeeClass varchar(25) = Null

AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON

    -- Insert statements for procedure here
    SELECT DISTINCT b.brandCode 
	FROM dbo.Brands AS b
	INNER JOIN(
			SELECT brandCode
			FROM dbo.LegalEntity
			WHERE legalEntity = @lEgalEntity
		UNION
			SELECT brandCode
			FROM dbo.EmployeeStatus
			WHERE employeeStatus = @eMployeeStatus

	)AS filters ON filters.brandCode = b.brandCode
END
GO
