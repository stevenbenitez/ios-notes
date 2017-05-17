# UIPageViewController

## Getting Started

> A page view controller lets the user navigate between pages of content, where each page is managed by its own view controller object. Navigation can be controlled programmatically by your app or directly by the user using gestures. When navigating from page to page, the page view controller uses the transition that you specify to animate the change.

Unlike a `UITableViewController`, a `UIPageViewController` does not automatically implement its datasource and delegate interfaces. Your class should extend `UIPageViewController` and implement `UIPageViewControllerDataSource` and `UIPageViewControllerDelegate`.

```swift
class MyPageViewController: UIPageViewController, UIPageViewControllerDataSource, UIPageViewControllerDelegate {
    // these are the child view controllers
    var pages = [UIViewController]()

    override func viewDidLoad() {
        super.viewDidLoad()

        // assign the class as the dataSource and delegate
        self.dataSource = self
        self.delegate = self

        // create your child pages
        let page1: UIViewController! = storyboard?.instantiateViewController(withIdentifier: "page1")
        let page2: UIViewController! = storyboard?.instantiateViewController(withIdentifier: "page2")

        // add them to the array
        pages.append(page1)
        pages.append(page2)

        // despite its name, the first argument to this method is a singleton array
        // containing the first page. subsequent pages are returned in the
        // dataSource methods when navigating
        setViewControllers([page1], direction: .forward, animated: true)
    }
}
```

## UIPageViewControllerDataSource

### Supporting Navigation

```swift
public func pageViewController(_ pageViewController: UIPageViewController, viewControllerBefore viewController: UIViewController) -> UIViewController? {
    // return the UIViewController to display or nil if there is no page prior
    // to the current one
}

public func pageViewController(_ pageViewController: UIPageViewController, viewControllerAfter viewController: UIViewController) -> UIViewController? {
    // return the UIViewController to display or nil if there is no page after
    // the current one
}
```

### Supporting a Page Indicator

`UIPageViewController` has a built-in page indicator. To display the indicator, you must implement the following methods:

```swift
public func presentationCount(for pageViewController: UIPageViewController) -> Int {
    // return the total number of pages in your page view controller
}

public func presentationIndex(for pageViewController: UIPageViewController) -> Int {
    // return the index of the current page in your page view controller
}
```

## Links

  *  [API Reference::UIPageViewController](https://developer.apple.com/reference/uikit/uipageviewcontroller)
  *  [API Reference::UIPageViewControllerDataSource](https://developer.apple.com/reference/uikit/uipageviewcontrollerdatasource)
  *  [API Reference::UIPageViewControllerDelegate](https://developer.apple.com/reference/uikit/uipageviewcontrollerdelegate)

## Example

```swift
class MyPageViewController: UIPageViewController, UIPageViewControllerDataSource, UIPageViewControllerDelegate {
    var pages = [UIViewController]()

    override func viewDidLoad() {
        super.viewDidLoad()

        self.delegate = self
        self.dataSource = self

        view.backgroundColor = UIColor.white

        let page1: UIViewController! = storyboard?.instantiateViewController(withIdentifier: "page1")
        let page2: UIViewController! = storyboard?.instantiateViewController(withIdentifier: "page2")

        pages.append(page1)
        pages.append(page2)

        setViewControllers([page1], direction: .forward, animated: true)
    }

    override func viewDidLayoutSubviews() {
        super.viewDidLayoutSubviews()

        for subView in view.subviews {
            if subView is UIScrollView {
                subView.frame = UIScreen.main.bounds // Why? I don't know.
            }
            else if subView is UIPageControl {
                var pageControl = subView as! UIPageControl

                //pageControl.currentPageIndicatorTintColor = UIColor.white
                //pageControl.pageIndicatorTintColor = UIColor.gray
                subView.backgroundColor = UIColor.clear
            }
        }
    }

    public func pageViewController(_ pageViewController: UIPageViewController, viewControllerBefore viewController: UIViewController) -> UIViewController? {
        let index = pages.index(of: viewController)!

        if index > 0 {
            return pages[index - 1]
        }

        return nil
    }

    public func pageViewController(_ pageViewController: UIPageViewController, viewControllerAfter viewController: UIViewController) -> UIViewController? {
        let index = pages.index(of: viewController)!

        if index < pages.count - 1 {
            return pages[index + 1]
        }

        return nil
    }

    public func presentationCount(for pageViewController: UIPageViewController) -> Int {
        return pages.count
    }

    public func presentationIndex(for pageViewController: UIPageViewController) -> Int {
        if let vc = viewControllers?.first {
            if let index = pages.index(of: vc) {
                return index
            }
        }

        return 0
    }
}
```
