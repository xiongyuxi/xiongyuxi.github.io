---
layout: post
title:  "New in swift3"
desc: "New in swift3"
keywords: "swift3,new, new in swift3"
date: 2016-06-12
categories: [ios]
tags: [blog]
icon: fa fa-apple
---

This is some note from WWDC 2016, what's new in swift

1.Why swift3:
    Dock is ~200,000 ines of code
    2.5x more Swift code
    15% less code to rewrite the same functionality in Swift


2.New swift website: swift.org


3.Everyone could contribute via github to help swift evolve


4.Changes in Swift3
Change in naming

Swift2

```
//Swift2 array
array.appendContentsOf([2,3,4])
array.insert(1,atIndex:0)

//Swift2 Foundation.NSURL
if url.fileURL {}
x = url.URLByAppendingPathComponent("file.txt")
```

Swift3

```
//Swift3 array
array.append(contentsOf: [2,3,4])
array.insert(1,at:0)

//Swift3 Foundation.NSURL
if url.isFileUrl {}
x = url.appendingPathComponent("file.txt")
```


Change in import objective-c

```
//Swift2
func CGContextFillPath(_: CGContext)
//Swift3
extension CGContext {
    func fillPath()
}
```


Change in generics(swift will fully import generics )

```
//Swift2
func findAnimals() {
    let request = NSFetchRequest(entityName:"Animal")
    guard let searchResults = 
                            try? context.executeFetchRequest(request) as! [Animal] {
        return
    }
    ...
    use(searchResults)
}
//Swift3
func findAnimals() {
    let request = NSFetchRequest<Animal> = Animal.fetchRequest
    guard let searchResults = try? context.fetch(request) {
        return
    }
    ...
    use(searchResults)
}
```


Change in import stringly typed objective-c constants (by using extention)

```
//Swift3
extrnsion UserDefaults {
    class let didChangeNotification: NSNotification.Name
}

center.addObserver(forName: UserDefaults.didChangeNotification, ...)
```


Change in Core Language

```
//Swift 2
func myFinction(a:Int, b:Int, c:Int){ }

myFunction(42, b: 57, c: 99)

//Swift3
func myFinction(a:Int, b:Int, c:Int){ }

myFunction(a:42, b: 57, c: 99)

```

generics

```
//Swift2
func anyCommon<T: Sequence, U: Sequence
                where T.Element: Equatable, 
                      T.Element == U.Element
               >(lhs: T, rhs: U) -> Bool {

//Swift3
func anyCommon<T: Sequence, U: Sequence>(lhs: T, rhs: U) -> Bool
    where T.Element: Equtable, T.Element == U.Element {

```


Warn on unused results by default

```
func plusOne(_ a: Int) -> Int {
    return a+1
}

plusOne(x) // Swift3 will warn unused
```


Change in type 

```
//Swift2
let ptr : UnsafeMutablePointer<Int> = nil

if ptr != nil {
    ptr.memory = 42
}

//Swift3
let ptr : UnsafeMutablePointer<Int>? = nil

ptr?.memory = 42
```

Change in IUO

```
//Swift2
func f(value: Int!){
    let x = value + 1           //x:Int - force unwrapped
    let y = value               //y:Int!

    let array = [value,42]      //[Int, Int!, Int?...]
    use(array)
}

//Swift3
func f(value: Int!){
let x = value + 1           //x:Int - force unwrapped
let y = value               //y:Int?

let array = [value,42]      //[Int?]
let array = [value!,42]      //[Int]

use(array)
}
```

Change in collection indexing model

```
//Swift2
i = collection.startIndex

next = i.successor()
//Swift3
i = collection.startIndex

next = i.successor(after: i)
```

Change in floating point and numerics

```
//Swift2
let v = 2 * Float(M_PI)

return x * CGFloat(M_PI) /180
//Swift3
let v = 2 * Float.pi

return x * .pi /180
```

