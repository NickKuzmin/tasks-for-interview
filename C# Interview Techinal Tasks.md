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