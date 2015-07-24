# Project 3: Social Media with UIActivityViewController

1. take the project1 folder on your desktop
1. rename it to project 3
1. open `DetailViewController.swift`
1. line 34 (in `viewDidLoad` method) - add
```swift
navigationItem.rightBarButtonItem = UIBarButtonItem(barButtonSystemItem: .Action, target: self, action: "shareTapped")
```
1. line 43 (brand new method) - add
```swift
func shareTapped() {
    let vc = UIActivityViewController(activityItems: [detailImageView.image!], applicationActivities: [])
    presentViewController(vc, animated: true, completion: nil)
}
```
1. compile
