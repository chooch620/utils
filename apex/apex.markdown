## Testing

When a Trigger prevents a record from being inserted, there should be a message associate with it.

```Apex
static void checkThatInsertionFailed(Database.SaveResult dmlResult, String message) {
    // Insertion should have been stopped by the user.
    System.assert(!dmlResult.isSuccess());
    // If it's stopped correctly, we should also receive an error
    System.assert(dmlResult.getErrors().size() > 0);
    // This error should say This room will be occupied during that time. Please choose another.
    System.assertEquals(message, dmlResult.getErrors()[0].getMessage());
}
```
