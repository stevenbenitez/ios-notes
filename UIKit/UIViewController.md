# UIViewController

## Performing a Manual Segue

```swift
// `self` refers to the UIViewController
self.performSegue(withIdentifier: "segueFromSourceToDestination", sender: self)
```

## Dismissing a Modal View Controller

```swift
self.dismiss(animated: true, completion: nil)
```

## Displaying an ActionSheet or Alert

```swift
let alert = UIAlertController(
    title: "Title Goes Here",
    message: "Are you sure you want to ... ?",
    // .actionsheet or .alert
    preferredStyle: .actionSheet
)

let deleteAction = UIAlertAction(title: "Delete", style: .destructive, handler: { action in
    // what happens if a user selects this option
})

// no handler, default just dismisses the alert
let cancelAction = UIAlertAction(title: "Cancel", style: .cancel, handler: nil)

alert.addAction(deleteAction)
alert.addAction(cancelAction)

// not sure if this is needed...
// Support display in iPad
alert.popoverPresentationController?.sourceView = self.view
alert.popoverPresentationController?.sourceRect = CGRect(origin: CGPoint(x: 1, y: 1), size: CGSize(width: self.view.bounds.size.width / 2.0, height: self.view.bounds.size.height / 2.0))

self.present(alert, animated: true, completion: nil)
```

## Links

  *  [API Reference: UIViewController](https://developer.apple.com/reference/uikit/uiviewcontroller)
