- title : History of C#
- description : 
- author : Andreas Schlapsi
- theme : night
- transition : default

***

# History of C#

<small>Andreas Schlapsi / [@aschlapsi](http://twitter.com/aschlapsi)</small>

***

Andreas Schlapsi ([@aschlapsi](http://twitter.com/aschlapsi))

C# since 2002

***

## January 2002

- Subversion was still replacing CVS
- Euro banknotes and coins become legal tender in 12 member states of the EU

***

## January 2002

![Bush and Schröder](images/Bush_and_Schroeder.jpg)

***

## January 2002

Microsoft releases the first version of the .NET framework with its new language C#

***

## C# 1.0 - Key Features

### Managed Code (.NET)
- IL Code (Intermediate Language)
- Common Language Runtime (Visual Basic.NET, J#, F#, ...)
- Base Class Library
- Garbage Collector

***

## C# 1.0 - Key Features

### OOP (classes)
- like Java
- no multiple inheritance

***

## C# 1.0 - Key Features

### Properties

    [lang=cs]
    public class ExampleClass
    {
        private int _number;

        public int Number
        {
            get { return _number; }
            set { _number = value; }
        }
    }

***

## C# 1.0 - Key Features

### Delegates and Events

Delegate: data structure that refers to either a static method, or an object and an instance method of its class

***

## C# 1.0 - Key Features

### Delegates and Events

    [lang=cs]
    public delegate int ChangeInt(int x);

    public class ExampleClass
    {
        public static int DoubleIt(int n)
        {
            return n * 2;
        }

        public void DoSomething()
        {
            ChangeInt myDelegate = new ChangeInt(DoubleIt);
            Console.WriteLine("{0}", myDelegate(5));
        }
    }

***

## C# 1.0 - Demo: Counter1

***

## November 2005

### C# 2.0

***

## C# 2.0 - Key Features

### Generics

    [lang=cs]
    public class ExampleClass
    {
        public void Before()
        {
            ArrayList list = new ArrayList();
            list.Add(42);
            int x = 2 + (int)list[0];
        }

        public void InCSharp2()
        {
            List<int> list = new List<int>();
            list.Add(42);
            int x = 2 + list[0];
        }
    }

***

## C# 2.0 - Key Features

### Anonymous Methods

    [lang=cs]
    public delegate int ChangeInt(int x);

    public class ExampleClass
    {
        public void DoSomething()
        {
            ChangeInt myDelegate = new ChangeInt(
                delegate(int x)
                {
                    return x * 2;
                }
            );
            Console.WriteLine("{0}", myDelegate(5));
        }
    }

***

## C# 2.0 - Key Features

### Nullable Types

- Reference Types
    - reference to object on heap
    - can be null
- Value Types
    - object on stack or embedded
    - can not be null

***

## C# 2.0 - Key Features

### Nullable Types

    [lang=cs]
    public class ExampleClass
    {
        public void DoSomething()
        {
            int? nullableInt = 42;
            Nullable<int> int2 = null;

            if (nullableInt.HasValue)
            {
                Console.WriteLine(nullableInt.Value);
            }
        }
    }

***

## C# 2.0 - Key Features

### Iterators

    [lang=cs]
    public interface IEnumerable<T>
    {
        IEnumerator<T> GetEnumerator();
    }

    public interface IEnumerator<T> : IDisposable
    {
        T Current { get; }
        void MoveNext();
        void Reset();
    }

***

## C# 2.0 - Key Features

### Iterators

    [lang=cs]
    public class ExampleClass
    {
        public void DoSomething()
        {
            List<string> list = new List<string>();
            list.Add("Hello");
            list.Add("World");
            IEnumerable<string> enumerable = list;

            foreach(string str in enumerable)
                Console.WriteLine(str);
        }
    }

***

## C# 2.0 - Key Features

### Iterators

    [lang=cs]
    public class ExampleClass
    {
        public void DoSomething()
        {
            foreach(int str in Iterate())
                Console.WriteLine(str);
        }

        public IEnumerable<int> Iterate()
        {
            yield return 1;
            yield return 2;
            yield return 3;
            yield return 4;
        }
    }

***

## C# 2.0 - Demo: Counter2

***

## C# 2.0 - Demo: IteratorExample

***

## November 2007

### C# 3.0

***

## C# 3.0 - Key Features

### Lambda Expressions

    [lang=cs]
    public delegate int ChangeInt(int x);

    public class ExampleClass
    {
        public void DoSomething()
        {
            ChangeInt myDelegate = x => x * 2;
            Console.WriteLine("{0}", myDelegate(5));
        }
    }

***

## C# 3.0 - Key Features

### Extension Methods

"Add" methods to existing types without creating a new derived type, recompiling, or otherwise modifying the original type.

***

## C# 3.0 - Key Features

### Extension Methods

    [lang=cs]
    namespace Extensions
    {
        public static class StringExtensions
        {
            public static int WordCount(this string str)
            {
                return str.split(new char[] { ' ', '.', '?' },
                                 StringSplitOptions.RemoveEmptyEntries).Length;
            }
        }
    }

***

## C# 3.0 - Key Features

### Extension Methods

    [lang=cs]
    using Extensions;

    public class ExampleClass
    {
        public void DoSomething()
        {
            string s = "Hello Extension Methods";
            int i = s.WordCount();
            Console.WriteLine(i);
        }
    }

***

## C# 3.0 - Key Features

### Expression Trees - Parsing

    [lang=cs]
    Expression<Func<int, bool>> exprTree = num => num < 5;

    ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];
    BinaryExpression operation = (BinaryExpression)exprTree.Body;
    ParameterExpression left = (ParameterExpression)operation.Left;
    ConstantExpression right = (ConstantExpression)operation.Right;

    Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",
                      param.Name, left.Name, operation.NodeType, right.Value);

***

## C# 3.0 - Key Features

### Expression Trees - Compiling

    [lang=cs]
    Expression<Func<int, bool>> exprTree = num => num < 5;
    Func<int, bool> result = exprTree.Compile();
    Console.WriteLine(result(4));

***

## C# 3.0 - Key Features

### Anonymous Types

    [lang=cs]
    var v = new { Amount = 108, Message = "Hello" };
    Console.WriteLine(v.Amount + v.Message);

***

## C# 3.0 - Key Features

### Implicit Typing (Type Inferencing)

    [lang=cs]
    //int i = 5;
    var i = 5;
    //string s = "Hello";
    var s = "Hello";
    //int[] a = new[] {0, 1, 2};
    var a = new[] {0, 1, 2};
    var anon = new { Name = "Terry", Age = 34 };

***

## C# 3.0 - Key Features

### Language Integrated Query (LINQ)

    [lang=cs]
    IEnumerable<Product> products;

    var productQuery = products
        .Where(product => product.Price > 50.0)
        .Select(product => new { product.Color, product.Price });

***

## C# 3.0 - Key Features

### Language Integrated Query (LINQ)

    [lang=cs]
    var productQuery =
        from product in products
        where product.Price > 50.0
        select new { product.Color, product.Price };

    var expr =
        from c in customers
        where c.City = "Vienna"
        select c;

***

## C# 3.0 - Demo: Counter3

***

## C# 3.0 - Demo: ExtensionMethods

***

## C# 3.0 - Demo: ExpressionTrees

***

## C# 3.0 - Demo: LinqExample

***

## April 2010

### C# 4.0

***

## C# 4.0 - Key Features

### Late Binding (dynamic)

object of type dynamic bypasses static type checking.

=> if code is not valid, errors are caught at run time!

***

## C# 4.0 - Key Features

### Late Binding (dynamic)

- Dynamic Language Runtime (IronPython)
- HTML DOM
- Reflection API
- COM Interop

***

## C# 4.0 - Key Features

### Late Binding (dynamic)

before C# 4.0:

    [lang=cs]
    ((Excel.Range)excelApp.Cells[1, 1]).Value2 = "Name";
    Excel.Range range2008 = (Excel.Range)excelApp.Cells[1, 1];

C# 4.0:

    [lang=cs]
    // access to the Value property and the conversion to
    // Excel.Range are handled by the run-time COM binder
    excelApp.Cells[1, 1].Value = "Name";
    Excel.Range range2010 = excelApp.Cells[1, 1];

***

## C# 4.0 - Demo: DynamicExample

***

## C# 4.0 - Key Features

### Named and optional arguments

***

## C# 4.0 - Demo: NamedAndOptionalArguments

***

## August 2012

### C# 5.0

***

## C# 5.0 - Key Features

### Async

***

## C# 5.0 - Demo: AsyncConsole

***

## C# 5.0 - Demo: AsyncExample

***

## ? 2015

### C# 6

- Roslyn
    - set of open-source compilers and code analysis APIs for C# and VB
    - Apache License 2.0
- [Language features in C# 6 and VB 14](https://roslyn.codeplex.com/wikipage?title=Language%20Feature%20Status&referringTitle=Documentation)
