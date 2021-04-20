# JPA Tricks

## Update during create/update
```
	@PrePersist
	@PreUpdate
	public void updateTimestampOnUpdateInsert() {
		this.setLastUpdatedDate(new Date());
	}
```

## Insert default value if null
```
	@Column(name = "lastUpdatedBy", length = 255)
	private String lastUpdatedBy = "API-user";
```

## Add multi column UniqueConstraint
```
@Data
@Entity
@Table( /* schema = "DBO", */  name = "ASSOCIATE_SUBMISSIONS",
		uniqueConstraints=
			@UniqueConstraint
			(columnNames={"globalId", "userId","brandCode"}))
public class LoyaltySubmissions {
```
## Multi columns primary key
add `@IdClass` on top of the class
```
@IdClass(EmployeeStatus.EmployeeCompositKey.class)
```
Implements Serializable
```
implements Serializable
```
Create inner CompositKey class
```
public static class EmployeeStatusCompositKey implements Serializable {

    	private static final long serialVersionUID = 1L;
    	
    	@SuppressWarnings("unused")
		private String brandCode;
    	
    	@SuppressWarnings("unused")
		private String employeeStatus;

		public EmployeeStatusCompositKey() {
			super();
		}

		public EmployeeStatusCompositKey(String brandCode, String employeeStatus) {
			super();
			this.brandCode = brandCode;
			this.employeeStatus = employeeStatus;
		}
    	
    	
	}
```
