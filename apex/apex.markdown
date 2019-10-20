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


## Trigger

Trigger Context Variables

```Apex
if (Trigger.isBefore) {
    if (Trigger.isInsert) {

    } else if (Trigger.isUpdate) {
        
    } else { // delete

    }
} else {
    if (Trigger.isInsert) {

    } else if (Trigger.isUpdate) {

    } else if (Trigger.isDelete) {

    } else { // undelete

    }
}
```

addError() generic method - I'd put these within a Utility class so that you may call them from others.

```Apex
static void preventDMLOperation(List<sObject> recordsToDeny, String message) {
    for (sObject record: recordsToDeny) {
        preventDMLOperation(record,  message);
    }
}

static void preventDMLOperation(sObject recordToDeny, String message) {
    recordToDeny.addError(message);
}
```