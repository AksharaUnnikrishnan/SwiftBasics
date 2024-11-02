# Lazy Properties

A lazy stored property is a property whose initial value is not calculated until the first time it is used


```cpp
lazy var name: String = {
  return "your name"
}()
```

In the above example, the property initialization code is contained within a closure which is passed as an argument to the lazy var declaration. When the property is first accessed, the closure is executed

1. It is a programming pattern that defers object creation, calculation or some expensive process until it is needed.
2. It can improve performance and reduce memory usage, particularly when initializing a value is costly or time consuming
3. Lazy types can be used with functions and methods


## Examples of lazy application

1. Cache mechanism:
   A lazy variable can be used to cache the result of the computation the first time it is performed and then returns the cached value for subsequent calls, this can be useful for expensive computations that are called frequently because it improves performance significantly

 ```cpp
    class CacheMechanism {
        lazy var cacheResult: Int = {
            let result = performComputation()
            return result
         }()
         func getResult() -> Int {
          return cacheResult
         }
         private func performComputation() -> Int {
             return 200
        }
  }

  let caching = CacheMechanism()
  print(caching.getResult()) // This will perform the expensive computation and cache the result
  print(caching.getResult()) // This will return result without performing the expensive computation
```


2. Properties Initialization:
    Initialize class or struct properties that rely on other properties that rely on other properties. Use a lazy var to ensure that all dependent properties are initialized before the dependent property is initialized. This can assist to avoid circular dependencies and better organizing the cpde
   
```cpp

class Point {
  let x: Int
  let y: Int

 lazy var distanceFromOrigin: Double = {
   let distance = sqrt(Double(x*x+y*y))
   return distance
 }()

 init(x: Int, y: Int) {
   self.x = x
   self.y = y
  }
}

let point = Point(x: 3, y: 4)
print(point.distanceFromOrigin)

```


3. Lazy Views:
    Using UIView, lazy initialization can be used to postepone the building of the view hierarchy until the view is actively shown on the screen

  ```cpp
lazy var label: UILabel = {
    let label = UILabel()
    // label properties
    return label
}()

 ```

4. Network Requests:
    Lazy initialization can be alos used with network requests to postpone request execution until it is actually required. This can be benificial for application that make frequent network request because it reduces unnecessart network traffic
  ```cpp
     lazy var networkResponse: String = {
        guard let url = URL(string: "add your url here") else {fatalError("error Message")}
        // Add the network codes here
        return "response value"
    }()

 ```


5. Lazy sequences:
   The use of lazy keyword in a sequence allows for a postponeof sequence operations until they are required. This is useful when you have a long sequence of items to load and dont want to do  all at once
   
```cpp
    func filterNumber() -> [Int] {
        var numbers = [1,2,3,4,5,6,7,8,9,10]
        let filteredNumbers = self.numbers.lazy.filter{$0 % 2 == 1}
        return Array(filteredNumbers)
    }
 ```
