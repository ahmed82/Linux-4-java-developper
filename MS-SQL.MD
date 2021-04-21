# Ms-SQl 20212

## Rename column name
```
EXEC sp_rename 'dbo.AssociateSubmissions.oldglobalIdname', 'newglobalId', 'COLUMN';
```

## Rename table name 
```
EXEC sp_rename 'dbo.EmployeeClass', 'AllowedEmployeeClass';
```

create multi column constrain
