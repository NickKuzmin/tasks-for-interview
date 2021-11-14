```
class A
{
    virtual void Foo()
    {
        Console.Write("Class A");
    }
}
class B: A
{
    override void Foo()
    {
        Console.Write("Class B");
    }
}


B obj1 = new A();
obj1.Foo();
 
B obj2 = new B();
obj2.Foo();
 
A obj3 = new B();
obj3.Foo();
```
