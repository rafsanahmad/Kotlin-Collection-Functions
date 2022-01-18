# Kotlin Collection Functions

The Kotlin standard library offers a broad variety of functions for performing operations on collections. This includes simple operations, such as getting or adding elements, as well as more complex ones including search, sorting, filtering, transformations, and so on.

## Helper Class
```
data class User(
    val id: Int,
    val name: String,
    val webDev: Boolean = false,
    val mobileDev: Boolean = false
)

data class Product(val name: String, val quantity: Int, val price: Double)

class Items(val items: List<String>)

data class Contact(val name: String, val phoneNumber: String)
```

## `distinct` - Retreive Distinct Items from Collection
```
fun distinctExample() {
        // Maintain the original order of items
        val devs = arrayOf("Alan", "Jones", "Bob", "Joe", "David", "Joe")
        println(devs.distinct()) // [Alan, Jones, Bob, David]

        // Maintain the original order of items
        println(devs.toSet()) // [Alan, Jones, Bob, David]

        // Maintain the original order of items
        println(devs.toMutableSet()) // [Alan, Jones, Bob, David]

        // DO NOT Maintain the original order of items
        println(devs.toHashSet()) // [Jones, Joe, Bob, Alan, David]
    }
```
Output:

```
[Alan, Jones, Bob, Joe, David]
[Alan, Jones, Bob, Joe, David]
[Alan, Jones, Bob, Joe, David]
[Jones, Joe, Bob, Alan, David]
```

## `joinToString` - Convert an array or list to a string

```
fun joinToStringExample() {
        val someKotlinCollectionFunctions = listOf(
            "distinct", "map",
            "isEmpty", "contains",
            "filter", "first",
            "last", "reduce",
            "single", "joinToString"
        )

        val message = someKotlinCollectionFunctions.joinToString(
            separator = ", ",
            prefix = "Kotlin has many collection functions like: ",
            postfix = "and they are awesome.",
            limit = 3,
            truncated = "etc "
        )

        println(message)
    }
```

Output:
```
Kotlin has many collection functions like: distinct, map, isEmpty, etc and they are awesome.
```

## `Reduce` - Transform a collection into a single result

```
fun reduceExample() {
        // NOTE: If the list is empty, then it will throw a RuntimeException
        val numList = listOf(1, 2, 3, 4, 5)
        val result = numList.reduce { result, item ->
            result + item
        }
        println(result) // 15
    }
```

Output:
```
15
```

## `All` - Find if all elements are satisfying a particular condition

```
fun allExample() {
        val user1 = User(id = 1, name = "Alan", webDev = true, mobileDev = false)
        val user2 = User(id = 2, name = "Joe", webDev = true, mobileDev = false)
        val user3 = User(id = 3, name = "Bob", webDev = true, mobileDev = false)
        val user4 = User(id = 4, name = "Jenny", webDev = true, mobileDev = false)

        val users = arrayOf(user1, user2, user3, user4)

        val allWebDevs = users.all { it.webDev }
        println(allWebDevs) // true

        val allMobileDevs = users.all { it.mobileDev }
        println(allMobileDevs) // false
    }
```

Output:
```
true
false
```

## `Single` - Find a single element based on a certain condition

```
fun singleExample() {
        val users = arrayOf(
            User(1, "Alan"),
            User(2, "Bob"),
            User(3, "Joe"),
            User(4, "Jenny")
        )

        val userWithId3 = users.single { it.id == 3 }
        println(userWithId3) // User(id=3, name=Joe)
    }
```

Output:
```
User(id=3, name=Joe, webDev=false, mobileDev=false)
```

## `Find` - Find a particular element based on a certain condition

```
fun findExample() {
        val users = arrayOf(
            User(1, "Alan"),
            User(2, "Bob"),
            User(3, "Joe"),
            User(4, "Jenny")
        )
        val userWithId1 = users.find { it.id == 1 }
        println(userWithId1) // User(id=1, name=Alan)
    }
```

Output:
```
User(id=1, name=Alan, webDev=false, mobileDev=false)
```

## 