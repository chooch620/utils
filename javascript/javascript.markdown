## Node.js

Create notification content to be passed to Swift

```javascript
createNotificationContent: (title, body, icon) => {
    return {
        notification: {
            title: title,
            body: body,
            icon: icon,
        },
        data: { // Add custom information here
        }
    };
}
```

Given a path and an Id, retrieve a [DocumentReference](https://firebase.google.com/docs/reference/js/firebase.firestore.DocumentReference)

```javascript
/**
 * Get firebase document path
 * 
 * @param documentPath A slash-separated path to a document.
 * @param document The unique document identifier for the specified `documentPath`.
 * 
 * @return The `DocumentReference` instance.
 */
function getDocument(documentPath, document) {
    return db.collection(documentPath).doc(document);
}
```

