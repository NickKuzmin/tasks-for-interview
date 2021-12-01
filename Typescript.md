- Во-первых, следует отметить, что TypeScript - это строго типизированный и компилируемый язык, чем, возможно, будет ближе к программистам Java, C# и других строго типизированных языков. Хотя на выходе компилятор создает все тот же JavaScript, который затем исполняется браузером. Однако строгая типизация уменьшает количество потенциальных ошибок, которые могли бы возникнуть при разработке на JavaScript.
- Во-вторых, TypeScript реализует многие концепции, которые свойствены объектно-ориентированным языкам, как, например, наследование, полиморфизм, инкапсуляция и модификаторы доступа и так далее.
- https://github.com/Microsoft/TypeScript\
- ```npm install -g typescript```
- ```tsc -v```
---
```
class User {
    name: string;
    constructor(_name: string) {          
        this.name = _name;
    }
}

const tom : User = new User("Том");
```
---
- Typescript style guide: https://github.com/ymaps/codestyle/blob/master/typescript.md
- 
