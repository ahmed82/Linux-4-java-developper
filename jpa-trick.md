# JPA Trick

## update during create/update
```
	@PrePersist
	@PreUpdate
	public void updateTimestampOnUpdateInsert() {
		this.setLastUpdatedDate(new Date());
	}
```
