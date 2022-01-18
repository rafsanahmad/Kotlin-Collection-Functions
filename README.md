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

## `chunked` - Break your list into multiple sublists of smaller size

```
fun chunkedExample() {
        val numList = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
        val chunkedLists = numList.chunked(3)
        print(chunkedLists) // [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10]]
        println()
    }
```

Output:
```
[[1, 2, 3], [4, 5, 6], [7, 8, 9], [10]]
```

## `copyInto` - Making copies of the array

```
fun copyArray() {
        val arrayOne = arrayOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
        val arrayTwo = arrayOf(11, 12, 13, 14, 15, 16, 17, 18, 19, 20)
        arrayOne.copyInto(
            destination = arrayTwo,
            destinationOffset = 2,
            startIndex = 0,
            endIndex = 4
        )
        arrayTwo.forEach { print("$it ") } // 11 12 1 2 3 4 17 18 19 20
        println()
    }
```

Output:
```
11 12 1 2 3 4 17 18 19 20 
```

## Changing type of collection to other

```
fun changeTypeExample() {
        var uIntArray = UIntArray(5) { 1U }
        val intArray = uIntArray.toIntArray()
        intArray[0] = 0
        println(uIntArray.toList()) // [1, 1, 1, 1, 1]
        println(intArray.toList()) // [0, 1, 1, 1, 1]
    }
```

Output:
```
[1, 1, 1, 1, 1]
[0, 1, 1, 1, 1]
```

## `associateBy` - Associating the data using some key

```
fun associateByExample() {
        val contactList = listOf(
            Contact("Alan", "+9199XXXX1111"),
            Contact("Bob", "+9199XXXX2222"),
            Contact("Joe", "+9199XXXX3333"),
            Contact("Jenny", "+9199XXXX4444")
        )

        val phoneNumberToContactMap = contactList.associateBy { it.phoneNumber }
        println(phoneNumberToContactMap)
        // Map with key: phoneNumber and value: Contact
        // {
        //     +9199XXXX1111=Contact(name=Alan, phoneNumber=+9199XXXX1111),
        //     +9199XXXX2222=Contact(name=Bob, phoneNumber=+9199XXXX2222),
        //     +9199XXXX3333=Contact(name=Joe, phoneNumber=+9199XXXX3333),
        //     +9199XXXX4444=Contact(name=Jenny, phoneNumber=+9199XXXX4444)
        // }

        val phoneNumberToContactMap2 = contactList.associateBy({ it.phoneNumber }, { it.name })
        println(phoneNumberToContactMap2)
        // Map with key: phoneNumber and value: name
        // {
        //     +9199XXXX1111=Alan,
        //     +9199XXXX2222=Bob,
        //     +9199XXXX3333=Joe,
        //     +9199XXXX4444=Jenny}
        // }
    }
```

Output:
```
{+9199XXXX1111=Contact(name=Alan, phoneNumber=+9199XXXX1111), +9199XXXX2222=Contact(name=Bob, phoneNumber=+9199XXXX2222), +9199XXXX3333=Contact(name=Joe, phoneNumber=+9199XXXX3333), +9199XXXX4444=Contact(name=Jenny, phoneNumber=+9199XXXX4444)}

{+9199XXXX1111=Alan, +9199XXXX2222=Bob, +9199XXXX3333=Joe, +9199XXXX4444=Jenny}
```

## `Zip, Unzip` Collections

```
fun zipExample() {
        val listOne = listOf(1, 2, 3, 4, 5)
        val listTwo = listOf("a", "b", "c", "d", "e", "f")
        println(listOne zip listTwo) // [(1, a), (2, b), (3, c), (4, d), (5, e)]

        //zipWithNext return a list of pairs. The elements of the pair will be the adjacent elements of the collection.
        val list = listOf(1, 2, 3, 4, 5)
        println(list.zipWithNext()) // [(1, 2), (2, 3), (3, 4), (4, 5)]

        //Unzip
        val list2 = listOf("Alan" to 8, "Bob" to 10, "Joe" to 4, "Jenny" to 2)
        val (players, devSkills) = list2.unzip()
        println(players) // [Alan, Bob, Joe, Jenny]
        println(devSkills) // [8, 10, 4, 2]
    }
```

Output:
```
[(1, a), (2, b), (3, c), (4, d), (5, e)]
[(1, 2), (2, 3), (3, 4), (4, 5)]
[Alan, Bob, Joe, Jenny]
[8, 10, 4, 2]
```

## `filter` - Filter a collection based on some condition

