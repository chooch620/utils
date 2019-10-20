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