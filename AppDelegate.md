# AppDelegate

## Launching App from an URL

TODO: How to register a scheme for your app.

```swift
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?

    public func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
        // sb: this should never happen, as we only have one scheme registered,
        // but just in case.
        if url.scheme != "YOUR REGISTERED SCHEME" {
            return false
        }

        // sb: segue to reset password
        if url.path == "/reset-password" {
            self.window!.rootViewController!.performSegue(withIdentifier: "segueToResetPassword", sender: self)
            return true
        }

        return false
    }
}
```

## Links

  *  [UIApplicationDelegate](https://developer.apple.com/reference/uikit/uiapplicationdelegate)
