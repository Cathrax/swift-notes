# Project 1: Storm Viewer

Hacking with Swift





## Setting Up



launch Xcode

&nbsp; create new Project

&nbsp;&nbsp; choose MasterDetail App

&nbsp;&nbsp; click next

&nbsp;&nbsp;&nbsp; name it “Project1”

&nbsp;&nbsp;&nbsp; select Swift for language

&nbsp;&nbsp;&nbsp; select iPhone for devices

&nbsp;&nbsp;&nbsp; Organization identifier is “com.example”

&nbsp;&nbsp;&nbsp; uncheck “use core data”

next to the play button it says Project1 - to the right select “iPhone 5”



click Compile (play)



drag the Content folder to just under “Supporting Files”

check “Copy items if needed”

check “Create groups”

click Finish (folder should be yellow, not blue)





## Deleting skeleton code



To display line numbers: Preferences>Text Editing>check “Live Numbers”



Lines 23-26 - delete

self.navigationItem.leftBarButtonItem

let addButton

self.navigationItem.rightBarButtonItem



Line 30-34 - delete entire method starting with

func insertNewObject() {



Line 66-73 (last method) - delete

override func tableView(tableView: UITableView, commitEditingStyle editingStyle: UITableViewCellEditingStyle, forRowAtIndexPath indexPath: NSIndexPath)



Line 53 - look for

tableView(_:cellForRowAtIndexPath:)

underneath it look for Line 56

let object = objects[indexPath.row] as! NSDate

cell.textLabel!.text = object.description



delete

as! NSDate

.description

so that it now looks like

let object = objects[indexPath.row]

cell.textLabel!.text = object



Line 34 - look for

prepareForSegue()

underneath it delete Line 37

as! NSDate

so that it now looks like

let object = objects[indexPath.row]







## Listing images with NSFileManager



Line 20 - look for

func viewDidLoad() {

underneath that look for Line 21

super.viewDidLoad()

underneath that, input

let fm = NSFileManager.defaultManager()

let path = NSBundle.mainBundle().resourcePath!

let items = fm.contentsOfDirectoryAtPath(path, error: nil)



for item in items as! [String] {

if item.hasPrefix("nssl") {

 objects.append(item)

}

}



Line 13 (at the top of MasterViewController) - look for

var objects = [AnyObject]()

change it to say instead

var objects = [String]()





## Introducing Interface Builder



click on the Interface Builder (Main.storyboard)

right click to choose “Zoom to 50%”



double-click on the detail view controller (rightmost of the boxes)

delete “Detail view content goes here”



look for the object library (bottom right box)

select the third icon (circle with square in the middle)

search for “Image” to select Image View

click and drag it to the detail view controller, don’t let go until the image stretches out to fill the entire controller

move it around until it’s centered



click the Pin button (lower right, anonymous looking button)

click the four dotted lines to make them solid

check “Add 4 Constraints”



click the overlapping circles button (Assistant Editor) in the upper right



Line 13 - delete

@IBOutlet weak var detailDescriptionLabel: UILabel!



hold down Ctrl, then click and drag from the UIImageView to where the @IBOutlet line was below class DetailViewController: UIViewController {



name your outlet “detailImageView” and click Connect



this line gets written for you: IBOutlet weak var detailImageView: UIImageView!





## Loading images with UIImage



Line 17 - look for in DetailViewController.swift

```swift
var detailItem: AnyObject? {
    didSet {
        // Update the view.
        self.configureView()
    }
}
```

delete `self.`

change `AnyObject?` to `String?` and press Cmd+B



Line 27 (error placement) - look for



```swift
if let detail: AnyObject = self.detailItem {
    if let label = self.detailDescriptionLabel {
        label.text = detail.description
    }
}
```


replace with

```swift
if let detail = self.detailItem {
    if let imageView = self.detailImageView {
        imageView.image = UIImage(named: detail)
    }
}
```

Line 43 - look for in MasterViewController.swift inside prepareForSeque() method Line 46

let object = objects[indexPath.row]

(segue.destinationViewController as DetailViewController).detailItem = object

replace with

let detailViewController = segue.destinationViewController as! DetailViewController

detailViewController.detailItem = objects[indexPath.row]



## Final tweaks: hidesBarsOnTap



press Cmd+R to run the app



select Main.storyboard, select the image view in the detail view controller

click the Attributes Inspector (4th of 6 buttons in top right, pointy arrow)

change “Scale to Fit” to “Aspect Fit”



Open DetailViewController.swift

Line 33 - look for viewDidLoad() and add directly underneath:

override func viewWillAppear(animated: Bool) {

    super.viewWillAppear(animated)

    navigationController?.hidesBarsOnTap = true

}



override func viewWillDisappear(animated: Bool) {

    super.viewWillDisappear(animated)

    navigationController?.hidesBarsOnTap = false

}

run the app… we’re done!s
