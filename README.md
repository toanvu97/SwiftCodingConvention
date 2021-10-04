# The Official matechmobile.com Swift Style Guide.
### Updated for Swift 5

Mục tiêu của chúng tôi là rõ ràng, nhất quán và ngắn gọn, theo thứ tự đó.

## Table of Contents

* [Using SwiftLint](#using-swiftlint)
* [Naming](#naming)
  * [Prose](#prose)
  * [Delegates](#delegates)
  * [Use Type Inferred Context](#use-type-inferred-context)
  * [Generics](#generics)
  * [Class Prefixes](#class-prefixes)
  * [Language](#language)
* [Code Organization](#code-organization)
  * [Protocol Conformance](#protocol-conformance)
  * [Unused Code](#unused-code)
  * [Minimal Imports](#minimal-imports)
* [Spacing](#spacing)
* [Comments](#comments)
* [Classes and Structures](#classes-and-structures)
  * [Use of Self](#use-of-self)
  * [Protocol Conformance](#protocol-conformance)
  * [Computed Properties](#computed-properties)
  * [Final](#final)
* [Function Declarations](#function-declarations)
* [Function Calls](#function-calls)
* [Closure Expressions](#closure-expressions)
* [Types](#types)
  * [Constants](#constants)
  * [Static Methods and Variable Type Properties](#static-methods-and-variable-type-properties)
  * [Optionals](#optionals)
  * [Lazy Initialization](#lazy-initialization)
  * [Type Inference](#type-inference)
  * [Syntactic Sugar](#syntactic-sugar)
* [Functions vs Methods](#functions-vs-methods)
* [Memory Management](#memory-management)
  * [Extending Object Lifetime](#extending-object-lifetime)
* [Access Control](#access-control)
* [Control Flow](#control-flow)
  * [Ternary Operator](#ternary-operator)
* [Golden Path](#golden-path)
  * [Failing Guards](#failing-guards)
* [Semicolons](#semicolons)
* [Parentheses](#parentheses)
* [Multi-line String Literals](#multi-line-string-literals)
* [No Emoji](#no-emoji)
* [No #imageLiteral or #colorLiteral](#no-imageliteral-or-colorliteral)
* [Organization and Bundle Identifier](#organization-and-bundle-identifier)
* [Copyright Statement](#copyright-statement)
* [Smiley Face](#smiley-face)
* [References](#references)


## Using SwiftLint
Bạn có thể tham khảo và sử dụng pod 'swiftLint' để kiểm tra lỗi theo format của raywenderlich.com

## Naming 

### File Name
- Đặt tên phải rõ ràng 
- Ưu tiên rõ ràng hơn ngắn gọn 
- Viết hoa chữ cái đầu với Class , Type , Protocol . Ví dụ : `ProductionLine`
- Viết thường chữ cái đầu với tất cả thứ còn lại như tên biến , tên Component , ... Ví dụ : viewMain , buttonTap
- Đặt tên dựa trên vai trò , chức năng 
- Không dùng các thuật ngữ gây nhầm lẫn cho người đọc
- Đặt tên không được viết tắt 

Ví dụ :
File chứa 1 loại duy nhất MyType thì được đặt tên là MyType.swift
  - File tên MyType có hàm hỗ trợ cao cấp hơn cũng được đặt tên MyType.swift
  - MyType bổ sung thêm MyProtocol được đặt tên MyType+MyProtoCol.swift
  - MyType chứa thêm phần mở rộng đặt tên : MyType+Additions.swift
  - Một tệp chưa những thứ không liên quan ( Như một tập hợp các hàm toán học ) có thể đặt tên Math.swift
 
### Naming Component , Function , Actions
- Đặt tên cho các biến : Loại mục ( button, label,... ) + lời giải thích 
 Ví dụ : buttonSignUp , LabelName
- Đặt tên cho function : Động từ giải thích nhiệm vụ hoặc mục đích của nó 
 Ví dụ : verifyCredentials(), loadHomePage()
- Đặt tên cho Actions : Một động từ ở quá khứ giải thích hành động 
 Ví dụ : signUpButtonTapped()
 
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

