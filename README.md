# Kotlin Collection Functions

The Kotlin standard library offers a broad variety of functions for performing operations on collections. This includes simple operations, such as getting or adding elements, as well as more complex ones including search, sorting, filtering, transformations, and so on.

## Retreive Distinct Items from Collection
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

## Convert an array or list to a string

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

## Reduce - Transform a collection into a single result

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

