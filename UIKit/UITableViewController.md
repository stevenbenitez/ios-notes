# UITableViewController

## Adding a Refresh Control

```swift
    override func viewDidLoad() {
        super.viewDidLoad()

        self.refreshControl?.addTarget(self, action: #selector(handleRefresh(refreshControl:)), for: UIControlEvents.valueChanged)
    }

    func handleRefresh(refreshControl: UIRefreshControl) {
        // do some reloading of data and update the table view's data source.
        // fetch more objects from a web service, for example

        self.tableView.reloadData()
        refreshControl.endRefreshing()
    }
```

## Links

  *  [API Reference: UITableViewController](https://developer.apple.com/reference/uikit/uitableviewcontroller)
