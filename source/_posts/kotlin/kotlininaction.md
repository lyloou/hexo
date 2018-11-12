
Only after understanding the surrounding code can you make the necessary
modifications.

Note that omitting the return type is allowed only for functions with an expression
body


Note that this example shows the
only place in the Kotlin syntax where you’re required to use semicolons: if you define
any methods in the enum class, the semicolon separates the enum constant list from the
method definitions.


The rule "the last expression in a block is the result" holds in all cases where a block
can be used and a result is expected. As you’ll see at the end of this chapter, the same
rule works for the try body and catch clauses, and chapter 5 discusses its application to
lambda expressions. But as we already mentioned in section 2.2.1, this rule doesn’t hold
for regular functions. A function can have either an expression body that can’t be a block,
or a block body with explicit return statements inside.
p41

Just like many other modern JVM languages, Kotlin doesn’t differentiate between
checked and unchecked exceptions. You don’t specify the exceptions thrown by a
function, and you may or may not handle any exceptions. This design decision is based
on the practice of using checked exceptions in Java. Experience has shown that the Java
rules often require a lot of meaningless code to rethrow or ignore exceptions, and the
rules don’t consistently protect you from the errors that can happen.
p48

Note that extension
functions don’t allow you to break encapsulation. Unlike methods defined in the class,
extension functions don’t have access to private or protected members of the class.
p61

Method overriding in Kotlin works as usual for member functions, but you can’t override
an extension function.
the function that’s called depends on the static type of the
variable being declared, not on the runtime type of the value stored in that variable.
p64-p65

Note: If the class has a member function with the same signature as an
extension function, the member function always takes precedence.
You should keep this in mind when extending the API of classes: if
you add a member function with the same signature as an
extension function that a client of your class has defined, and they
then recompile their code, it will change its meaning and start
referring to the new member function. 
p65
//TODO but how to override CharSequence.split, if the member function always takes precedence ???
```kotlin
class A(var c: String) {
    fun getDiffC(): String {
        return "---$c---"
    }

    fun getDiffD(): String {
        return "!!!!!$c!!!!!"
    }
}
fun A.getDiffD(): String = "====${this.c}===="
fun main(args: Array<String>) {
    println(A("a").getDiffC())
    println(A("d").getDiffD())
}
```


The destructuring declaration feature isn’t limited to pairs. For example, you can
assign a map entry to two separate variables, key and value , as well.
p69

The to function is an extension function. You can create a pair of any elements,
which means it’s an extension to a generic receiver: you can write `1 to "one"` , 
`"one" to 1` , `list to list.size()` , and so one.
Even though the creation of a new map may look like a special construct in Kotlin,
it’s a regular function with a concise syntax

```kotlin
1.to("one)
// ====equivalent====
1 to "one"
```
p70



local functions and extensions
Kotlin gives you a cleaner solution: you can nest the functions you’ve extracted in the
containing function. This way, you have the structure you need without any extra
syntactic overhead. (meaning fun in fun)
p75
```kotlin
class User(val id: Int, val name: String, val address: String)

fun saveUser(user: User) {
    fun validate(user: User,
                 value: String,
                 fieldName: String) {
        if (value.isEmpty()) {
            throw IllegalArgumentException(
                    "Cannot save user ${user.id}: $fieldName is empty")
        }
    }
    validate(user, user.name, "Name")
    validate(user, user.address, "Address")
// Save user to the database
}
```