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

## Testing

Basic setup for creating a mock View Controller to test.

```swift
class MyCustomVCTests: XCTestCase {
    
    var appDelegate: AppDelegate?
    var storyboard : UIStoryboard?
    var viewController : MyCustomVC? // Replace MyCustomVC with the View Controller you are testing.
    
    override func setup() {
        storyboard = UIStoryboard(name: "Storyboard Name", bundle: nil) // Replace Storyboard Name
        viewController = storyboard.instantiateViewController(withIdentifier: "View Controller") as? MyCustomVC // Replace View Controller and MyCustomVC
        let _ = viewController.view // This will trigger viewDidLoad() 
    }
}
```

Trigger the initialization of the UI elements when testing.

```swift
    viewController.beginAppearanceTransition(true, animated: false)
    viewController.endAppearanceTransition()
```