# Ms-SQl 20212

List all linked server if you don’t want the local server returned
```
SELECT 
  name,
  provider,
  data_source
FROM sys.servers
WHERE is_linked = 1;

```


* Rename column name
```
EXEC sp_rename 'dbo.AssociateSubmissions.oldglobalIdname', 'newglobalId', 'COLUMN';
```

* Rename table name 
```
EXEC sp_rename 'dbo.EmployeeClass', 'AllowedEmployeeClass';
```
