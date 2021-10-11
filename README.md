# The Official matechmobile.com Swift Style Guide.
### Updated for Swift 5

Mục tiêu của chúng tôi là rõ ràng, nhất quán và ngắn gọn, dễ dàng cho người đọc.

## Table of Contents

* [Using SwiftLint](#using-swiftlint)
* [Naming](#naming)
  * [File Name](#file-name)
  * [Naming Component Function Actions](#naming-component-function-actions)
  * [Naming Delegate](#naming-delegate)
  * [Use Type Inferred Context](#use-type-inferred-context)
  * [Language](#language)
* [Code Organization](#code-organization)
  * [Protocol Conformance](#protocol-conformance)
  * [Unused Code](#unused-code)
  * [Minimal Imports](#minimal-imports)
* [Spacing](#spacing)
* [Comments](#comments)
* [Classes and Structures](#classes-and-structures)
  * [Self](#self)
  * [Protocol Conformance](#protocol-conformance)
  * [Computed Properties](#computed-properties)
* [Function Declarations](#function-declarations)
* [Closure Expressions](#closure-expressions)
* [Types](#types)
  * [Constants](#constants)
  * [Optionals](#optionals)
  * [Lazy Initialization](#lazy-initialization)
* [Memory Management](#memory-management)
  * [Extending Object Lifetime](#extending-object-lifetime)
* [Access Control](#access-control)
* [Control Flow](#control-flow)
* [Golden Path](#golden-path)


## Using SwiftLint
Bạn có thể tham khảo và sử dụng pod 'swiftLint' để kiểm tra lỗi theo format của raywenderlich.com

## Naming 

### File Name
- Đặt tên phải rõ ràng 
- Ưu tiên rõ ràng hơn ngắn gọn 
- Viết hoa chữ cái đầu với Class , Type , Protocol . Ví dụ : `ProductionLine`
- Viết thường chữ cái đầu với tất cả thứ còn lại như tên biến , tên Component , ... Ví dụ : `viewMain` , `buttonTap`
- Đặt tên dựa trên vai trò , chức năng 
- Không dùng các thuật ngữ gây nhầm lẫn cho người đọc
- Đặt tên không được viết tắt 

Ví dụ :
File chứa 1 loại duy nhất MyType thì được đặt tên là `MyType.swift`
  - MyType bổ sung thêm MyProtocol được đặt tên `MyType+MyProtoCol.swift`
  - MyType chứa thêm phần mở rộng đặt tên : `MyType+Additions.swift`
  - Một tệp chưa những thứ không liên quan ( Như một tập hợp các hàm toán học ) có thể đặt tên `Math.swift`
 
### Naming Component Function Actions

- Đặt tên cho biến theo quy tắc : lời giải thích +  Hậu tố ( button, label,... )
  - Ví dụ :  `SignUp`(Giải thích) + `button`(Hậu tố) = `signUpButton`  ,
    `name`(Giải thích) + `Label`(Hậu tố) = `nameLabel`

List Component :

| Kiểu          | Hậu tố       |		Ví dụ               |
|---------------| --------------|-----------------------|
| UIButton        | `button`	      | `nextButton`            |
| UILabel        | `label`	      | `nameLabel`            |
| UISlider        | `slider`	      | `sizeSlider`            |
| UISwitch        | `switch`	      | `nameSwitch`            |
| Page Control        | `pageControl`	      | `bannerPageControl`            |
| UIImageView     | `image`	    | `starImage`          |
| Navigation bar          | `navigation	`     | `homeNavigation`       |
| UIView    | `view`	    | `backgroundView`         |
| UiTextView      | `textView`       | `userNameTextView`      |
| UITextField      | `textField`       | `userNameTextField`      |
| UITableView      | `tableView`       | `contentTableView`      |
| UICollectionView      | `collectionView`       | `contentCollectionView`      |

Quy ước đặt tên cho Icon và Image trong Assets :

| Kiểu                            | Tiền tố            | Ví dụ                        |
| --------------------------------| ----------------   | ---------------------------- | 
| Icons                           | `ic_`              | `ic_star.png`                |
| Menu icons and Action Bar icons | `ic_menu`          | `ic_menu_archive.png`        |
| Tab icons                       | `ic_tab`           | `ic_tab_recent.png`          |
| Dialog icons                    | `ic_dialog`        | `ic_dialog_info.png`         |
| Background                      | `bg_`              | `bg_info.png`                |


- Đặt tên cho function : 
  - Nó phải bắt đầu bằng chữ thường.
  - Nó phải là một động từ như main (), print (), println ().
  - Nếu tên chứa nhiều từ, hãy bắt đầu nó bằng một chữ thường, sau đó là một chữ hoa, chẳng hạn như actionPerformed ().

### Naming Delegate
Khi đặt tên phương thức delegate , tuân theo quy tắc : tiền tố delegate + tên phương thức 

**Preferred**:
```swift
func namePickerView(_ namePickerView: NamePickerView, didSelectName name: String)
func namePickerViewShouldReload(_ namePickerView: NamePickerView) -> Bool
```

**Not Preferred**:
```swift
func didSelectName(namePicker: NamePickerViewController, name: String)
func namePickerShouldReload() -> Bool
```
### Use Type Inferred Context
Sử dụng Type Inferred Context của Xcode để viết mã ngắn gọn hơn , rõ ràng 

**Preferred**:
```swift
let selector = #selector(viewDidLoad)
view.backgroundColor = .red
let toView = context.view(forKey: .to)
let view = UIView(frame: .zero)
```

**Not Preferred**:
```swift
let selector = #selector(ViewController.viewDidLoad)
view.backgroundColor = UIColor.red
let toView = context.view(forKey: UITransitionContextViewKey.to)
let view = UIView(frame: CGRect.zero)
```

### Language
Sử dụng ngôn ngữ là tiếng anh Mỹ chuẩn Math Apple's API .

**Preferred**:
```swift
let color = "red"
```

**Not Preferred**:
```swift
let colour = "red"
```

### Initializers
Tên của hàm khởi tạo phải tương ứng với thuộc tính được lưu trữ , Dùng self để phân biệt đối số của hàm khởi tạo với thuộc tính được lưu trữ .

**Preferred**:
```swift
public struct Person {
   public let name: String
   public let phoneName: String

   // GOOD
   public init(name: String, phoneNumber: String) {
      self.name = name
      self.phoneNumber = phoneNumber
   }
}
```
**Not Preferred**:
```swift
public struct Person {
  public let name: String
  public let phoneNumber: String

  // AVOID.
  public init(name otherName: String, phoneNumber otherPhoneNumber: String) {
    name = otherName
    phoneNumber = otherPhoneNumber
  }
}
```

### Static and Class Properties

Thuộc tính static và class trả về các kiểu khai báo không được ghi kèm theo tên của kiểu đó .

**Preferred**:
```swift
public class UIColor {
  public class var red: UIColor {                // GOOD.
    // ...
  }
}

public class URLSession {
  public class var shared: URLSession {          // GOOD.
    // ...
  }
}
```
**Not Preferred**:
```swift
public class UIColor {
  public class var redColor: UIColor {           // AVOID.
    // ...
  }
}

public class URLSession {
  public class var sharedSession: URLSession {   // AVOID.
    // ...
  }
}
```

## Code Organization
- Sử dụng Extension để tổ chức code của bạn thành các khối chức năng hợp lí 
- Mỗi Extention nên được thiết lập một `// MARK: -` nói về nội dung của Extension

### Protocol Conformance
Khi protocol conformance , Hãy phân từng phần mở rộng riêng cho các protocol methods  
- Điều này giữ cho các phương thức liên quan được nhóm cùng với protocol

**Preferred**:
```swift
class MyViewController: UIViewController {
  // class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate methods
}
```

**Not Preferred**:
```swift
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all methods
}
```

### Unused Code
Các mã không sử dụng nên được xoá 

**Preferred**:
```swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  return Database.contacts.count
}
```

**Not Preferred**:
```swift
override func didReceiveMemoryWarning() {
  super.didReceiveMemoryWarning()
  // Dispose of any resources that can be recreated.
}

override func numberOfSections(in tableView: UITableView) -> Int {
  // #warning Incomplete implementation, return the number of sections
  return 1
}

override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  // #warning Incomplete implementation, return the number of rows
  return Database.contacts.count
}
```

### Minimal Imports
Chỉ nhập các mo-đun sử dụng . 
- Ví dụ : không nhập `UIKit` khi nhập `Foundation` đã đủ và ngược lại

**Preferred**:
```swift
import UIKit
var view: UIView
var deviceModels: [String]
```

**Preferred**:
```swift
import Foundation
var deviceModels: [String]
```

**Not Preferred**:
```swift
import UIKit
import Foundation
var view: UIView
var deviceModels: [String]
```

**Not Preferred**:
```swift
import UIKit
var deviceModels: [String]
```
## Spacing

Các dấu ngoặc nhọn (`if`/`else`/`switch`/`while` etc.) luôn mở trên cùng 1 dòng với câu lệnh nhưng đóng trên một dòng mới .

**Preferred**:
```swift
if user.isHappy {
  // Do something
} else {
  // Do something else
}
```

**Not Preferred**:
```swift
if user.isHappy
{
  // Do something
}
else {
  // Do something else
}
```

- Nên có 1 dòng trống giữa các phương thức để nhìn rõ ràng và tổ chức code trực quan .
- Không được có dòng trống sau dấu ngoặc nhọn mở hoặc trước dấu ngoặc đóng .
- Dấu 2 chấm luôn không có khoảng cách ở bên trái và một khoảng trắng ở bên phải . Một số ngoại lệ : toán tử bậc ba `? :` , `[:]`, `#selector` , `addTarget(_:action:)`.

**Preferred**:
```swift
class TestDatabase: Database {
  var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```

**Not Preferred**:
```swift
class TestDatabase : Database {
  var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```
- Các dòng dài nên có khoảng 70 kí tự .
- Tránh các khoảng trắng ở cuối dòng .

- Tương tự khoảng trắng với dấu phẩy 

**Preferred**:
```swift
let numbers = [1, 2, 3]
```

**Not Preferred**:
```swift
let numbers = [ 1, 2, 3 ]
```

## Comments

- Comment trước Outlet 
```
// MARK - Outlet
```
- Comment khi khai báo biến
```
// MARK - Variables And Properties
```
- Comment trước Outlet Action
```
// MARK - Action
```
- Comment trước Function
```
// MARK - Function
```
- Comment Life Cycle
```
// MARK - Life Cycle
```
Life Cycle gồm : LoadView , ViewDidLoad , viewWillAppear , viewDidAppear , viewWillDisappear , viewDidDisappear

- Khi cần thiết , hãy sử dụng 'comment' để giải thích tại sao đoạn mã này lại làm được điều đó .

- Tránh sử dụng các chú thích kiểu (`/* ... */`) . Ưu tiên sử dụng dấu gạch kép hoặc ba .

## Classes and Structures

Remember, structs have value semantics. Use structs for things that do not have an identity. An array that contains [a, b, c] is really the same as another array that contains [a, b, c] and they are completely interchangeable. It doesn't matter whether you use the first array or the second, because they represent the exact same thing. That's why arrays are structs.

Classes have reference semantics. Use classes for things that do have an identity or a specific life cycle. You would model a person as a class because two person objects are two different things. Just because two people have the same name and birthdate, doesn't mean they are the same person. But the person's birthdate would be a struct because a date of 3 March 1950 is the same as any other date object for 3 March 1950. The date itself doesn't have an identity.

Sometimes, things should be structs but need to conform to AnyObject or are historically modeled as classes already (NSDate, NSSet). Try to follow these guidelines as closely as possible.

- Bỏ qua định nghĩa ta đi đến với ví dụ cụ thể :

```swift
class Circle: Shape {
  var x: Int, y: Int
  var radius: Double
  var diameter: Double {
    get {
      return radius * 2
    }
    set {
      radius = newValue / 2
    }
  }

  init(x: Int, y: Int, radius: Double) {
    self.x = x
    self.y = y
    self.radius = radius
  }

  convenience init(x: Int, y: Int, diameter: Double) {
    self.init(x: x, y: y, radius: diameter / 2)
  }

  override func area() -> Double {
    return Double.pi * radius * radius
  }
}

extension Circle: CustomStringConvertible {
  var description: String {
    return "center = \(centerString) area = \(area())"
  }
  private var centerString: String {
    return "(\(x),\(y))"
  }
}
```
Ví dụ trên nói lên các quy tắc sau :
 + Chỉ định kiểu cho các thuộc tính, biến, hằng số, khai báo đối số và các câu lệnh khác có dấu cách sau dấu hai chấm nhưng không phải trước dấu hai chấm, ví dụ x: Int, và Circle: Shape.
 + Xác định nhiều biến và cấu trúc trên một dòng nếu chúng có chung mục đích / ngữ cảnh.
 + Thụt lề các định nghĩa getter và setter .
 + Không thêm các công cụ sửa đổi chẳng hạn như `internal` khi chúng đã là mặc định. Tương tự, không lặp lại công cụ sửa đổi quyền truy cập khi ghi đè một method.
 + Tổ chức chức năng bổ sung (e.g. printing) trong Extension.
 + Ẩn các chi tiết triển khai, không được chia sẻ, chẳng hạn như `centerString` bên trong Extension bằng cách sử dụng `private` kiểm soát truy cập.

### Self

- Để ngắn gọn , Hãy tránh sử dụng `self` vì swift không bắt buộc .
- Nếu Xcode bắt sử dụng thì hãy sử dụng (trong các `@escaping` đóng hoặc trong các trình khởi tạo để phân biệt các thuộc tính khỏi các đối số)

### Computed Properties
- Nếu 1 thuộc tính chỉ đọc , hãy bỏ qua mệnh get . Mệnh get chỉ được yêu cầu khi một mệnh đề đã đặt được cung cấp.

**Preferred**:
```swift
var diameter: Double {
  return radius * 2
}
```

**Not Preferred**:
```swift
var diameter: Double {
  get {
    return radius * 2
  }
}
```

## Function Declarations

Giữ cho các khai báo hàm ngắn trên một dòng bao gồm cả dấu ngoặc nhọn mở đầu : 

```swift
func reticulateSplines(spline: [Double]) -> Bool {
  // reticulate code goes here
}
```

Đối với các hàm có chữ ký dài , hãy đặt mỗi tham số trên một dòng mới và thêm một thụt lề phụ trên các dòng tiếp theo :

```swift
func reticulateSplines(
  spline: [Double], 
  adjustmentFactor: Double,
  translateConstant: Int, 
  comment: String
) -> Bool {
  // reticulate code goes here
}
```
Sử dụng `Void` thay vì `()` cho kết quả `func()` .

```swift
func updateConstraints() -> Void {
  // magic happens here
}

typealias CompletionHandler = (result) -> Void
```

**Not Preferred**:

```swift
func updateConstraints() -> () {
  // magic happens here
}typealias CompletionHandler = (kết quả) -> ()
```
## Closure Expressions

Chỉ sử dụng cú pháp bao đóng theo sau khi có một tham số biểu thức bao đóng duy nhất ở cuối danh sách đối số.

**Preferred**:
```swift
UIView.animate(withDuration: 1.0) {
  self.myView.alpha = 0
}

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}, completion: { finished in
  self.myView.removeFromSuperview()
})
```

**Not Preferred**:
```swift
UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
})

UIView.animate(withDuration: 1.0, animations: {
  self.myView.alpha = 0
}) { f in
  self.myView.removeFromSuperview()
}
```

Các phương thức chuỗi sử dụng dấu đóng cuối phải rõ ràng và dễ đọc .Các quyết định về khoảng cách, ngắt dòng và khi nào sử dụng các đối số .

```swift
let value = numbers.map { $0 * 2 }.filter { $0 % 3 == 0 }.index(of: 90)

let value = numbers
  .map {$0 * 2}
  .filter {$0 > 50}
  .map {$0 + 10}
```
## Types
### Constants

- Luôn sử dụng `let` thay vì `var` nếu giá trị của biến sẽ không thay đổi.

Mẹo: Một kỹ thuật tốt là xác định mọi thứ bằng cách sử dụng `let` và chỉ thay đổi nó thành `var` nếu Xcode nhắc nhở!

- Để khai báo một thuộc tính kiểu như một hằng số, chỉ cần sử dụng `static let`
- Các thuộc tính kiểu được khai báo theo cách này thường được ưu tiên hơn các hằng số toàn cục vì chúng dễ phân biệt hơn với các thuộc tính .

Ví dụ :
**Preferred**:
```swift
enum Math {
  static let e = 2.718281828459045235360287
  static let root2 = 1.41421356237309504880168872
}

let hypotenuse = side * Math.root2

```

**Not Preferred**:
```swift
let e = 2.718281828459045235360287  // pollutes global namespace
let root2 = 1.41421356237309504880168872

let hypotenuse = side * root2 // what is root2?
```

### Optionals

Khai báo các biến bắt buộc `?` với các giá trị có thể `nil`

Không trồng chéo 'if' đối với các biến check 'nil'

Ví dụ :

**Preferred**:
```swift
var subview: UIView?
var volume: Double?

// later on...
if let subview = subview, let volume = volume {
  // do something with unwrapped subview and volume
}

```

**Not Preferred**:
```swift
var optionalSubview: UIView?
var volume: Double?

if let unwrappedSubview = optionalSubview {
  if let realVolume = volume {
    // do something with unwrappedSubview and realVolume
  }
}
```

### Lazy Initialization
- Cân nhắc sử dụng lazy để kiểm soát chi tiết hơn đối với thời gian tồn tại của đối tượng 
- Bạn có thể sử dụng bao đóng ngay lập tức {} ()

Ví dụ :
```swift
lazy var locationManager = makeLocationManager()

private func makeLocationManager() -> CLLocationManager {
  let manager = CLLocationManager()
  manager.desiredAccuracy = kCLLocationAccuracyBest
  manager.delegate = self
  manager.requestAlwaysAuthorization()
  return manager
}
```

### Type Annotation for Empty Arrays and Dictionaries
Đối với các Array và Dictionaries, hãy sử dụng chú thích . (Đối với một Array hoặc Dictionaries được gán cho một ký tự lớn, nhiều dòng, hãy sử dụng chú thích .)

**Preferred**:
```swift
var names: [String] = []
var lookup: [String: Int] = [:]
```

**Not Preferred**:
```swift
var names = [String]()
var lookup = [String: Int]()
```

## Memory Management
Code không nên tạo các chu trình tham chiếu. Phân tích đồ thị đối tượng của bạn và ngăn chặn các chu kỳ mạnh với `weak` và `unowned` tham chiếu. Ngoài ra, hãy sử dụng các kiểu giá trị ( `struct`, `enum`) để ngăn chặn hoàn toàn các chu kỳ.

### Extending object lifetime

Kéo dài thời gian tồn tại của đối tượng bằng cách sử dụng `[weal self]` và `guard let self = self else {return}` . `[weak self]` được ưu tiên hơn `[unowned self]`.

**Preferred**
```swift
resource.request().onComplete { [weak self] response in
  guard let self = self else {
    return
  }
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**Not Preferred**
```swift
// might crash if self is released before response returns
resource.request().onComplete { [unowned self] response in
  let model = self.updateModel(response)
  self.updateUI(model)
}
```

**Not Preferred**
```swift
// deallocate could happen between updating the model and updating UI
resource.request().onComplete { [weak self] response in
  let model = self?.updateModel(response)
  self?.updateUI(model)
}
```
### Access Control
- Chú thích kiểm soát truy cập đầy đủ  . Using `private` and `fileprivate` , tuy nhiên , một cách thích hợp , làm tăng thêm sự rõ ràng và thúc đẩy sự đóng gói
- Chỉ sử dụng `open` , `public` , and `internal` khi bạn yêu cầu đặc tả kiểm soát truy cập đầy đủ 
- Sử dụng kiểm soát truy cập làm công cụ xác định thuộc tính hàng đầu, Những thứ duy nhất nên đến trước kiểm soát truy cập là `static` hoặc các thuộc tính như 
`@IBAction`, `@IBOutlet` và `@discardableResult`

**Preferred**:
```swift
private let message = "Great Scott!"

class TimeMachine {  
  private dynamic lazy var fluxCapacitor = FluxCapacitor()
}
```

**Not Preferred**:
```swift
fileprivate let message = "Great Scott!"

class TimeMachine {  
  lazy dynamic private var fluxCapacitor = FluxCapacitor()
}
```

## Control Flow 

Dùng `for-in` hơn dùng `while`

**Preferred**:
```swift
for _ in 0..<3 {
  print("Hello three times")
}

for (index, person) in attendeeList.enumerated() {
  print("\(person) is at position #\(index)")
}

for index in stride(from: 0, to: items.count, by: 2) {
  print(index)
}

for index in (0...3).reversed() {
  print(index)
}
```

**Not Preferred**:
```swift
var i = 0
while i < 3 {
  print("Hello three times")
  i += 1
}


var i = 0
while i < attendeeList.count {
  let person = attendeeList[i]
  print("\(person) is at position #\(i)")
  i += 1
}
```

## Golden Path

Khi viết Code với `if`, Không lồng các câu lệnh `if`. Các `guard` sinh ra để làm việc này.

**Preferred**:
```swift
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {
  guard let context = context else {
    throw FFTError.noContext
  }
  guard let inputData = inputData else {
    throw FFTError.noInputData
  }

  // use context and input to compute the frequencies
  return frequencies
}
```

**Not Preferred**:
```swift
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {
  if let context = context {
    if let inputData = inputData {
      // use context and input to compute the frequencies

      return frequencies
    } else {
      throw FFTError.noInputData
    }
  } else {
    throw FFTError.noContext
  }
}
```

**Preferred**:
```swift
guard 
  let number1 = number1,
  let number2 = number2,
  let number3 = number3 
else {
  fatalError("impossible")
}
// do something with numbers
```

**Not Preferred**:
```swift
if let number1 = number1 {
  if let number2 = number2 {
    if let number3 = number3 {
      // do something with numbers
    } else {
      fatalError("impossible")
    }
  } else {
    fatalError("impossible")
  }
} else {
  fatalError("impossible")
}
```

## End See you again
















































