# JPA Trick

## update during create/update
```
	@PrePersist
	@PreUpdate
	public void updateTimestampOnUpdateInsert() {
		this.setLastUpdatedDate(new Date());
	}
```

## insert default value if null
```
	@Column(name = "lastUpdatedBy", length = 255)
	private String lastUpdatedBy = "API-user";
```

## add ,ulti column constraints
```
@Data
@Entity
@Table( /* schema = "DBO", */  name = "ASSOCIATE_SUBMISSIONS",
		uniqueConstraints=
			@UniqueConstraint
			(columnNames={"globalId", "userId","brandCode"}))
public class LoyaltySubmissions {
```
