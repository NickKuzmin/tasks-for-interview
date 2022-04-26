- https://www.entityframeworktutorial.net/code-first/inheritance-strategy-in-code-first.aspx
----------------------------------------------
- **Inheritance Strategy for Code First:**
1) **Table per Hierarchy (TPH):** This approach suggests one table for the entire class inheritance hierarchy. The table includes a discriminator column which distinguishes between inheritance classes. This is a default inheritance mapping strategy in Entity Framework.
2) **Table per Type (TPT):** This approach suggests a separate table for each domain class.
3) **Table per Concrete Class (TPC):** This approach suggests one table for one concrete class, but not for the abstract class. So, if you inherit the abstract class in multiple concrete classes, then the properties of the abstract class will be part of each table of the concrete class.
----------------------------------------------
**EntityFramework (not Core):**
```
using (var context = new ArticleContext())
{
    var groupingQuery = from article in context.ArticleCommonTables
        group article by article.Type
        into g
        select new
        {
            Key = g.Key,
            Array = g.Select(x => x),
            Grouping = g
        };

    var grouping = groupingQuery.ToArray();
}
```
