# Kotlin Collection Functions

The Kotlin standard library offers a broad variety of functions for performing operations on collections. This includes simple operations, such as getting or adding elements, as well as more complex ones including search, sorting, filtering, transformations, and so on.

# Contents
 - [distinct](#distinct) 
 - [joinToString](#jointostring)
 - [reduce](#reduce)
 - [all](#all)
 - [single](#single)
 - [find](#find)
 - [chunked](#chunked)
 - [copyInto](#copyinto)
 - [Changing type of collection to other](#changing-type-of-collection-to-other)
 - [associateBy](#associateby)
 - [Zip, Unzip](#zip-unzip)
 - [filter](#filter)
 - [union](#union)
 - [intersect](#intersect)
 - [map](#map)
 - [flatMap](#flatmap)
 - [binarySearch](#binarysearch)
 - [groupBy](#groupby)
 - [sorted, sortedDescending](#sorted-sorteddescending)
 - [sortedBy](#sortedby)
 - [reversed, asReversed](#reversed-asreversed)
 - [retainAll](#retainall)
 - [removeFirst, removeLast, removeAll](#removefirst-removelast-removeall)
 - [partition](#partition)
 - [sum()](#sum)
 - [sumBy](#sumby)
 - [maxOrNull, minOrNull](#maxornull-minornull)
 - [maxByOrNull, minByOrNull](#maxbyornull-minbyornull)
 - [maxWithOrNull](#maxwithornull)

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

## `distinct` 
Retreive Distinct Items from Collection
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

## `joinToString` 
Convert an array or list to a string

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

## `Reduce` 
Transform a collection into a single result

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

## `All` 
Find if all elements are satisfying a particular condition

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

## `Single` 
Find a single element based on a certain condition

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

## `Find` 
Find a particular element based on a certain condition

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

## `chunked` 
Break your list into multiple sublists of smaller size

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

## `copyInto` 
Making copies of the array

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

## `associateBy` 
Associating the data using some key

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

## `Zip, Unzip` 
Zip or Unzip a Collection

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

## `filter` 
Filter a collection based on some condition

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

## `union` 
Union of collections

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

## `intersect` 
Intersection of collections

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

## `map` 
Map a collection for transformation

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

## `flatMap` 
Flatten Collection

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

## `binarySearch` 
Perform search in collection

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

## `groupBy` 
Group elements of a collection based on some condition

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

## `sorted, sortedDescending` 
Sort a collection

```
fun sortExample() {
        val unsortedAges = listOf(1, 3, 2, 7, 5, 15, 9, 8, 20, 18, 25)

        //Automatic sorting order is ascending
        val youngestToOldestAges = unsortedAges.sorted()
        println("Youngest to oldest ages: $youngestToOldestAges")

        val oldestToYoungestAges = unsortedAges.sortedDescending()
        println("Oldest to youngest ages: $oldestToYoungestAges")
        /*Similarly, there are other functions that can be used to sort the collection based on certain conditions.
         Some of these functions are sortedArray, sortedArrayWith, sortedBy, sortedByDescending,
         sortedArraydescending, sortedWith, etc.*/
    }
```

Output:
```
Youngest to oldest ages: [1, 2, 3, 5, 7, 8, 9, 15, 18, 20, 25]
Oldest to youngest ages: [25, 20, 18, 15, 9, 8, 7, 5, 3, 2, 1]
```

## `sortedBy` 
Sort Collection by custom property

```
fun sortedByExample() {
        val products = listOf(
            Product("A1", 10, 6.90),
            Product("B1", 20, 3.45),
            Product("C1", 30, 1.05),
            Product("D1", 50, 5.05)
        )
        val sorted = products.sortedBy { it.price }
        println(sorted)
        /*[Product(name=C1, quantity=30, price=1.05),
        Product(name=B1, quantity=20, price=3.45),
        Product(name=D1, quantity=50, price=5.05),
        Product(name=A1, quantity=10, price=6.9)]*/
    }
```

Output:
```
[Product(name=C1, quantity=30, price=1.05), Product(name=B1, quantity=20, price=3.45), Product(name=D1, quantity=50, price=5.05), Product(name=A1, quantity=10, price=6.9)]
```

## `reversed, asReversed` 
Reverse a collection

```
fun reverseExample() {
        val list = listOf(1, 2, 3, 4, 5)
        println(list.reversed()) // [5, 4, 3, 2, 1]
        println(list.asReversed()) // [5, 4, 3, 2, 1]
    }
```

Output:
```
[5, 4, 3, 2, 1]
[5, 4, 3, 2, 1]
```

## `retainAll` 
Keep the specified elements only

```
fun retainExample() {
        val listOne = mutableListOf(1, 2, 3, 3, 4, 5, 6)
        val listTwo = listOf(1, 2, 3, 3, 4, 5, 6)
        val listThree = listOf(1, 2, 3, 3, 4, 5, 7)
        println(listOne.retainAll(listTwo)) // false
        println(listOne.retainAll(listThree)) // true
        println(listOne) // [1, 2, 3, 3, 4, 5]
        //you can use removeAll to remove all the elements of one collection that are present in another
        // collection.
    }
```

Output:
```
false
true
[1, 2, 3, 3, 4, 5]
```

## `removeFirst, removeLast, removeAll` 
Remove element in collection

```
fun removeExample() {
        val listOne = mutableListOf(1, 2, 3, 3, 4, 5, 6)
        val listTwo = listOf(1, 2, 3)
        val listThree = listOf(6, 7)
        println(listOne.removeFirst())  //Prints 1
        println(listOne.removeLast())   //Prints 6
        println(listOne) // Prints [2,3,3,4,5]
        println(listOne.removeAll(listTwo)) //Prints True
        println(listOne) // Prints [4,5]
        println(listOne.removeAll(listThree)) //Prints False
        println(listOne) // Prints [4,5]
    }
```

Output:
```
1
6
[2, 3, 3, 4, 5]
true
[4, 5]
false
[4, 5]
```

## `partition` 
Split array into two parts based on some condition

```
fun partitionExample() {
        val users = listOf(
            User(1, "Alan", true),
            User(2, "Bob", true),
            User(3, "Joe", false),
            User(4, "Jenny", false)
        )

        val (webDevs, nonWebDevs) = users.partition { it.webDev }
        println(webDevs) // [User(id=1, name=Alan, webDev=true), User(id=2, name=Bob, webDev=true)]
        println(nonWebDevs) // [User(id=3, name=Joe, webDev=false), User(id=4, name=Jenny, webDev=false)]
    }
```

Output:
```
[User(id=1, name=Alan, webDev=true, mobileDev=false), User(id=2, name=Bob, webDev=true, mobileDev=false)]
[User(id=3, name=Joe, webDev=false, mobileDev=false), User(id=4, name=Jenny, webDev=false, mobileDev=false)]
```

## `sum()` 
Calculate sum of element in collection

```
fun sumExample() {
        val nums = listOf(10, 20, 30)
        println(nums.sum()) // 60

        val doubles = listOf(1.05, 2.05, 3.65)
        println(doubles.sum()) // 6.75

        val products = listOf(
            Product("A", 10, 6.90),
            Product("B", 20, 3.45),
            Product("C", 30, 1.05)
        )

        val totalQuantity: Int = products.map { it.quantity }.sum()
        println(totalQuantity) //60
    }
```

Output:
```
60
6.75
60
```

## `sumBy` 
sum of specific field in List of Objects

```
fun sumByExample() {
        /*Kotlin sumBy()
        sum (and change value to Int) of all items in the normal List
        sum of specific Int field in List of Objects (no need map())
        sum of specific Int field of all values in Map of Objects (no need map())
        Why we don’t need map()?
        Look at protoype of sumBy() function:

        inline fun sumBy(selector: (T) -> Int): Int
        You can see that sumBy() receives a selector which indicates the field to be processed.*/
        val nums = listOf(10, 20, 30)
        println(nums.sumBy { it }) // 60
        println(nums.sumBy { it * 2 }) // 120

        val doubles = listOf(1.05, 2.05, 3.65)
        println(doubles.sumBy { it.roundToInt() }) // 7

        val products = listOf(
            Product("A", 10, 6.90),
            Product("B", 20, 3.45),
            Product("C", 30, 1.05)
        )

        val totalQuantity: Int = products.sumBy { it.quantity }
        println(totalQuantity) // 60

        val productsMap = mapOf(
            "a" to Product("A", 10, 6.90),
            "b" to Product("B", 20, 3.45),
            "c" to Product("C", 30, 1.05)
        )

        val totalQuantity2: Int = productsMap.map { it.value }.sumBy { it.quantity }
        println(totalQuantity2) // 60
    }
```

Output:
```
60
120
7
60
60
```

## `maxOrNull, minOrNull` 
Find max or min element in Collection

```
fun maxMinExample() {
        val simpleList = listOf(1.99, 55.4, 20.0, 99.99, 23.0, 34.2, 88.0, 72.1, 61.2, 43.9)
        val largestElement = simpleList.maxOrNull()
        println(largestElement) //99.99
        val smallestElement = simpleList.minOrNull()
        println(smallestElement) //1.99
    }
```

Output:
```
99.99
1.99
```

## `maxByOrNull, minByOrNull` 
Find max or min element based on custom property

```
fun maxMinByExample() {
        val products = listOf(
            Product("A", 10, 6.90),
            Product("B", 20, 3.45),
            Product("C", 30, 1.05)
        )
        val productWithHighestPrice = products.maxByOrNull { it -> it.price }
        println(productWithHighestPrice)

        val productWithLowestPrice = products.minByOrNull { it -> it.price }
        println(productWithLowestPrice)
    }
```

Output:
```
Product(name=A, quantity=10, price=6.9)
Product(name=C, quantity=30, price=1.05)
```

## `maxWithOrNull` 
Find first element having the largest value according to the provided comparator

```
fun maxWithExample() {
        //maxWith() returns the first element having the largest value according to the provided [comparator]
        val productList = listOf(
            Product("A", 10, 6.90),
            Product("B", 20, 3.45),
            Product("C", 30, 1.05),
            Product("D", 20, 9.05)
        )
        val productWithHighestPrice = productList.maxWithOrNull(object : Comparator<Any> {
            override fun compare(o1: Any?, o2: Any?): Int {
                val obj1: Product? = o1 as? Product
                val obj2: Product? = o2 as? Product
                safeLet(obj1, obj2) { p1, p2 ->
                    if (p1.price > p2.price) return 1
                    if (p1.price == p2.price) return 0
                    else return -1
                }
                return -1
            }
        })

        println(productWithHighestPrice)
    }

inline fun <T1 : Any, T2 : Any, R : Any> safeLet(p1: T1?, p2: T2?, block: (T1, T2) -> R?): R? {
        return if (p1 != null && p2 != null) block(p1, p2) else null
    }
```

Output:
```
Product(name=D, quantity=20, price=9.05)
```