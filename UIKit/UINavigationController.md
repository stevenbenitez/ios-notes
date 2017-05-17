# UINavigationController

TODO

## Displaying an Image in a UINavigationController Title

Note that this must be done inside the class that is displayed in your `UINavigationController`, not in the navigation controller itself.

```swift
class MyViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()

        // change "navigation-logo" to the name of your image in your assets
        // catalog
        let logo = UIImage(named: "navigation-logo")
        let imageView = UIImageView(image: logo)
        self.navigationItem.titleView = imageView
    }
}
```

## Links

  *  [API Reference: UINavigationController](https://developer.apple.com/reference/uikit/uinavigationcontroller)
