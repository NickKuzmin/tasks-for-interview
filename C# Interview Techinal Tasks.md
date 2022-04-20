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
object obj = "Int32";
string s1 = "Int32";
string s2 = typeof(int).Name; // "Int32"

Console.WriteLine(obj == s1); // true
Console.WriteLine(s1 == s2); // true
Console.WriteLine(obj == s2); // FALSE (!)
```
