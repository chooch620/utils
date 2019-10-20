## Swift

Reference to the App Delegate

```Swift
let appDelegate = (UIApplication.shared.delegate as! AppDelegate)
```


Store user's session which will automatically sign the user in on their next visit. This is dependent on you having two string variables prior, `email` and `password`.

```swift
let defaults = UserDefaults.standard
defaults.set(email, forKey: "emailAddress")
defaults.set(password, forKey: "password")
defaults.synchronize()
```

Safely retrieve user's session credentials. This is dependent on `emailAddress` and `password` being stored in the UserDefaults prior.

```swift
let defaults = UserDefaults.standard
if let email = defaults.object(forKey: "emailAddress") as? String, 
    let password = defaults.object(forKey: "password") as? String { 
        // do something
}
```


## Firebase

Update a Firebase document.

```swift
let db = Firestore.firestore()
func updateDocument(documentId: String, pathToDocument: String, fieldsToUpdate: [String:Any]) {
    let document = db.collection(pathToDocument).document(documentId)
    
    document.updateData(fieldsToUpdate) {
        err in
        if let err = err {
            print("Error updating document: \(err)")
        } else {
            print("Document successfully updated")
        }
    }
}
```