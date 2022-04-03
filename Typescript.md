- **Описание атрибутом tsconfig.json:** https://gist.github.com/KRostyslav/82a25c469ffa6652825d58537ac6bc22
- **Typescript style guide:** https://github.com/ymaps/codestyle/blob/master/typescript.md
- **tsconfig:** https://www.typescriptlang.org/tsconfig
----------------------------------------------------------------
- **Typescript interview questions:** https://github.com/aershov24/typescript-interview-questions
- **Typescript interview questions:** https://github.com/FedorovAlexander/typescript-interview-questions-ru
- **Typescript interview questions:** https://github.com/Devinterview-io/typescript-interview-questions
- **Typescript interview questions:** https://github.com/dotnetcrunch/typescript-interview-questions
----------------------------------------------------------------
- Во-первых, следует отметить, что TypeScript - это строго типизированный и компилируемый язык, чем, возможно, будет ближе к программистам Java, C# и других строго типизированных языков. Хотя на выходе компилятор создает все тот же JavaScript, который затем исполняется браузером. Однако строгая типизация уменьшает количество потенциальных ошибок, которые могли бы возникнуть при разработке на JavaScript.
- Во-вторых, TypeScript реализует многие концепции, которые свойствены объектно-ориентированным языкам, как, например, наследование, полиморфизм, инкапсуляция и модификаторы доступа и так далее.
- https://github.com/Microsoft/TypeScript
----------------------------------------------------------------
- ```npm install -g typescript```
- ```tsc -v```
- ```tsc app.ts```
- **Опция --watch**, а также ее сокращенная версия -w автоматически перекомпилирует файлы typescript, если в них были внесены какие-либо изменения. Благодаря чему не надо при каждом малейшем изменении вручную вводить команду в консоль для перекомпиляции.
```tsc -w app.ts```
- **Версия ECMAScript**
С помощью параметра –-target или его сокращенной версии –t можно задать версию стандарта JavaScript, в которую будет компилироваться код TypeScript. Этот параметр может принимать следующие значения: "ES3" (по умолчанию), "ES5", "ES6" / "ES2015", "ES7" / "ES2016", "ES2017", "ES2018", "ES2019", "ES2020" или "ESNext":
```tsc app.ts -t ES5```
- **Удаление комментариев**. По умолчанию в файлы javascript переходят все комментариии, которыми снабжен код в файлах TS. Удаление комментариев при компиляции осуществляется с помощью параметра –-removeComments:
```tsc app.ts --removeComments```
- **Установка каталога.** С помощью параметра --outDir можно задать папку для хранения скомпилированных файлов js:
```tsc --outDir D:\ts\js app.ts```
- Объединение файлов
Если у нас несколько файлов TS, то с помощью параметра --outFile их можно объединить в один файл js:
```tsc --outFile output.js app.ts hello.ts```
- **Тип модуля**. С помощью параметра --module, либо -m можно указать тип модуля, который будет использоваться для компиляции. Эта опция может принимать следующие значения: "None", "CommonJS" (значение по умолчанию, если задана версия ECMAScript "ES3" или "ES5"), "AMD", "System", "UMD", "ES2015", "ES2020" и "ESNext".
```tsc -m commonjs app.ts```
- **Несколько параметров**. Если надо задать несколько параметров, то они и их значения последовательно перечисляются через пробел.
```tsc -t ES5 --outDir js -m commonjs app.ts```
- И чтобы посмотреть все доступные параметры и справку по ним, можно воспользоваться параметром -h:
```tsc -h```
----------------------------------------------------------------
***tsconfig.json:***
- include
- lib
- module
- outDir
- strict
- target

- Флаг "Noimplicitany"
----------------------------------------------------------------
***tslint.json:***

- **TSLint** is an extensible static analysis tool that checks TypeScript code for readability, maintainability, and functionality errors. It is widely supported across modern editors & build systems and can be customized with your own lint rules, configurations, and formatters. 
----------------------------------------------------------------
- **Аннотация типов** и **автоматическое выведение типов**
- **Литерал типа** - ...
- **Сигнатура индексов** (`[key: T] : U`) - для этого ключа типа Т все значения должны иметь значения типа U. Тип Т - должны быть совместим с string/number.
- **Псведоним типа** 
```
type Age = number;
type Person = {
    age: Age
}
```
- **Гетерогенный Enum** - ...
- **Константный enum** - ...
----------------------------------------------------------------
Типы:

- Unknown
- Any
- Void
- Undefined
- Null
- Number
- BigInt
- Boolean
- String
- Symbol
- Object
- Number Enum
- String Enum
- Unique Enum
- Array
- Function
- Constructor
- Tuple
- Never
----------------------------------------------------------------
```
class User {
    name: string;
    constructor(_name: string) {          
        this.name = _name;
    }
}

const tom : User = new User("Том");
```
----------------------------------------------------------------
- С помощью файла **tsconfig.json** можно настроить проект TypeScript. В частности, этот файл выполняет следующие задачи:
устанавливает корневой каталог проекта TypeScript
выполняет настройку параметров компиляции
устанавливает файлы проекта

```
{
    "compilerOptions": {
        "target": "es5",
        "removeComments": true,
        "outDir": "js",
        "sourceMap": true
        "outFile": "main.js"
    }
}
```

