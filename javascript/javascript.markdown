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

Given a path and an Id, retrieve a [DocumentReference](https://firebase.google.com/docs/reference/js/firebase.firestore.DocumentReference).

```javascript
/**
 * Get firebase document
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

Given a document which contains user device Ids, send a notification.

```javascript
/**
 * Send notification a device registered in Firebase with a unique device Id.
 * @param deviceIdDocument Holds the Firebase Id for a given device.
 * @param notificationContent The JSON message to send to the receiving user.
 */
function sendNotification(deviceIdDocument, notificationContent) {
    // Retrieve device Id
    deviceIdDocument.get()
        .then(doc => {
            if (!doc.exists) {
                console.log('No such document!');
            } else {
                var deviceId = doc.data()["id"];
                sendNotificationToDevice(deviceId, notificationContent);
            }
        })
        .catch(err => {
            console.log('Error getting document', err);
        });
}
```

Send a notificationt to a device using their Id.

```javascript
/**
 * Send notification a device registered in Firebase with a unique device Id.
 * @param deviceId Holds the Firebase Id for a given device.
 * @param notificationContent The message to send to the receiving user.
 */
function sendNotificationToDevice(deviceId, notificationContent) {
    admin.messaging().sendToDevice(deviceId, notificationContent);
}
```

Allows us to nicely format our cloud function folders, with scale in mind.

```javascript
/**
 * 
 *  Loads all `.f.js` files.
 *  Exports a cloud function matching the file name
 * 
 *  See: https://github.com/firebase/functions-samples/issues/170#issuecomment-325118145
 *       https://codeburst.io/organizing-your-firebase-cloud-functions-67dc17b3b0da
 *       
 */
const files = glob.sync('./**/*.f.js', { cwd: __dirname, ignore: './node_modules/**'});
for(let f=0,fl=files.length; f<fl; f++){
  const file = files[f];
  const functionName = camelCase(file.slice(0, -5).split('/').join('_')); // Strip off '.f.js'
  if (!process.env.FUNCTION_NAME || process.env.FUNCTION_NAME === functionName) {
    exports[functionName] = require(file);
  }
}
```