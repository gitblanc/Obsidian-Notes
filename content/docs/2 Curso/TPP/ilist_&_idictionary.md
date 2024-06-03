---
title: IList y IDictionary🤠
---
## The C# Station Tutorial

###### by [Joe Mayo](http://web.archive.org/web/20160304170417/http://twitter.com/#!/JoeMayo "C# Tutorial Author")  
created 2/21/08, updated 7/6/08, 9/1/11

- [Obtained here](http://web.archive.org/web/20160304170417/http:/www.csharp-station.com/Tutorials/Lesson20.aspx)
## Lesson 20: Introduction to Generic Collections

All the way back in Lesson 02, you learned about arrays and how they allow you to add and retrieve a collection of objects. Arrays are good for many tasks, but C# v2.0 introduced a new feature called generics. Among many benefits, one huge benefit is that generics allow us to create collections that allow us to do more than allowed by an array. This lesson will introduce you to generic collections and how they can be used. Here are the objectives for this lesson:

- Understand how generic collections can benefit you
- Learn how to create and use a generic List
- Write code that implements a generic Dictionary

### What Can Generics Do For Me?

Throughout this tutorial, you've learned about types, whether built-in (_int_, _float_, _char_) or custom (_Shape_, _Customer_, _Account_). In .NET v1.0 there were collections, such as the _ArrayList_ for working with groups of objects. An _ArrayList_ is much like an array, except it could automatically grow and offered many convenience methods that arrays don't have. The problem with _ArrayList_ and all the other .NET v1.0 collections is that they operate on type _object_. Since all objects derive from the _object_ type, you can assign anything to an _ArrayList_. The problem with this is that you incur performance overhead converting value type objects to and from the _object_ type and a single _ArrayList_ could accidentally hold different types, which would cause hard to find errors at runtime because you wrote code to work with one type. Generic collections fix these problems.

A generic collection is strongly typed (type safe), meaning that you can only put one type of object into it. This eliminates type mismatches at runtime. Another benefit of type safety is that performance is better with value type objects because they don't incur overhead of being converted to and from type _object_. With generic collections, you have the best of all worlds because they are strongly typed, like arrays, and you have the additional functionality, like _ArrayList_ and other non-generic collections, without the problems.

The next section will show you how to use a generic _List_ collection.

### Creating Generic _List`<T>`_ Collections

The pattern for using a generic _List_ collection is similar to arrays. You declare the _List_, populate its members, then access the members. Here's a code example of how to use a _List_:

```cs
List<int> myInts = new List<int>();

myInts.Add(1);
myInts.Add(2);
myInts.Add(3);

for (int i = 0; i < myInts.Count; i++)
{
	Console.WriteLine("MyInts: {0}", myInts[i]);
}
````
								 
The first thing you should notice is the generic collection _List`<int>`_, which is referred to as List of int. If you looked in the documentation for this class, you would find that it is defined as _List`<T>`_, where _T_ could be any type. For example, if you wanted the list to work on _string_ or _Customer_ objects, you could define them as _List`<string>`_ or _List`<Customer>`_ and they would hold only _string_ or _Customer_ objects. In the example above, _myInts_ holds only type _int_.

Using the _Add_ method, you can add as many _int_ objects to the collection as you want. This is different from arrays, which have a fixed size. The _List`<T>`_ class has many more methods you can use, such as _Contains_, _Remove_, and more.

There are two parts of the _for_ loop that you need to know about. First, the condition uses the _Count_ property of _myInts_. This is another difference between collections and arrays in that an array uses a _Length_ property for the same thing. Next, the way to read from a specific position in the _List`<T>`_ collection, _myInts`[i]`_, is the exact same syntax you use with arrays.

The next time you start to use a single-dimension array, consider using a _List`<T>`_ instead. That said, be sure to let your solution fit the problem and use the best tool for the job. i.e. it's common to work with _byte`[]`_ in many places in the .NET Framework.

### Working with _Dictionary<TKey, TValue>_ Collections

Another very useful generic collection is the _Dictionary_, which works with key/value pairs. There is a non-generic collection, called a _Hashtable_ that does the same thing, except that it operates on type _object_. However, as explained earlier in this lesson, you want to avoid the non-generic collections and use their generic counterparts instead. The scenario I'll use for this example is that you have a list of _Customers_ that you need to work with. It would be natural to keep track of these _Customers_ via their _CustomerID_. The _Dictionary_ example will work with instances of the following _Customer_ class:

```cs
public class Customer
    {
        public Customer(int id, string name)
        {
            ID = id;
            Name = name;
        }

        private int m_id;

        public int ID
        {
            get { return m_id; }
            set { m_id = value; }
        }

        private string m_name;

        public string Name
        {
            get { return m_name; }
            set { m_name = value; }
        }
    }
```
    

The _Customer_ class above has a constructor to make it easier to initialize. It also exposes its state via public properties. It isn't very sophisticated at this point, but that's okay because its only purpose is to help you learn how to use a _Dictionary_ collection.  The following example populates a _Dictionary_ collection with _Customer_ objects and then shows you how to extract entries from the _Dictionary_:

```cs
Dictionary<int, Customer> customers = new Dictionary<int, Customer>();

    Customer cust1 = new Customer(1, "Cust 1");
    Customer cust2 = new Customer(2, "Cust 2");
    Customer cust3 = new Customer(3, "Cust 3");

    customers.Add(cust1.ID, cust1);
    customers.Add(cust2.ID, cust2);
    customers.Add(cust3.ID, cust3);

    foreach (KeyValuePair<int, Customer> custKeyVal in customers)
    {
        Console.WriteLine(
            "Customer ID: {0}, Name: {1}",
            custKeyVal.Key,
            custKeyVal.Value.Name);
    }
```

The _customers_ variable is declared as a _Dictionary<int, Customer>_.  Considering that the formal declaration of _Dictionary_ is _Dictionary<TKey, TValue>_, the meaning of _customers_ is that it is a _Dictionary_ where the key is type _int_ and the value is type _Customer_. Therefore, any time you add an entry to the _Dictionary_, you must provide the key because it is also the key that you will use to extract a specified _Customer_ from the _Dictionary_.

I created three _Customer_ objects, giving each an _ID_ and a _Name_. I'll use the _ID_ as the key and the entire _Customer_ object as the value. You can see this in the calls to _Add_, where _custX.ID_ is added as the key (first parameter) and the _custX_ instance is added as the value (second parameter).

Extracting information from a _Dictionary_ is a little bit different. Iterating through the _customers_ _Dictionary_ with a _foreach_ loop, the type returned is _KeyValuePair<TKey, TValue>_, where _TKey_ is type _int_ and _TValue_ is type _Customer_ because those are the types that the _customers_ _Dictionary_ is defined with.

Since _custKeyVal_ is type _KeyValuePair<int, Customer>_ it has _Key_ and _Value_ properties for you to read from. In our example, _custKeyVal.Key_ will hold the _ID_ for the _Customer_ instance and _custKeyVal.Value_ will hold the whole _Customer_ instance. The parameters in the _Console.WriteLine_ statement demonstrate this by printing out the _ID_, obtained through the _Key_ property, and the _Name_, obtained through the _Name_ property of the _Customer_ instance that is returned by the _Value_ property.

The _Dictionary_ type is handy for those situations where you need to keep track of objects via some unique identifier. For your convenience, here's Listing 20-1, shows how both the _List_ and _Dictionary_ collections work.

##### Listing 20-1. Introduction to Using Generic Collections with an Example of the List`<T>` and Dictionary<TKey, TValue> Generic Collections

```cs
using System;
using System.Collections.Generic;

public class Customer
{
    public Customer(int id, string name)
    {
        ID = id;
        Name = name;
    }

    private int m_id;

    public int ID
    {
        get { return m_id; }
        set { m_id = value; }
    }

    private string m_name;

    public string Name
    {
        get { return m_name; }
        set { m_name = value; }
    }
}

class Program
{
    static void Main(string[] args)
    {
        List<int> myInts = new List<int>();

        myInts.Add(1);
        myInts.Add(2);
        myInts.Add(3);

        for (int i = 0; i < myInts.Count; i++)
        {
            Console.WriteLine("MyInts: {0}", myInts[i]);
        }

        Dictionary<int, Customer> customers = new Dictionary<int, Customer>();

        Customer cust1 = new Customer(1, "Cust 1");
        Customer cust2 = new Customer(2, "Cust 2");
        Customer cust3 = new Customer(3, "Cust 3");

        customers.Add(cust1.ID, cust1);
        customers.Add(cust2.ID, cust2);
        customers.Add(cust3.ID, cust3);

        foreach (KeyValuePair<int, Customer> custKeyVal in customers)
        {
            Console.WriteLine(
                "Customer ID: {0}, Name: {1}",
                custKeyVal.Key,
                custKeyVal.Value.Name);
        }

        Console.ReadKey();
    }
}
```

Whenever coding with the generic collections, add a _using System.Collections.Generic_ declaration to your file, just as in Listing 20-1.

### Summary

Generic collections give you the best of all worlds with the strong typing of arrays and flexibility of non-generic collections. There are many more generic collections to choose from also, such as _Stack_, _Queue_, and _SortedDictionary_. Look in the _System.Collections.Generic_ namespace for other generic collections.