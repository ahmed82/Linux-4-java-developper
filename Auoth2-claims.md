## Auoth2-claims

```java
@GetMapping("/1")
	public void getPolicy(Authentication authentication) {
		AADOAuth2AuthenticatedPrincipal userPrincipal = (AADOAuth2AuthenticatedPrincipal) authentication.getPrincipal();
		 Map<String, Object> map = new LinkedHashMap<>();
		 map = (Map<String, Object>) userPrincipal.getClaims();
		 System.out.println(map.get("GlobalID"));
		 System.out.println("Username: " + map.get("name"));
		 System.out.println("Email: " + map.get("upn"));
		System.out.println(userPrincipal.getName());
		System.out.println(userPrincipal.getGid());

	}
```
