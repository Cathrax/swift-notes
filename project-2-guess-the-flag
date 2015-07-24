# Project 2: Guess the Flag

**Hacking with Swift**

Make a game using UIKit and learn about integers, buttons, colors, and actions.
The game will show random flags to users and ask them to choose which one
belongs to a particular country.


## Setting Up

* launch Xcode
* choose “Create a new project”
* choose Single View Application
* click Next
* Product Name “Project2”
* select Swift for language
* select iPhone for devices
* click Next


## Designing your layout


choose Main.storyboard

click inside the view controller

Editor>Embed In>Navigation Controller



click inside the view controller again

in the bottom right box, click the circle with square in the middle of it icon

search “button”

drag three “Button” to the canvas



click on the size indicator (ruler in upper right)

Width 200

Height 100

first flag y-axis 100

second flag y-axis 230

third flag y-axis 360



select the top button (so the rest of the controller is grey)

Ctrl-drag the button to the grey area so it lights up blue

hold down Shift

select “Top Space to Top Layout Guide”

let go of Shift

select “Center Horizontally in Container”



select images.xcassets

select all the files for the course (36 flag icons)

drag and drop under “AppIcon”



select Main.storyboard

select attributes inspector

delete the title “Button”

dropdown arrow “Image”

select “us”



assign “us” to the 2nd and 3rd buttons



select the 2nd button

select it so the rest of the controller is grey

drag it to the 1st button

select “Vertical Spacing”

select “Center X”



repeat for 3rd button



select the 1st button

select the blue vertical line

change Constant to 0



select the “Center X” constraints

change Constant to 0 (all should snap into placement)



open assistant editor (two rings button)

drag each flag one by one to just under class ViewController: UIViewController {

name: button1, button2, button3

exit out of assistant editor



select ViewController.swift





## Making the basic game work: UIButton and CALayer



directly below @IBOutlet lines 12-14, add

var countries = [String]()

var score = 0



Line 21 under super.viewDidLoad() - add

countries += ["estonia", "france", "germany", "ireland", "italy", "monaco", "nigeria", "poland", "russia", "spain", "uk", "us"]

underneath, add (error ok)

askQuestion()



Line 26 - add

func askQuestion() {

    button1.setImage(UIImage(named: countries[0]), forState: .Normal)

    button2.setImage(UIImage(named: countries[1]), forState: .Normal)

    button3.setImage(UIImage(named: countries[2]), forState: .Normal)

}

compile



Line 22 - add above askQuestion()

button1.layer.borderWidth = 1

button2.layer.borderWidth = 1

button3.layer.borderWidth = 1

Line 25 - add

button1.layer.borderColor = UIColor.lightGrayColor().CGColor

button2.layer.borderColor = UIColor.lightGrayColor().CGColor

button3.layer.borderColor = UIColor.lightGrayColor().CGColor

*optional* change the colors to

UIColor(red: 1.0, green: 0.6, blue: 0.2, alpha: 1.0).CGColor



Guess which flag: Random numbers



open the project files

select Array+Shuffling.swift

drag to just under ViewController.swift



Line 33 under func askQuestion()- add

countries.shuffle()

Line 18 - add

var correctAnswer = 0

Line 38 - add

correctAnswer = Int(arc4random_uniform(3))

Line 39 (just underneath) - add

title = countries[correctAnswer].uppercaseString



From outlets to actions: IBAction and string interpolation



select Main.storyboard

click assistant editor

ctrl+drag Button1 to Line 42

change Connection: Outlet to Action

change Type: AnyObject to UIButton

name buttonTapped

click Connect

ctrl+drag Button2 and Button3 to the same method

close assistant editor



select Button2

click on attributes inspector

change Tag to 1



select Button3

change Tag to 2



select ViewController.swift



Line 43 inside the method - add

var title: String



if sender.tag == correctAnswer {

    title = "Correct"

    ++score

} else {

    title = "Wrong"

    --score

}



Line 52 - add (error ok) just underneath but still inside buttonTapped method

let ac = UIAlertController(title: title, message: "Your score is \(score).", preferredStyle: .Alert)

ac.addAction(UIAlertAction(title: "Continue", style: .Default, handler: askQuestion))

presentViewController(ac, animated: true, completion: nil)

Line 33 - change (error ok)



func askQuestion() {

to



func askQuestion(action: UIAlertAction!) {



Line 29 - change to EITHER



askQuestion(nil)

OR Line 33 to

func askQuestion(action: UIAlertAction! = nil) {



Compile
