# Intro to Kotlin

* labs at `git clone https://github.com/venkats/ato2019`
* declared as primary language for Android
* compiling
  * kotlinc-<lang>
  * kotlinc-jvm
  * kotlinc-js
  * kotlinc-wasm
* Run
  * `kotlin <BYTECODE>` or `java -classpath <BYTECODE>`

* `val` is immutable, `var` is not
  * 'var is keyword of shame'
  * type inference is possible
    * only for local variables, properties within classes
    * function params must have types declared
  * 
* functions (`fun <name>()`)
  * single line : `fun greet(name: String) = "Hello $name"`
    * will allow inference of return type and `return` keyword
  * multi-line
````
fun greet(name: String): String{
  return "Hello $name, how are you?"
}
````
  * if you don't declare a type, functino returns void (Unit class, NOOP)
* Nullable type
  * add '?' to return type declaration to allow null return value
  * if evauluating a method with a null type you can reference the val with a '?' to safely navgiate (safe navigation): `result?.length` prints null
  * with safe nav - Substitute null `result?.length ?: 0` returns 0.  (Elvis Operator)
* `when` expression
  * case-ish statement

## Classes
* create in as little as one line
`class Car(val year:Int, var dist: Int)`
  * var => accessible instance method changable
  * val => accessible instance method immutable
  * <no declation> => non-accessible instance method
* Uses python syntaxt to instantiate
`val car = Car(2019,0)`
* contructors
  * are all secondary, call parent primary
`constructor(year: Int) : this(year, 0) {}`
* getters and setters - see examples
* companion objects = create Factories as subclasses, etc.