- С помощью секции files можно установить набор включаемых в проект файлов:
- Параметр exclude, наоборот, позволяет исключить при компиляции определенные файлы:
```
{
    "compilerOptions": {
        "target": "es5",
        "removeComments": true,
        "outFile": "../../built/local/tsc.js"
    },
    "files":[
        "app.ts",
        "interfaces.ts",
        "classes.ts",
    ],
    "exclude":[
        "wwwroot",
        "node_modules"
    ]
}
```
- При этом следует учитывать, что если в файле одновременно будут заданы обе секции files и exclude, то секция exclude будет игнорироваться.
- Параметр compileOnSave при значении true указывает используемой IDE сгенерировать все файлы js при каждом сохранении файлов TypeScript.
- Файл tsconfig.json используется при компиляции в том случае, если компилятору не передаются названия файлов, которые надо скомпилировать. В этом случае компилятор TypeScript просматривает текущий каталог, ищет в нем файл tsconfig.json и затем при компиляции использует те параметры, которые определены в этом файле. Если же компилятору передаются названия файлов, например, tsc app.ts, то файл tsconfig.json игнорируется.
- 
```
var z;
```

```
let z;
```

- Применение let является более предпочтительным, поскольку позволяет избежать ряд проблем, связанных с объявлением переменных. В частности, с помощью var мы можем определить два и более раз переменную с одним и тем же именем:
```
var x = "hello";
console.log(x);
var x = "work";
console.log(x);
```

- Если программа большая, то мы можем не уследить за тем, что такая переменная уже объявлена, что является источником потенциальных ошибок. Подобную проблему позволяет решить let:
```
let x = "hello";
console.log(x);
let x = "work"; // здесь будет ошибка, так как переменная x уже объявлена
console.log(x);
```

```
let x = "hello";
console.log(x);
var x = "work"; // здесь будет ошибка, так как переменная x уже объявлена
console.log(x);
```

- Определив переменную, мы можем установить ее значение и в процессе работы программы поменять его на другое:
```
let z = 6;
z = 8;
```

```
const z = 6;
z = 8;  // здесь ошибка - нельзя изменить значение константы z
```

- Здесь определены две переменных с одним и тем же именем. Но ошибки нет, поскольку они определены в разных областях видимости.
```
let x = 10;
{
    let x = 25;
    console.log(x); // 25
}
console.log(x); // 10
```
----------------------------------------------------------------
```
let p = {...o, k: 3}
```

```
let a: any = 100;
let b: any = ['danger'];
let c = a + b; // any
```

```
let d: boolean = true;
let e: true = true;
let f: true = false; // Error
```

```
const c = 100;
let e: number = 100;
let f: 3.14 = 3.14;
let g: 3.14 = 6; // Error
```

```
let oneMillion = 1_000_000;
```

```
let g: 'john' = 'zoe'; // Error
```

```
let a = Symbol('a')
const f: unique symbol = Symbol('f');
let g: unique symbol = Symbol('f');  // Error. Should be 'const'
```

```
let b = {
    c: {
        d: 'f'
    }
}; // {c: {d: string}}
```

```
let a : {b: number} = {
    b: 12
};
```

```
let c : { firstName: string, lastName: string} = {
    firstName: 'a',
    lastName: 'b'
}
```

```
class Person {
    constructor(
        public  firstName: string, // аналог: this.firstName  = firstName
        public  secondName: string 
    ) {}
}
```
----------------------------------------------------------------
**Tuple:**
```
const skill: [number, string] = [1, "Dev"];

const [id, skillName] = skill;
```

```
const skill: [number, string] = [1, "Dev"];
const id = skill[0];
const skillName = skill[1];
// const q = skill[2]; - ERROR

skill.push('test'); // Ok
skill.pop();
```

```
const arr: [number, string, ...boolean[]] =  [1, "test", true, false, true];
```

```
const skill: readonly [number, string] = [1, "Dev"];
skill[0] = [2, "Dev2"]; // Error
```

```
const skill: ReadonlyArray<string> = ["1", "Dev"];
skill.push("2"); // Error
```
----------------------------------------------------------------
**Enum:**

```
enum StatusCode {
    Success,
    Failed,
    InProgress
}
```

```
enum StatusCode {
    Success = 1,
    Failed = 5,
    InProgress
}
```

```
function compute() {
    return 3;
}

enum Roles {
    Admin = 2,
    User = compute()
}
```
----------------------------------------------------------------
**Продвинутые типы данных:**

**Union:**
```
function log(id: string | number | boolean) {
    console.log(id);
}
```

**Сужение типов:**
```
function log(id: string | number | boolean) {
    if (typeof id === 'string) {
        console.log(id);
    } else if (typeof id === 'number) {
        console.log(id);
    } else {
        console.log(id);
    }
}
```

```
function logError(error: string | string[]) {
    if (Array.isArray(error)) {
        console.log(id);
    } else {
        console.log(id);
    }
}
```

```
function logObject(obj: { a: number} | {b: number}) {
    if ('a' in obj) {
        console.log(obj.a);
    } else {
        console.log(obj.b);
    }
}
```

**Literial types:**
```
function fetchWithAuth(url: string, method: 'post' | 'get'): 1 | -1 {
    return -1;
}

fetchWithAuth('s', 'post');
let method = 'post';
fetchWithAuth('s', method as 'post');
```

```
function fetchWithAuth(url: string, method: 'post' | 'get'): 1 | -1 {
    return 3; // error
}
```

**Type alias:**
```
type httpMethod = 'post' | 'get';
type myStringAlias = string;
```

```
type User = {
    name: string,
    age: number
};

type Role = {
    roleId: number
};

type UserWithRole = User & Role;
let userWithRole: UserWithRole = {
    name: 'user',
    age: 18,
    roleId: 10
};
```
