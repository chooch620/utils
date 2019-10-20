## JavaScript

Generic response handler when there is an ERROR with the server-side call.
See: [Error Handling Best Practices for Lightning and Apex](https://developer.salesforce.com/blogs/2017/09/error-handling-best-practices-lightning-apex.html)

```javascript
let errors = response.getError();
let message = 'Unknown error'; // Default error message
// Retrieve the error message sent by the server
if (errors && Array.isArray(errors) && errors.length > 0) {
    message = errors[0].message;
}
// Display the message
console.error(message);
```
