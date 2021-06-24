## Auoth2-claims

```java
@GetMapping("/enrollments")
	public void getPolicy(Authentication authentication) {
		AADOAuth2AuthenticatedPrincipal userPrincipal = (AADOAuth2AuthenticatedPrincipal) authentication.getPrincipal();
		/*******************
		* For overload the method and add custom methods
		********************/
		String userId = userPrincipal.getName();
		String gloableId = userPrincipal.getGid();
		System.out.println(userPrincipal.getName());
		System.out.println(userPrincipal.getGid());
		/*******************
		* For extracting the claims from the JWT token
		********************/
		 Map<String, Object> map = new LinkedHashMap<>();
		 map = (Map<String, Object>) userPrincipal.getClaims();
		 System.out.println(map.get("GlobalID"));
		 System.out.println("Username: " + map.get("name"));
		 System.out.println("Email: " + map.get("upn"));
		 


	}
```
