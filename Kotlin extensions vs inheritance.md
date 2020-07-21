Kotlin Extensions vs Inheritance
=====


we usually use inheritance in our code as it is **OOP** concept. we use this concept to extend classes and add features or properties to the class.

There is another concept in a new programming language like **Kotlin** called **extension** which can add functionality to a class without extending it

Inheritance
----

Inheritance is nothing but extending a class and adding functionality to it. You can add properties (variables) as well as functions in the extending class. You can access the variables of extending ( ***Base*** ) class if they are not private ( ***protected or internal or public*** ) can override them if they are not final (open variables) or you can override the functions also

```
    open class MotorVehicle(val maxSpeed: Double, val horsePower: Int) {
        open fun getDetails(): String {
            return "$maxSpeed :: $horsePower"
        }
    }

    class Car(
        val color: String,
        maxSpeed: Double,
        horsePower: Int
    ) : MotorVehicle(maxSpeed, horsePower) {
        override fun getDetails(): String {
            return "$maxSpeed :: $horsePower :: $color"
        }
    }
```
and we can call it 
```
    var car = Car("RED", 200.50, 2000)
    println(car.getDetails())
```
> ## Inheritance Notes:
> - can add properties and override function of the base class (*** nonfinal class***)
> - you can access properties and functions from Base class

Extensions
---
adding function to a class without extending the class, and all objects of the class type will have this function.

```
class Car(val maxSpeed: Double)

fun Car.getDetails(): String {
    return "$maxSpeed"
}
```
and we can call it 
```
var car = Car(200.20)
println(car.getDetails())
```
> ## Extensions Notes:
> - can add funtion to a class and this class should not be (***non final class***)
> - extensions does not need extending base class
> ## Extensions Limitations:
> - can't access the protected variables/ functions of the class 
> - Can't add any new variable/properties in your extension functions

## how are extension functions resolved?
it is resolved statically 

example:
```
open class BaseClass()
class DerivedClass(): BaseClass()
fun BaseClass.doSomething() {
    print("BaseClass.doSomething")
}

fun DerivedClass.doSomething() {
    print("DerivedClass.doSomething")
}
```
to call it 
```
fun callFunction(base: BaseClass) {
    base.doSomething()
}

callFunction(DerivedClass())
```
> this callFunction will print ```BaseClass.doSomething``` because of the reference for this function from type base class not the derived and it is different than the inheritance which is resolved by runtime **Polymorphism** so extension function will effect on compile-time not run time.

> if we added extension function to class and we created many objects from this class, we already have this function inside all objects we created and this is why we use extensions, we want to add function to class without edit it or extend. for example, when we develop for android we use libraries that we don't have source code to edit any class and new functionality. so the solution is to use the extension.
> examples: 
> ```View.hide()``` , 
> ```Context.doSomeThing()```
> we use it to add the boilerplate code to the class once and use it everywhere.


Extensions functions are often described as being similar to static utils classes as many java codebases. let's have an example: what if we want to reverse string, we will do this using static methods like ```StringUtils.reverse(string: String)``` in kotlin using extension function could be written as ```String.reverse()```
to use examples:
> ```StringUtils.reverse("Ahmed")```

or
> ```"Ahmed".reverse()```

### Extension vs Class Method
> it is different than Class method as it is used at the runtime and also create an object in the heap and execute the function and it retained from the memory after it finishes its execution

### Extension usage:
- used for clean code and scalability 
- improving the readability of code itself
- converting object to another

## Summary

Extension Methods are useful tools to extend types that already exist in the system – either because they don't have the functionality we need or simply to make some specific area of code easier to manage.