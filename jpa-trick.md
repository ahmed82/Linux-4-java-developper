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
		uniqueConstraints={
			@UniqueConstraint
			(columnNames={"globalId", "userId","brandCode"})})
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
## Call Stored Procedure

Spring boot and Sql Server- In your Repository

1) with no parameter
```
@Query(value = "{call yourSpName()}", nativeQuery = true)
List<Map<String, Object>> methodName();
```
2) with Parameter
```
@Query(value = "{call yourSpName(:param1)}", nativeQuery = true)
List<Map<String, Object>> methodName(@Param("param1")Long param1);
```
## Old implementation:
```java
@Service
public class LoginServiceImpl implements LoginService {

    @PersistenceContext
    private EntityManager entityManager;

    public Boolean checkUsernameAndPassword(String username, String password) {

        //"login" this is the name of your procedure
        StoredProcedureQuery query = entityManager.createStoredProcedureQuery("login"); 

        //Declare the parameters in the same order
        query.registerStoredProcedureParameter(1, String.class, ParameterMode.IN);
        query.registerStoredProcedureParameter(2, String.class, ParameterMode.IN);
        query.registerStoredProcedureParameter(3, Integer.class, ParameterMode.OUT);
        query.registerStoredProcedureParameter(4, String.class, ParameterMode.OUT);

        //Pass the parameter values
        query.setParameter(1, username);
        query.setParameter(2, password);

        //Execute query
        query.execute();

        //Get output parameters
        Integer outCode = (Integer) query.getOutputParameterValue(3);
        String outMessage = (String) query.getOutputParameterValue(4);

        return true; //enter your condition
    }
}
```