```
fun filterExample() {
        val list = listOf(1, 2, 3, 4, 5, 6, 7, 8)
        val filteredList = list.filter { it % 2 == 0 }
        println(filteredList) // [2, 4, 6, 8]

        //Similarly, you can filter the collection based on the index of elements by using filterIndexed.

        //If you want to store the filtered elements in some collection, then you can use the filterIndexedTo:

        val list2 = listOf(1, 2, 3, 4, 5, 6, 7, 8)
        val filteredList2 = mutableListOf<Int>()
        list2.filterIndexedTo(filteredList2) { index, i -> list[index] % 2 == 0 }
        println(filteredList2) // [2, 4, 6, 8]

        //You can also find the elements that are instances of a specified type in a collection by using
        // filterIsInstance.

        val mixedList = listOf(1, 2, 3, "one", "two", 4, "three", "four", 5, 6, "five", 7)
        val strList = mixedList.filterIsInstance<String>()
        println(strList) // [one, two, three, four, five]
    }
```

Output:
```
[2, 4, 6, 8]
[2, 4, 6, 8]
[one, two, three, four, five]
```

## `union` - Union of collections

```
fun unionExample() {
        val listOne = listOf(1, 2, 3, 3, 4, 5, 6)
        val listTwo = listOf(2, 2, 4, 5, 6, 7, 8)
        println(listOne.union(listTwo)) // [1, 2, 3, 4, 5, 6, 7, 8]
    }
```

Output:
```
[1, 2, 3, 4, 5, 6, 7, 8]
```

## `intersect` - Intersection of collections

```
fun intersectionExample() {
        val listOne = listOf(1, 2, 3, 3, 4, 5, 6)
        val listTwo = listOf(2, 2, 4, 5, 6, 7, 8)
        println(listOne.intersect(listTwo)) // [2, 4, 5, 6]
    }
```

Output:
```
[2, 4, 5, 6]
```

## `map` - Map collection

```
fun mapExample() {
        val userAgeStrings =
            listOf("1", "15", "10", "32", "14", "45", "9", "16", "18", "19", "27", "24")
        //Simple map function that just converts strings to an int
        val userAgeInts = userAgeStrings.map { it.toInt() }
        //A perfect example of the filter feature here
        val userAgesThatCanDrive = userAgeInts.filter { it >= 16 }

        println("All user ages: $userAgeInts")
        println("User ages that can drive: $userAgesThatCanDrive")
    }
```

Output:
```
All user ages: [1, 15, 10, 32, 14, 45, 9, 16, 18, 19, 27, 24]
User ages that can drive: [32, 45, 16, 18, 19, 27, 24]
```

## `flatMap` - Flatten Collection

```
fun mapFlatMapExample() {
        val dataObjects = listOf(
            Items(listOf("a", "b", "c")),
            Items(listOf("1", "2", "3"))
        )

        //With flatMap, you can "flatten" multiple Data::items into one collection as shown with the items variable.
        val items: List<String> = dataObjects
            .flatMap { it.items } //[a, b, c, 1, 2, 3]
        println(items)

        //Using map, on the other hand, simply results in a list of lists.
        val items2: List<List<String>> = dataObjects
            .map { it.items } //[[a, b, c], [1, 2, 3]]
        println(items2)

        /*FLatten produces the same result as flatMap. So flatMap is a combination of the two functions, map{}
        and then flatten()*/
        val nestedCollections: List<String> = dataObjects
            .map { it.items }
            .flatten() //[a, b, c, 1, 2, 3]
        println(nestedCollections)
    }
```

Output:
```
[a, b, c, 1, 2, 3]
[[a, b, c], [1, 2, 3]]
[a, b, c, 1, 2, 3]
```

## `binarySearch` - Perform search in collection

```
fun binarySearchExample() {
        //This example uses the sort extension, so put this after it.
        val largeIntArray = arrayOf(
            4,
            9,
            2,
            19,
            1,
            3,
            2,
            6
        )
        //largeIntArray.sort()
        println("Array = ${largeIntArray.asList()}")
        println("Index of element 19: ${largeIntArray.binarySearch(19)}")
    }
```

Output:
```
Array = [4, 9, 2, 19, 1, 3, 2, 6]
Index of element 19: 3
```

## `groupBy` - Group elements of a collection based on some condition

```
fun groupByExample() {
        val list = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
        println(list.groupBy { it % 4 })
        // {
        //     1=[1, 5, 9],
        //     2=[2, 6, 10],
        //     3=[3, 7],
        //     0=[4, 8]
        // }
    }
```

Output:
```
{1=[1, 5, 9], 2=[2, 6, 10], 3=[3, 7], 0=[4, 8]}
```

##