- [DebuggerDisplay]
```
int? a = 42;
if (a is int valueOfA)
{
    Console.WriteLine($"a is {valueOfA}");
}
```

```
public abstract class TestBase
{
    protected Fixture Builder = new();
}
```
---------------------------------------------------
**Records:**

```
public record Person
{
    public string Name { get; set; }
    public Person(string name) => Name = name;
}
```

```
public record class Person
{
    public string Name { get; set; }
    public Person(string name) => Name = name;
}
```

```
public record struct Person
{
    public string Name { get; set; }
    public Person(string name) => Name = name;
}
```

**with:**
```
var tom = new Person("Tom", 37);
var sam = tom with { Name = "Sam" };
Console.WriteLine($"{sam.Name} - {sam.Age}"); // Sam - 37
```
