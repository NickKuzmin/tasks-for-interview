```
class A
{
    virtual void Foo() // Virtual и Override используются с public доступом.
    {
        Console.Write("Class A");
    }
}
class B: A
{
    override void Foo() // Virtual и Override используются с public доступом.
    {
        Console.Write("Class B");
    }
}


B obj1 = new A(); // Downcast - не скомпилируется
obj1.Foo();
 
B obj2 = new B(); 
obj2.Foo();
 
A obj3 = new B();
obj3.Foo();
```
--------------------------------------------
```
public class A
{
    public virtual void Print1()
    {
        Console.Write("A");
    }
    public void Print2()
    {
        Console.Write("A");
    }
}

public class B: A
{
    public override void Print1()
    {
        Console.Write("B");
    }
}

public class C : B
{
    new public void Print2()
    {
        Console.Write("C");
    }
}

var c = new C();
A a = c;
 
a.Print2();
a.Print1();
c.Print2();
```
--------------------------------------------
```
object a = new int?();
object b = new int?();

Console.WriteLine(a == b);
```
--------------------------------------------
```
object objectString = "Int32";
string @string = "Int32";
string dynmaicStringInterned = string.Intern(typeof(int).Name);
string dynmaicStringWithoutInterning = typeof(int).Name;

Console.WriteLine(objectString == @string); // true
Console.WriteLine(objectString == @string); // true
Console.WriteLine(objectString == dynmaicStringInterned); // true
Console.WriteLine(@string == dynmaicStringInterned); // true
Console.WriteLine(@string == dynmaicStringWithoutInterning); // true
Console.WriteLine(objectString == dynmaicStringWithoutInterning); // FALSE (!)
```
--------------------------------------------
```
Console.WriteLine("A" + "B" + "C"); // "ABC"
Console.WriteLine('A' + 'B' + 'C'); // 198
```
--------------------------------------------
```
var i = 0;
var list = new[] {0, 1, 2};
var a = list.Select(x => (x + i++).ToString());

Console.WriteLine(string.Join(" ", a.ToArray())); // 0 2 4
Console.WriteLine(string.Join(" ", a.ToArray())); // 3 5 7
```
