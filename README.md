# SwiftUI Cheat Sheet

![SwiftUI](https://raw.githubusercontent.com/SimpleBoilerplates/SwiftUI-Cheat-Sheet/master/assets/image.png)


### Table of Contents
- [SwiftUI Cheat Sheet](#swiftui-cheat-sheet)
    - [Table of Contents](#table-of-contents)
- [Resource](#resource)
- [UIKit equivalent in SwiftUI](#uikit-equivalent-in-swiftui)
- [View](#view)
    - [Text](#text)
    - [Image](#image)
    - [Shape](#shape)
- [Layout](#layout)
    - [Background](#background)
    - [VStack](#vstack)
    - [HStack](#hstack)
    - [ZStack](#zstack)
- [Input](#input)
    - [Toggle](#toggle)
    - [Button](#button)
    - [TextField](#textfield)
    - [Slider](#slider)
    - [Date Picker](#date-picker)
    - [Segmented Control](#segmented-control)
    - [Tap](#tap)
    - [Gesture](#gesture)
- [List](#list)
- [Containers](#containers)
    - [NavigationView](#navigationview)
    - [Group](#group)
- [Alerts and Action Sheets](#alerts-and-action-sheets)
- [Navigation](#navigation)
- [Work with UIKit](#work-with-uikit)
    - [Navigate to ViewController](#navigate-to-viewcontroller)
    - [Use UIKit and SwiftUI Views Together](#use-uikit-and-swiftui-views-together)

# Resource
- [SwiftUI Tutorials (Official)](https://developer.apple.com/tutorials/swiftui/creating-and-combining-views)
- [Introducing SwiftUI: Building Your First App (Official)](https://developer.apple.com/videos/play/wwdc2019/204/)
- [SwiftUI: Getting Started Raywenderlich](https://www.raywenderlich.com/3715234-swiftui-getting-started)
- [SwiftUI Essentials (Official)](https://developer.apple.com/videos/play/wwdc2019/216)
- [SwiftUI - How to setup a project](https://medium.com/@martinlasek/swiftui-getting-started-372389fff423)
- [About SwiftUI](https://github.com/Juanpe/About-SwiftUI)


# UIKit equivalent in SwiftUI
| UIKit | [SwiftUI](https://developer.apple.com/xcode/swiftui/) |
| ----------- | ----------- |
| UILabel | [Text](#text) |
| UIImageView | [Image](#image) |
| UITextField | [TextField](#textfield) |
| UITextView | No equivalent (use [Text](#text)) |
| UISwitch | [Toggle](#toggle) |
| UISlider | [Slider](#slider) |
| UIButton | [Button](#button) |
| UITableView | [List](#list) |
| UICollectionView | No equivalent (can be implemented by [List](#list)) |
| UINavigationController | [NavigationView](#navigationview) |
| UIAlertController with style .alert | [Alert](#alerts-and-action-sheets) |
| UIAlertController with style .actionSheet | [ActionSheet](#alerts-and-action-sheets) |
| UIStackView with horizontal axis| [HStack](#hstack) |
| UIStackView with vertical axis| [VStack](#vstack) |
| UISegmentedControl | [SegmentedControl](#segmented-control) |
| UIStepper | Stepper |
| UIDatePicker | [DatePicker](#date-picker) |
| NSAttributedString | No equivalent (use [Text](#text)) |

# View

### Text

To show a **text** in UI simply write
``` swift
Text("Hello World")
```

To add style
``` swift
Text("Hello World")
    .font(.largeTitle)
    .foregroundColor(Color.green)
    .lineSpacing(50)
    .lineLimit(nil)
    .padding()
```

To format text inside text view
``` swift
static let dateFormatter: DateFormatter = {
    let formatter = DateFormatter()
    formatter.dateStyle = .long
    return formatter
}()

var now = Date()
var body: some View {
    Text("Task due date: \(now, formatter: Self.dateFormatter)")
}
```

### Image
 To show image
``` swift
Image("hello_world") //image name is hello_world
```

To use system icon
``` swift
Image(systemName: "cloud.heavyrain.fill")
```

you can add style to system icon set
``` swift
Image(systemName: "cloud.heavyrain.fill")
    .foregroundColor(.red)
    .font(.largeTitle)
```

Add style to Image
``` swift
Image("hello_world")
    .resizable() //it will sized so that it fills all the available space
    .aspectRatio(contentMode: .fill)
    .padding(.bottom)
```

### Shape

To create Rectangle
``` swift
Rectangle()
    .fill(Color.red)
    .frame(width: 200, height: 200)
```

To create circle
``` swift
Circle()
    .fill(Color.blue)
    .frame(width: 50, height: 50)
```

# Layout

### Background
To use image as a background
``` swift
Text("Hello World")
    .font(.largeTitle)
    .background(
        Image("hello_world")
            .resizable()
            .frame(width: 100, height: 100))
```

Gradient background
``` swift
Text("Hello World")
    .background(LinearGradient(gradient: Gradient(colors: [.white, .red, .black]), startPoint: .leading, endPoint: .trailing), cornerRadius: 0)
```

### VStack
Shows child view vertically
``` swift
VStack {
    Text("Hello")
    Text("World")
}
```
Styling
``` swift
VStack (alignment: .leading, spacing: 20){
    Text("Hello")
    Divider()
    Text("World")
}
```

### HStack
Shows child view horizontally
``` swift
HStack {
    Text("Hello")
    Text("World")
}
```


### ZStack

To create overlapping content use ZStack
``` swift
ZStack() {
    Image("hello_world")
    Text("Hello World")
        .font(.largeTitle)
        .background(Color.black)
        .foregroundColor(.white)
}
```

# Input

### Toggle

Toggle lets users move between true and false states
``` swift
@State var isShowing = true //state

Toggle(isOn: $isShowing) {
    Text("Hello World")
}.padding()
```

### Button
To create button
``` swift
Button(action: {
    // do something
}) {
    Text("Click Me")
}
```
To create image Button
``` swift
Button(action: {
    // do something
}) {
    Image("hello_world")
}
```

### TextField

It heavily relies in state, simply create a state and pass it as it will bind to it
``` swift
@State var fullName: String = "Joe" //create State

TextField($fullName) // passing it to bind
    .textFieldStyle(.roundedBorder) //adds border

```

To create secure TextField
``` swift
@State var password: String = "" //create State

SecureField($password) // passing it to bind
    .textFieldStyle(.roundedBorder) //adds border

```

### Slider

``` swift
@State var value: Double = 0 //create State
    
Slider(value: $value, from: -100, through: 100, by: 1)
```

### Date Picker
``` swift
@State var selectedDate = Date()
DatePicker(
    $selectedDate,
    maximumDate: Date(),
    displayedComponents: .date
)
```

### Segmented Control

``` swift
@State var favoriteColor = 0
var colors = ["Red", "Green", "Blue"]

SegmentedControl(selection: $favoriteColor) {
    ForEach(0..<colors.count) { index in
        Text(self.colors[index]).tag(index)
    }
}
```

### Tap
For single tap
``` swift
Text("Tap me!")
    .tapAction {
       print("Tapped!")
}
```
For double tap
``` swift
Text("Tap me!")
    .tapAction (count: 2) {
       print("Tapped!")
}
```

### Gesture
 Gesture like **TapGesture**, **LongPressGesture**, **DragGesture**
``` swift
Text("Tap")
    .gesture(
        TapGesture()
            .onEnded { _ in
                        
            }
        )

Text("Drag Me")
    .gesture(
        DragGesture(minimumDistance: 50)
            .onEnded { _ in
                        
            }
        )

Text("Long Press")
   .gesture(
        LongPressGesture(minimumDuration: 2)
            .onEnded { _ in
                        
            }
        )
```

# List

To create static scrollable **List**

``` swift
List {
    Text("Hello world")
    Text("Hello world")
    Text("Hello world")
}
```

To create dynamic **List**
``` swift
let names = ["Thanos", "Iron man", "Ant man"]
List(names) { name in
        Text(name)
}
```

To add section
``` swift
List {
    Section(header: Text("Good Hero")) {
        Text("Thanos")
    }

    Section(header: Text("Bad Heros")) {
        Text("Iron man")
    }
}
```

To make it grouped add *.listStyle(.grouped)*
``` swift
List {
    Section(header: Text("Good Hero")) {
        Text("Thanos")
    }

    Section(header: Text("Bad Heros")) {
        Text("Iron man")
    }
}.listStyle(.grouped)
```

# Containers

### NavigationView

**NavigationView** is more/less like **UINavigationController**, It handles navigation between views, shows title, places navigation bar on top. 

``` swift
NavigationView {
    Text("Hello")
        .navigationBarTitle(Text("World"), displayMode: .inline)
}
```

For large title use *.large*

Add bar items to **NavigationView**
``` swift
NavigationView {
    Text("Hello")
        .navigationBarTitle(Text("World"), displayMode: .inline)
        .navigationBarItems(trailing:
                Button(action: {
                    print("Going to Setting")
                }) {
                    Text("Setting")
                })
}
```

### Group
Group creates several views to act as one, also to avoid Stack's 10 View maximum limit.
``` swift
VStack {
    Group {
        Text("Hello")
        Text("Hello")
        Text("Hello")
    }
    Group {
        Text("Hello")
        Text("Hello")
    }
}
```

# Alerts and Action Sheets
To Show an Alert
``` swift
Alert(title: Text("Title"), message: Text("message"), dismissButton: .default(Text("Ok!")))

```
To Show Action Sheet
``` swift
ActionSheet(title: Text("Title"), message: Text("Message"), buttons: [.default(Text("Ok!"), onTrigger: {
    print("hello")
})])
```

# Navigation
Navigate via **NavigationButton**
``` swift
NavigationView {
    NavigationButton(destination: SecondView()) {
        Text("Show")
    }.navigationBarTitle(Text("First View"))
}
```

Navigate via tap on List Item
``` swift
let names = ["Thanos", "Iron man", "Ant man"]
List(names) { name in
    NavigationButton(destination: HeroView(name: name)) {
        Text(name)
    }
}
```

Navigate via **PresentationButton**

``` swift
PresentationButton(Text("Tap"), destination: HeroView())
```

# Work with UIKIT

### Navigate to ViewController

>  It's possible to work with UIKIT component from SwiftUI or call SwiftUI view as View Controller from UIKIT. 

Let's say you have a View Controller named as SuperVillainViewController and want to call from SwiftUI view, to do that ViewController need to implement UIViewControllerRepresentable

``` swift
struct SuperVillainViewController: UIViewControllerRepresentable {
    var controllers: [UIViewController]
    func makeUIViewcontroller(context: Context) -> SuperVillainViewController {
        // you could have a custom constructor here, I'm just keeping it simple
        let vc = SuperVillainViewController()
        return vc
    }
}
```
Now you can use it like 
``` swift
NavigationButton(destination: SuperVillainViewController()) {
    Text("Click")
}
```
### Use UIKit and SwiftUI Views Together

> To use UIView subclasses from within SwiftUI, you wrap the other view in a SwiftUI view that conforms to the UIViewRepresentable protocol. ([Reference](https://developer.apple.com/tutorials/swiftui/creating-and-combining-views#use-uikit-and-swiftui-views-together))

as example 
``` swift

import SwiftUI
import MapKit

struct MapView: UIViewRepresentable {
    func makeUIView(context: Context) -> MKMapView {
        MKMapView(frame: .zero)
    }

    func updateUIView(_ view: MKMapView, context: Context) {
        let coordinate = CLLocationCoordinate2D(
            latitude: 34.011286, longitude: -116.166868)
        let span = MKCoordinateSpan(latitudeDelta: 2.0, longitudeDelta: 2.0)
        let region = MKCoordinateRegion(center: coordinate, span: span)
        view.setRegion(region, animated: true)
    }
}

struct MapView_Preview: PreviewProvider {
    static var previews: some View {
        MapView()
    }
}
```

