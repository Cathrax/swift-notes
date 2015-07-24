# Project 4: Easy Browser with WKWebView

1. open a new project
	1. Single View Application
	1. name Project4

then:

1. open Main.storyboard
	1. select the view controller
	1. Editor>Embed In>Navigation Controller


## Creating a simple browser with WKWebView

open `ViewController.swift`

line 13 - add
```
override func loadView() {
    webView = WKWebView()
    webView.navigationDelegate = self
    view = webView
}
```

line 10 - add
```
import WebKit
```

line 14 - add
```
var webView: WKWebView!
```

line 12 - change to
```
class ViewController: UIViewController, WKNavigationDelegate {
```

line 24 - add
let url = NSURL(string: "http://www.slashdot.org")!
webView.loadRequest(NSURLRequest(URL: url))
webView.allowsBackForwardNavigationGestures = true
Choosing a Website: UIAlertController

line 27 - add
navigationItem.rightBarButtonItem = UIBarButtonItem(title: "Open", style: .Plain, target: self, action: "openTapped")

line 31 - add
func openTapped() {
    let ac = UIAlertController(title: "Open page…", message: nil, preferredStyle: .ActionSheet)
    ac.addAction(UIAlertAction(title: "apple.com", style: .Default, handler: openPage))
    ac.addAction(UIAlertAction(title: "slashdot.org", style: .Default, handler: openPage))
    ac.addAction(UIAlertAction(title: "Cancel", style: .Cancel, handler: nil))
    presentViewController(ac, animated: true, completion: nil)
}

line 39 - add
func openPage(action: UIAlertAction!) {
    let url = NSURL(string: "http://" + action.title)!
    webView.loadRequest(NSURLRequest(URL: url))
}

line 44 - add

func webView(webView: WKWebView, didFinishNavigation navigation: WKNavigation!) {
    title = webView.title
}


## Monitoring page loads: UIToolbar and UIProgressView

line 28 - add
let spacer = UIBarButtonItem(barButtonSystemItem: .FlexibleSpace, target: nil, action: nil)
let refresh = UIBarButtonItem(barButtonSystemItem: .Refresh, target: self, action: "refreshTapped")

toolbarItems = [spacer, refresh]
navigationController?.toolbarHidden = false
line 58 - add
func refreshTapped() {
    webView.reload()
}
line 29 - change to
let refresh = UIBarButtonItem(barButtonSystemItem: .Refresh, target: webView, action: "reload")
line 15 - add
var progressView: UIProgressView!
line 29 - add
progressView = UIProgressView(progressViewStyle: .Default)
progressView.sizeToFit()
let progressButton = UIBarButtonItem(customView: progressView)
line 35 - change to
toolbarItems = [progressButton, spacer, refresh]
line 28 - add
webView.addObserver(self, forKeyPath: "estimatedProgress", options: .New, context: nil)

line 41 - add
override func observeValueForKeyPath(keyPath: String, ofObject object: AnyObject, change: [NSObject: AnyObject], context: UnsafeMutablePointer<Void>) {
    if keyPath == "estimatedProgress" {
        progressView.progress = Float(webView.estimatedProgress)
    }
}


## Refactoring for the win

line 16 - add
var websites = ["apple.com", "slashdot.org"]
line 26 - change to
let url = NSURL(string: "http://" + websites[0])!
webView.loadRequest(NSURLRequest(URL: url))
lines 50 - 51 - change to
for website in websites {
    ac.addAction(UIAlertAction(title: website, style: .Default, handler: openPage))
}
line 75 - add
func webView(webView: WKWebView, decidePolicyForNavigationAction navigationAction: WKNavigationAction, decisionHandler: (WKNavigationActionPolicy) -> Void) {
    let url = navigationAction.request.URL

    if let host = url!.host {
        for website in websites {
            if host.rangeOfString(website) != nil {
                decisionHandler(.Allow)
                return
            }
        }
    }

    decisionHandler(.Cancel)
}
compile
