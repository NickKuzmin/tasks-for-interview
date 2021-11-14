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
