## Capture the argument

```java
    @Test
	public void should_DeleteIdentityProvider_For_ValidIdpId() throws Exception {
		ArgumentCaptor<DynamoIdentityProvider> captor = ArgumentCaptor.forClass(DynamoIdentityProvider.class);

		dynamoIdentityProviderRepository.deleteIdentityProvider(testIDP);
		// verify 'delete' is called on dynamoDBMapper exactly '1' times, and that 'delete' is called against the 'testDynamoIdentityProvider' object
		verify(idpDynamoDBMapper, times(1)).delete(captor.capture(), any(DynamoDBDeleteExpression.class));

		DynamoIdentityProvider actual = captor.getValue();
		assertEquals("name:", testDynamoIDP.getName(), actual.getName());
		assertEquals("display name:", testDynamoIDP.getDisplayName(), actual.getDisplayName());
		assertEquals("icon url:", testDynamoIDP.getIconURL(), actual.getIconURL());
		assertEquals("support url:", testDynamoIDP.getSupportURL(), actual.getSupportURL());
		assertEquals("partition:", testDynamoIDP.getPartition(), actual.getPartition());
		assertEquals("sort key:", testDynamoIDP.getSortKey(), actual.getSortKey());
	}
```
