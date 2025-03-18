# Lecture 5 Lists, Stacks, Queues, and Priority Queues

# Data Structure

* <span data-type="text" style="font-size: 19px;">A </span>**data structure**<span data-type="text" style="font-size: 19px;"> or </span>**collection**<span data-type="text" style="font-size: 19px;"> is a collection of data organized in some fashion.</span>

  * <span data-type="text" style="font-size: 19px;">not only </span>**stores**<span data-type="text" style="font-size: 19px;"> data but also supports </span>**operations**<span data-type="text" style="font-size: 19px;"> for accessing and manipulating the data</span>

    * <span data-type="text" style="font-size: 19px;">Choosing the best data structures and algorithms for a particular task is one of the keys to developing high-performance software.</span>
* <span data-type="text" style="font-size: 19px;">In object-oriented thinking, a data structure, also known as a </span>**container**<span data-type="text" style="font-size: 19px;">, is an object that stores other objects, referred to as </span>**elements**<span data-type="text" style="font-size: 19px;">.</span>

# <span data-type="text" style="font-size: 24px;">Java Collection Framework hierarchy</span>

* <span data-type="text" style="font-size: 19px;">Java provides several data structures that can be used to organizeand manipulate data efficiently, commonly known as </span>**Java Collections Framework.**
* <span data-type="text" style="font-size: 19px;">The Java Collections Framework supports two types of containers:</span>

  * <span data-type="text" style="font-size: 19px;">One for </span>**storing**<span data-type="text" style="font-size: 19px;"> a collection of elements, simply called a </span>**collection**

    * ***Lists***<span data-type="text" style="font-size: 19px;"> store an ordered collection of elements</span>
    * ***Sets***  store a group of nonduplicate elements
    * ***Stacks***  store objects that are processed in a last-in, first-outfashion <span data-type="text" style="font-size: 19px;">后进先出</span>

    * ***Queues***  store objects that are processed in a first-in, first-outfashion <span data-type="text" style="font-size: 19px;">先进先出</span>

    * ***PriorityQueues***  store objects that are processed in the order of their priorities
  * One for storing **key/value** pairs, called a ***map***

    * Note: this is called a ***dictionary*** in Python
  * All the interfaces and classes defined in the Java Collections are grouped in the **java.util** package
  * The design of the Java Collections Framework is an excellent example of using interfaces, abstract classes, and concrete classes

    * The interfaces define the framework/general API
    * <span data-type="text" style="font-size: 19px;">The abstract classes provide partial implementation</span>

      * <span data-type="text" style="font-size: 19px;">Providing an abstract class that partially implements an interface makes it convenient for the user to write the code for the specialized containers</span>
      * **AbstractCollection**<span data-type="text" style="font-size: 19px;"> is provided for convenience</span>
      * <span data-type="text" style="font-size: 19px;">The concrete classes implement the interfaces with concrete data structures</span>
    * The **Collection** interface is the root interface for manipulating a collection of objects

      * The **AbstractCollection**class provides partial implementation for the **Collection**interface (all the methods in **Collection** except the **add**, **size**, and **iterator** methods)
    * the **Collection** nterface implements the **Iterable** interface Collection 接口实现了 Iterable 接口。

      * We can obtain an **Iterator** object for traversing elements in the collection
      * Also used by for-each loops

```java
import java.util.*;
public class TestCollection {
	public static void main(String[] args) {
	ArrayList<String> collection1 = new ArrayList<>();
	collection1.add("New York"); // add
	collection1.add("Atlanta"); 
	collection1.add("Dallas"); 
	collection1.add("Madison"); 

	System.out.println("A list of cities in collection1:");
	System.out.println(collection1);

	// the Collection interface’s contains method
	System.out.println("\nIs Dallas in collection1? "
	+ collection1.contains("Dallas")); // contains

	// the Collection interface’s remove method
	collection1.remove("Dallas"); // remove

	// the Collection interface’s size method
	System.out.println("\n" + collection1.size() + // size
	" cities are in collection1 now");

	Collection<String> collection2 = new ArrayList<>();
	collection2.add("Seattle"); 
	collection2.add("Portland"); 

	System.out.println("\nA list of cities in collection2:");
	System.out.println(collection2);

	ArrayList<String> c1 = (ArrayList<String>)
		(collection1.clone()); // clone
	c1.addAll(collection2); // addAll

	System.out.println("\nCities in collection1 or collection2:");
	System.out.println(c1);

	c1 = (ArrayList<String>)(collection1.clone());
	c1.retainAll(collection2); // retainAll
	System.out.print("\nCities in collection1 and collection2:");
	System.out.println(c1);

	c1 = (ArrayList<String>)(collection1.clone());
	c1.removeAll(collection2); // removeAll
	System.out.print("\nCities in collection1, but not in 2: ");
	System.out.println(c1);
	}
}

Output:
	A list of cities in collection1:
	[New York, Atlanta, Dallas, Madison]
	
	Is Dallas in collection1? true
	
	3 cities are in collection1 now
	
	A list of cities in collection2:
	[Seattle, Portland]
	
	Cities in collection1 or collection2:
	[New York, Atlanta, Madison, Seattle, Portland]
	
	Cities in collection1 and collection2:[]
	
	Cities in collection1, but not in 2: [New York, Atlanta, 
	Madison]
```

* <span data-type="text" style="font-size: 19px;">All the concrete classes in the Java Collections Framework implement the </span>**java.lang.Cloneable**<span data-type="text" style="font-size: 19px;"> and</span>  **java.io.Serializable**<span data-type="text" style="font-size: 19px;"> interfaces except that </span>**java.util.PriorityQueue**<span data-type="text" style="font-size: 19px;"> does not implement the </span>**Cloneable**<span data-type="text" style="font-size: 19px;"> interface</span>
* Some of the methods in the **Collection** interface cannot be implemented in the concrete subclass (e.g., the read-only collections cannot add or remove)

‍
