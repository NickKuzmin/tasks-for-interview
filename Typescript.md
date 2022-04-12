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
- **Union** - ...
- **Literal types** - ...
- **Type aliases** - ...
- **Interface** - ...
- **Optional** - ...
- **void** - ...
- **Unknown** - ...
- **Never** - ...
- **Null** - ...
- **Type Guard** - ...
- **Индексное свойство** - ...
- **Type vs Interface** - ...
- **Optional chain** - ...
- **Void vs undefined**  - ...
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
- async/await VS Promise
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

**Interface:**
```
interface User {
    name: string,
    age: number
}

interface UserWithRole extends User {
    roleId: number;
};

let userWithRole: UserWithRole = {
    name: 'user',
    age: 18,
    roleId: 10
};
```

```
interface User {
    name: string,
    age: number
}

interface Role {
   roleId: number;
}

interface UserWithRole extends User, Role {
};

let userWithRole: UserWithRole = {
    name: 'user',
    age: 18,
    roleId: 10
};
```

```
interface User {
    name: string,
    log: (id: number) => string;
}
```

**Индексные свойство:**
```
interface UserDic {
    [index: number]: User
}

type UserDic2 = {
    [index: number]: User
}

type ud = Record<number, User>
```

**Optional:**
```
interface User {
    login: string;
    password?: string
}

const user: User = {
    login: 'userlogin'
};
```

```
type User = {
    login: string;
    password?: string
}

const user: User = {
    login: 'userlogin'
};
```

```
type User = {
    login: string;
    password: string | undefined
}

const user: User = {
    login: 'userlogin' // error: should be password = string | undefined
};
```

```
function multiply(first: number, second: number = 5) {
    return first * number;
}

multiply(10);
```

```
function multiply(first: number, second?: number = 5) {
    return first * number;
}

multiply(10);
```

```
interface User {
    password?: {
        type: 'primary' | 'secondary'
    }
}

function log(user: User) {
    const t = user.password?.type;
}

function log2(user: User) {
    const t = user.password!.type;
}

function log3(user: User) {
    const t = user.password ? user.password.type : undefined;
}

function test(param?: string) {
    const t = param ?? multiply(5);
}
```

**Void:**
```
type voidFunc = () => void;

const f1: voidFunc = () => {
    console.log('f1');
};

const f2: voidFunc = () => {
    console.log('f2');
    return 10; // Correct! Возвращаемое значение будет игнорироваться
};
```

**Unknown:**
```
let input: Unknown;

input = 3;
input = ['some', 'any'];
```

```
let input: Unknown;

let result: string = input; // compile error
```

```
let input: any;

let result: string = input; // compile okay
```

```
type U1 = unknown | number;
type U2 = unknown & number;
```

**Never:**
```
function generateError(message: string) : never {
    throw new Error(message);
}
```

```
function dumpError() : never {
    while(true) {}
}
```

```
function recursive() : never {
    return recursive();
}
```

```
const a: never = 1; // compile error
const b: void = undefined; // compile OK
```

**Приведение типов:**
```
let stringValue: string = new String('some'); // compile error
let stringValue2: string = new String('some').valueOf(); // compile OK
```

**Type Guard:**
```
function isAdmin(user: User | Admin): user is Admin {
    return (user as Admin).role !== undfined;
}
```
----------------------------------------------------------------
```
class User {
	name: string;
	
	constructor(name: string) {
		this.name = name;
	}
}
```

```
class User {
	name!: string;
}
```

```
class User {
	name: string;
	
	constructor();
	constructor(name: string);
	constructor(name?: string) {
		if (typeof name === 'string') {
			this.name = name;
		}
	}
}

var user1 = new User('Ivan');
var user2 = new User();
```

```
class User {
	name: string;
	
	constructor();
	constructor(name: string);
	constructor(age: number);
	constructor(ageOrName?: string | number) {
		if (typeof ageOrName === 'string') {
			this.name = ageOrName;
		} else if (typeof ageOrName === 'string') {
			this.age = ageOrName;
		}
	}
}

var user1 = new User('Ivan');
var user2 = new User();
var user3 = new User(33);
```


```
strictPropertyInitialization
```
------------------------------------------------------------------------------------------
```
enum PaymentStatus {
	Holded,
	Processed
}

class Payment {
	id: number;
	status: PaymentStatus;
	createdAt: Date;
	updatedAt: Date;
	
	constructor(id: number) {
		this.id = id;
		this.createdAt = new Date();
		this.status = PaymentStatus.Holded;
	}
	
	getPaymentLifeTime(): number {
		return new Date().getTime() - this.createdAt.getTime();
	}
	
	unholdPayment() {
		this.status = PaymentStatus.Processed;
	}
	
	unholdPayment2(): void {
		this.status = PaymentStatus.Processed;
	}
}
```

```
enum PaymentStatus {
	Holded,
	Processed
}

class Payment {
	id: number;
	status: PaymentStatus = PaymentStatus.Holded;
	createdAt: Date = new Date();
	updatedAt: Date;
	
	constructor(id: number) {
		this.id = id;
	}
}
```
------------------------------------------------------------------------------------------
**Перегрузки методов:**

```
class User {
	skills: string[];
	
	addSkills(skills: string): void;
	addSkills(skills: string[]): void;
	addSkills(skills: string | string[]): void {
		if (typeof skills === 'string') {
			this.skills.push(skills);
		} else {
			this.skills.concat(skills);
		}
	} 
}
```

```
function run(distance: string): string;
function run(distance: number): number;
function run(distance: number | string): number | string {
	if (typeof distance === 'string') {
		return 1;
	} else {
		return '';
	}
}
```
------------------------------------------------------------------------------------------
**Setter/Getter:**

```
class User {
	_login: string;
	
	set login(loginValue: string) {
		this._login = 'user-' + loginValue;
	}
	
	get login() {
		return this._login;
	}
}

const user = new User();
user.login = 'Ivan';
```

```
class User {
	_login: string;
	
	set login(loginValue: string | number) {
		this._login = 'user-' + loginValue;
	}
	
	get login() {
		return this._login;
	}
}
```

```
Сеттеры/Геттеры не могут быть асинхронными.
```
------------------------------------------------------------------------------------------
**Extends:**

```
class Payment {
	id: number;
	statis: string;
	
	constructor(id: number) {
		this.id = id;
	}
	
	pay() {
		this.status = 'paid';
	}
}

class PersistedPayment extends Payment {
	databaseId: number;
	paidAt: Date;
	
	constructor() {
		const id = Math.random();
		super(id);
	}
	
	save() {
		// ...
	}
	
	pay(date?: Date) {
		// this.status = 'paid';
		super.pay();
		if (date) {
			this.paidAt = date;
		}
	}
}
```

```
class Payment {
	id: number;
	statis: string;
	
	constructor(id: number) {
		this.id = id;
	}
	
	pay() {
		this.status = 'paid';
	}
}

class PersistedPayment extends Payment {
	databaseId: number;
	paidAt: Date;
	
	constructor() {
		const id = Math.random();
		super(id);
	}
	
	save() {
		// ...
	}
	
	override pay(date?: Date) {
		// this.status = 'paid';
		super.pay();
		if (date) {
			this.paidAt = date;
		}
	}
}
```

- Переопределяемый конструктор необязательно должен совпапдать с конструктором наследуемого класса.
- Конструкторы производного класса должны вызывать конструктор базового класса через super.
- Override - дополнительная проверка на этапе компиляции, если в базовом классе метод будет удален.
------------------------------------------------------------------------------------------
**Порядок вызова в конструкторе и наследовании:**

- Обращения к параметрам класса в классе наследние перед super.
- Сначала вызывается inline-инициализация поля класса, а потом уже инициализация в конструкторе.

```
class User {
	name: string = 'user';
	
	constructor() {
		console.log(this.name);
	}
}

class Admin extends User {
	name: string = 'admin';
	
	constructor() {
		console.log(this.name);
		super(); // Запрещено вызывать super после обращения к полям
	}
}
```
------------------------------------------------------------------------------------------
**Видимость свойств:**

```
class Venicle {
	private make: string;
	protected run: number;
	#price: number;
	
	set model(m: string) {
		this.#price = 100;
	}
}

class EuroVenicle extends Venicle {
	setRun(km: number) {
		this.run = km / 0.62;
	}
}
```
------------------------------------------------------------------------------------------
**Статическое свойство:**

```
class UserService {
	static db: any;
}
```

```
class UserService {
	private static db: any;
	
	static getUser(id: number) {
		return this.db.findById(id);
	}
}
```
------------------------------------------------------------------------------------------
**Контекст this:**

```
class Payment {
	private date: Date = new Date();

	getDate(this: Payment) {
		return this.date;
	}
	
	getArrowDate = () => {
		return this.date;
	}
}

const payment = new Payment();
const user = {
	id: 1,
	paymentDate: p.getDate.bind(payment),
	paymentArrowDate: p.getArrowDate
};

class PaymentPersistent extends Payment {
	save() {
		var result = super.getDate(); // OK
		return this.getArrowDate(); // NOT: super.getArrowDate();
	}
}
```
------------------------------------------------------------------------------------------
**Типизация this:**

```
class UserBuilder {
	name: string;
	
	setName(name: string): this { // this for inherited builders
		this.name = name;
		return this;
	}
	
	isAdmin(): this is AdminBuilder {
		return this is instanceof AdminBuilder;
	}
}

class AdminBuilder {
	roles: string[];
}

const result = new UserBuilder().setName('Ivan');
const result2 = new AdminBuilder().setName('Ivan');
```
------------------------------------------------------------------------------------------
**Абстрактный класс:**

```
abstract class Controller {
	abstract handle(req: any): void;
	
	handleWithLogs(req: any) {
		console.log('before');
		handle(req);
		console.log('after');
	}
}

class UserController extends Controller {
	handle(req: any): void {
		console.log(req);
	}
}
```
------------------------------------------------------------------------------------------
**Архитектура Typescript:**

- Language Service
- TSC (Standalone component)
- Core Typescript Compiler

**ts.config:**
- `files`
- `include`
- `exclude`
- `extends`
- `allowjs`
- `outdir`
- `removeComments`
- `noEmit`
- `importsNotUsedAsValues`
- `sourceMap`
- `declaration` (d.ts-файлы)
- `stringInternal` (убирает код, помеченный `@internal`)
- `nonUsedLocals`
- `nonUsedParameters`
- `@ts-ignore`
- `allowUnreachableCode`
------------------------------------------------------------------------------------------
**Generic:**

```
function logMiddleware<T>(data: T) {
	console.log(data);
	return data;
}

const result = logMiddleware('1');
const result2 = logMiddleware<string>('1');
```

```
function logMiddleware<TValue>(data: TValue) {
	console.log(data);
	return data;
}
```

```
interface IVenicle {
	run: number;
}

interface IVenicleAdvanced extends IVenicle {
	capacity: number;
}

function kmToMiles<T extends IVenicle>(venicle: T): T {
	venicle.run = venicle.run / 0.62;
	return venicle;
}
```
------------------------------------------------------------------------------------------
**Mixins:**

```
type Constructor = new (...args: any[]) => {}
type GConstructor<T = {}> = new (...args: any[]) => T

class List {
	constructor(public items: string[]) { }
}

class Accordion {
	isOpened: boolean;
}

type ListType = GConstructor<List>;
type AccordionType = GConstructor<Accordion>;

class ExtendedListClass extends List {
	first() {
		return this.items[0];
	}
}

class ExtendedListClass<TBase extends ListType & AccordionType>(Base: TBase) {
	return class ExtendedListClass extends Base {
		first() {
			return this.items[0];
		}
	}
}

class AccordionList {
	isOpened: boolean;
	constructor(public items: string[]) { }
}
```
------------------------------------------------------------------------------------------
**Манипуляция с типами:**

```
interface IUser {
	name: string;
	age: number;
}

type KeysOfUser = keyof User;

function getValue<T, K extends keyof T>(obj: T, key: K) {
	return obj[key];
}

const user: IUser = {
	name: 'Ivan',
	age: 30
};

const userName = getValue(user, 'name');
const userAge = getValue(user, 'age');
const result = getValue(user, 'name2'); // Compile error
```
------------------------------------------------------------------------------------------
**Индексное свойство:**

```
interface Role {
	name: string;
}

interface User {
	name: string;
	roles: Role[];
}

const user: User = {
	name: 'Ivan',
	roles: []
}

const nameUser = user['name'];
let roleNames: 'roles' = 'roles';

type roleType = User['roles'];
type roleType = User2[typeof roleNames];

type roleType = User['roles'][number];

const roles = ['admin', 'user', 'super-user'] as const;
type roleTypes = typeof roles[number];
```
------------------------------------------------------------------------------------------
**Conditional types:**

```
interface HttpResponse<T extends 'success' | 'failed> {
	code: number;
	data: T extends 'sucess' ? string : Error;
}

const suc: HttpResponse<'success'> = {
	code: 200,
	data: 'done'
}

const err: HttpResponse<'failed'> = {
	code: 200,
	data: new Error()
}
```

```
class User {
	id: number;
	name: string;
}

class UserPersistend extends User {
	dbId: string;
}

function getUser(id: number): User;
function getUser(dbId: string): UserPersistend;
function getUser(dbIdOrId: string | number): User | UserPersistend {
	if (typeof dbIdOrId === 'number') {
		return new User();
	} else {
		return new UserPersistend();
	}
}

type UserOrUserPersistend<T extends string | number> = T extends number ? User : UserPersistend;

function getUser2<T extends string| number>(id: T): UserOrUserPersistend<T> {
	if (typeof id === 'number) {
		return new User() as UserOrUserPersistend<T>;
	} else {
		return new UserPersistend() as UserOrUserPersistend<T>;
	}
}
```
------------------------------------------------------------------------------------------
**Infer:**

```
function runTransaction(transaction: {
	from: [string, string]
}) {
	console.log(transaction);
}

const transaction: GetFirstArg<typeof runTransaction> = {
	from: ['1', '2']
}

runTransaction(transaction);

type GetFirstArg<T> = T extends (first: infer First, ...args: any[]) => any ? First : never;
```
------------------------------------------------------------------------------------------
**Mapped types:**

```
type Modified = 'read' | 'update' | 'create';

type UserRoles = {
	customers?: Modified,
	projects?: Modified,
	adminPanel?: Modified,
}

type ModifierToAccess<Type> = {
	[Property in keyof Type]: boolean;
}

type UserAccess2 = ModifierToAccess<UserRoles>;

type UserAccess1 = {
	customers?: boolean;
	projects?: boolean;
	adminPanel?: boolean;
}
```
------------------------------------------------------------------------------------------
**Template Literal Types:**

```
type ReadOrWrite = 'read' | 'write';

type Access = `can${Capitalize<ReadOrWrite>}`;

type ReadOrWriteBulk<T> = T extends `can${infer R}` ? R : never;

type T = ReadOrWriteBulk<Access>;

type ErrorOrSuccess = 'error' | 'success';

type ReponseT = {
	result: `http${Capitalize<ErrorOrSuccess>}`
}

const a2: ReponseT = {
	result: 'httpSuccess'
}
```
------------------------------------------------------------------------------------------
**Partial/Required/Readonly:**

```
interface User {
	name: string;
	age?: number;
}

type partial = Partial<User>;
const p: partial = {};

type required = Required<User>;
type readonly = Readonly<User>;
type readonlyAndRequired = Readonly<Required<User>>;
```
------------------------------------------------------------------------------------------
**Partial/Required/Readonly:**

```
interface PaymentPersistent {
	id: number;
	sum: number;
	from: string;
	to: string;
}

type PaymentOmitType = Omit<PaymentPersistent, 'id'>;
type PaymentPickType = Pick<PaymentPersistent, 'from' | 'to'>;

type ExtractPaymentType = Extract<'from' | 'to' | Payment, string>;
type ExcludePaymentType = Exclude<'from' | 'to' | Payment, string>;
```
------------------------------------------------------------------------------------------
**ReturnType/Parameters/ConstructorParameters/InstanceType:**

```
class User {
	constructor(public id: number, public name: string) { }
}

function getData(id: number): User {
	return new User(id, 'Ivan');
}

type RT = ReturnType<typeof getData>;
type RT2 = ReturnType<() => void>;
type RT3 = ReturnType<<T>() => T>;
type RT4 = ReturnType<<T extends string>() => T>;

type PT = Parameters<typeof getdata>;
type PT2 = Parameters<typeof getdata>[0];

type CP = ConstructorParameters<typeof User>;
type IT = InstanceType<typeof User>;
```
------------------------------------------------------------------------------------------
**Awaited:**

```
type A = Awaited<Promise<string>>; // string
type A2 = Awaited<Promise<Promise<<string>>>; // string

interface IMenu {
	name: string;
	url: string;
}

async function getMenu(): Promise<IMenu[]> {
	return [{ name: 'Analytics', url: 'analytics' }];
}

type R = Awaited<ReturnType<typeof getMenu>>; // IMenu[]

async function getArray<T>(x: T): Promise<Awaited<T>>[]> {
	return [await x];
}
```
------------------------------------------------------------------------------------------
- Декораторы:
1) Декораторы класса
2) Декораторы метода
3) Декораторы свойств

- Инициализация идет в порядке сверху вниз. Исполняется - в обратном порядке (снизу вверх). Порядок влияет. Имеет смысл для логирования ошибок и др.

```
@nullUser
@threeUserAdvanced
class UserService {
	users: number = 1000;
	
	getUsersInDatabase(): number {
		return this.users;
	}
}

function nullUser(target: Function) {
	target.prototype.users = 0;
}

function threeUserAdvanced<T extends { new(..args: any[]): {} }>(constructor: T) {
	return class extends constructor {
		users = 3;
	};
}
```
-----------------------------------------
**Фабрика декораторов:**

```
@setUsers(2)
@setUsersAdvanced(4)
class UserService {
	users: number = 1000;
	
	getUsersInDatabase(): number {
		return this.users;
	}
}

function setUsers(users: number) {
	return (target: Function) => {
		target.prototype.users = users;
	};
}

function setUsersAdvanced<T extends { new(..args: any[]): {} }>(constructor: T) {
	return <T extends { new(..args: any[]): {} }>(constructor: T) {
		return class extends constructor {
			users = 3;
		};
	}
}
```
-----------------------------------------
**Декоратор метода:**

```
class UserService {
	users: number = 1000;
	
	@Catch({ rethrow: true })
	getUsersInDatabase(): number {
		throw new Error('Error Message');
	}
}

function Catch({ rethrow }: { rethrow: boolean } = { rethrow: true }) {
	return (
		target: Object,
		_: string | symbol,
		descriptor: TypedPropertyDescriptor<(...args: any[]) => any>
	): TypedPropertyDescriptor<(...args: any[]) => any | void => {
		const method = descriptor.value;
		descriptor.value = (..args: any[]) => {
			try {
				return method?.apply(target, args);
			} catch(e) {
				if (e instanceof Error) {
					console.log(e.message);
					if (rethrow) {
						throw e;
					}
				}
			}
		}
	}
}
```
-----------------------------------------
**Декоратор свойств:**

```
class UserService {
	@Max(100)
	users: number = 10;
}

function Max(max: number) {
	return (
		target: Object,
		propertyKey: string | symbol
	) => {
		let value: number;
		const setter = function(newValue: number) {
			if (newValue > max) {
				console.log(`Can not set value greater than ${max}`);
			} else {
				value = newValue;
			}
		}
		
		const getter = function() {
			return value;
		}
		
		Object.defineProperty(target, propertyKey, {
			set: setter,
			get: getter
		});
	}
}
```
-----------------------------------------
**Декоратор accessor:**

```
class UserService {
	private _users: number;
	
	@Log()
	set users(num: number) {
		this._users = num;
	}
	
	get users() {
		return this._users;
	}
}

function Log() {
	return (
		target: Object,
		_: string | symbol,
		descriptor: PropertyDescriptor
	) => {
		const set = descriptor.set;
		descriptor.set = (...args: any) => {
			console.log(args);
			set?.apply(target, args);
		}
	}
}
```
-----------------------------------------
**Декоратор параметра:**

```
class UserService {
	private _users: number;
	
	
	setUsersInDatabase(@Positive() num: number, @Positive() num2: number): void {
		return this._users;
	}
}

function Positive() {
	return (
		target: Object,
		propertyKey: string | symbol,
		parameterIndex: number
	) => {
		console.log(Reflect.getOwnMetadata('design:type', target, propertyKey);
		console.log(Reflect.getOwnMetadata('design:paramtypes', target, propertyKey);
		console.log(Reflect.getOwnMetadata('design:returntype', target, propertyKey);
	}
}
```
-----------------------------------------
**Namespaces:**

```
namespace A {
	export cons a = 5;
	
	export interface B {
		c: number;
	}
}
```

```
import { A } from './module/app2'

console.log(A.a);
```

```
import run, { a, type MyType2 } from './module/app2'
import running from './module/app2'
import * as all from './module/app2'
import { Test as CL } from './module/app2'
import { type MyType } from './module/app2'

console.log(all.a);
```
-----------------------------------------
**D.ts:**

```
declare module 'really-relaxed-json' {
	export function toJson(rjsonString: string, compact?: boolean): string;
}
```
----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
**Factory:**

```
interface IInsurance {
	id: number;
	status: string;
	submit(): Promise<boolean>;
}

class TFInsurance implements IInsurance {
	id: number;
	status: string;
	
	async submit(): Promise<boolean> {
		const response = await fetch('TF-url', {
			method: 'POST',
			body: JSON.stringify({ id: this.id })
		});
		
		const data = await res.json();
		return data.isSuccess;
	}
}

class ABInsurance implements IInsurance {
	id: number;
	status: string;
	
	async submit(): Promise<boolean> {
		const response = await fetch('AB-url', {
			method: 'POST',
			body: JSON.stringify({ id: this.id })
		});
		
		const data = await res.json();
		return data.isSuccess;
	}
}

abstract class InsuranceFactory {
	abstract createInstance(): IInsurance;
}

class TFInsuranceFactory extends InsuranceFactory {
	createInstance(): TFInsurance {
		return new TFInsurance();
	}
}

class ABInsuranceFactory extends InsuranceFactory {
	createInstance(): TFInsurance {
		return new ABInsurance();
	}
}
```
-----------------------------------------
**Singleton:**

```
class Singleton {
	private static instance: Singleton;
	
	private constructor() {}
	
	public static get(): Singleton {
		if (!Singleton.instance) {
			Singleton.instance = new Singleton();
		}
		
		return Singleton.instance;
	}
}
```
-----------------------------------------
**Prototype:**

```
interface Prototype<T> {
	clone(): T;
}

class UserHistory implements Prototype<UserHistory> {
	createdAt: Date;

	constructor(public email: string, public name: string) {
		this.createdAt = new Date();
	}
	
	clone(): UserHistory {
		let target = new UserHistory(this.email, this.name);
		target.createdAt = this.createdAt;
		return target;
	}
}
```
-----------------------------------------
**Builder:**

```
enum ImageFormat {
	Png = 'png',
	Jpeg = 'jpeg'
}

interface IResolution {
	width: number;
	height: number;
}

interface IImageConversation extends IResolution {
	format: ImageFormat;
}

class ImageBuilder {
	private formats: ImageFormat[] = [];
	private resolutions: IResolution[] = [];
	
	addPng() {
		if (this.formats.push(ImageFormat.Png))
			return this;
			
		this.formats.push(ImageFormat.Png);
		return this;
	}
	
	addJpeg() {
		if (this.formats.push(ImageFormat.Jpeg))
			return this;
			
		this.formats.push(ImageFormat.Jpeg);
		return this;
	}
	
	addResolution(width: number, height: number) {
		this.resolutions.push({ width, height });
	}
	
	build(): IImageConversation[] {
		const res: IImageConversation[] = [];
		for (const r of this.resolutions)
			for (const f of this.formats)
				res.push({
					format: f,
					width: r.width,
					height: r.height
				});
				
		return res;
	}
}

var result = new ImageBuilder()
	.addJpeg()
	.addPng()
	.addResolution(100, 50)
	.addResolution(200, 30)
	.build();
```
-----------------------------------------
**Bridge:**

```
interface IProvider {
	sendMessage(message: string): void;
	connect(config: string): void;
	disconnect(): void;
}

class TelegramProvider implements IProvider {
	sendMessage(message: string): void {
		// Telegram specific
	}
	
	connect(message: string): void {
		// Telegram specific
	}
	
	disconnect(): void {
		// Telegram specific
	}
}

class WhatsUpProvider implements IProvider {
	sendMessage(message: string): void {
		// WhatsUp specific
	}
	
	connect(message: string): void {
		// WhatsUp specific
	}
	
	disconnect(): void {
		// WhatsUp specific
	}
}

class NotificationSender {
	constructor(private provider: IProvider) {}
	
	send(): void {
		this.provider.connect('connect');
		this.provider.sendMessage('connect');
		this.provider.disconnect();
	}
}

class DelayedNotificationSender extends NotificationSender {
	constructor(private provider: IProvider) {
		super(provider);
	}
	
	send(): void {
		// Delayed sending
	}
}

const sender = new NotificationSender(new TelegramProvider());
sender.send();

const sender2 = new NotificationSender(new WhatsUpProvider());
sender2.send();
```
-----------------------------------------
**Facade:**

```
class NotificationService {
	send(template: string, to: string): void {
		console.log(`Send ${template}: ${to}`);
	}
}

class LogService {
	log(message: string): void {
		console.log(message);
	}
}

console TemplateService {
	private templates = [
		{ name: 'other', template: '<div>Info:</div>'
	];
	
	getByName(name: string): void {
		return this.templates.find(t => t.name === name);
	}
}

class NotificationFacade {
	private notificationService: NotificationService;
	private logger: LogService;
	private templateService: TemplateService;
	
	constructor() {
		this.notificationService = new NotificationService();
		this.logger = new LogService();
		this.templateService = new TemplateService();
	}
	
	send(to: string, templateName: string) {
		const data = this.templateService.getByName(templateName);
		if (!data) {
			this.logger.log('Not found');
			return;
		}
		
		this.notificationService.send(data.template, to);
		this.logger.log('Sent');
	}
}
```
-----------------------------------------
**Adapter:**

```
class KeyValueDatabase {
	private db: Map<string, string> = new Map();
	save(key: string, value: string): void {
		this.db.set(key, value);
	}
}

class PersistentDatabase {
	savePersistent(data: Object): void {
		console.log(data);
	}
}

class PersistentDatabaseAdapter extends KeyValueDatabase {
	constructor(public database: PersistentDatabase) {
		super();
	}
	
	override save(key: string, value: string): void {
		this.database.savePersistent({ key, value });
	}	
}

function run(base: KeyValueDatabase) {
	base.save('key', 'value);
}

run(new PersistentDatabaseAdapter(new PersistentDatabase()));
```
---------------------------------------------------------
**Proxy:**

```
inteface IPaymentApi {
	getPaymentDetail(id: number): IPaymentDetail | undefined;
}

interface IPaymentDetail {
	id: number;
	sum: number;
}

class PaymentApi implements IPaymentApi {
	private data = [{ id: 1, sum: 1000 }];
	
	getPaymentDetail(id: number): IPaymentDetail | undefined {
		return this.data.find(d => d.id === id);
	}
}

class PaymentAccessProxy implements IPaymentApi {
	constructor(private api: IPaymentApi, private userId: number) {}
	
	getPaymentDetail(id: number): IPaymentDetail | undefined {
		if (this.userId === 1) {
			return this.api.getPaymentDetail(id);
		}
		
		console.log('Attempt to get access');
		return undefined;
	}
}

const proxy = new PaymentAccessProxy(new PaymentApi(), 1);
console.log(proxy.getPaymentDetail(1));

const proxy2 = new PaymentAccessProxy(new PaymentApi(), 2);
console.log(proxy2.getPaymentDetail(2));
```
---------------------------------------------------------
**Composite:**

```
abstract class DeliveryItem {
	items: DeliveryItem[];
	
	addItem(item: DeliveryItem) {
		this.items.push(item);
	}
	
	getItemPrices(): number {
		return this.items.reduce((acc: number, i: DeliveryItem) => acc + i.getPrice(), 0);
	}
	
	abstract getPrice(): number;
}

export class DeliveryShop extends DeliveryItem {
	constructor(private deliveryFee: number) {
		super();
	}
	
	getPrice(): number {
		return this.getItemPrices() + this.deliveryFee;
	}
}

export class Package extends DeliveryItem {	
	getPrice(): number {
		return this.getItemPrices() + this.deliveryFee;
	}
}

export class Product extends DeliveryItem {
	constructor(private price: number) {
		super();
	}
	
	getPrice(): number {
		return this.price;
	}
}
```

---------------------------------------------------------
**Chain of Command:**

```
interface IMiddleware {
	next(middleware: IMiddleware): IMiddleware;
	handle(request: any): any;
}

abstract class AbstractMiddleware implements IMiddleware {
	private nextMiddleware: IMiddleware;
	
	next(middleware: IMiddleware) : IMiddleware {
		this.nextMiddleware = middleware;
		return middleware;
	}
	
	handle(request: any) {
		if (this.middleware) {
			return this.middleware.handle(request);
		}
		
		return;
	}
}

class AuthMiddleware implements AbstractMiddleware {	
	override handle(request: any) {
		if (request.userId === 1) {
			return this.middleware.handle(request);
		}
		
		return { error: 'Not authorized' };
	}
}

class ValidateMiddleware implements AbstractMiddleware {	
	override handle(request: any) {
		if (request.body) {
			return this.middleware.handle(request);
		}
		
		return { error: 'No body' };
	}
}

class ControllerMiddleware implements AbstractMiddleware {	
	override handle(request: any) {
		return { sucess: true };
	}
}

const controllerMiddleware = new ControllerMiddleware();
const validateMiddleware = new ValidateMiddleware();
const authMiddleware = new AuthMiddleware();

authMiddleware.next(validateMiddleware).next(controllerMiddleware);
```
---------------------------------------------------------
**Mediator:**

```
interface Mediator {
	notify(sender: string, event: string): void;
}

class NotificationService {
	send() {
		console.log('Send notification');
	}
}

class Logger {
	log() {
		console.log('Logging');
	}
}

abstract class Mediated {
	mediator: Mediator;
	setMediator(mediator: Mediator) {
		this.mediator = mediator;
	}
}

class EventHandler {
	myEvent() {
		this.mediator.notify('EventHandler', 'myEvent');
	}
}

class NotificatationMediator extends Mediator {
	constructor(
		public notificationService: NotificationService,
		public logger: Logger,
		public eventHandler: EventHandler
	) {}
	
	notify(_: string, event: string): void {
		switch (event):
			case 'myEvent':
				this.notificationService.send();
				this.logger.log('Sent');
				break;
	}
}

const eventHandler = new EventHandler();
const logger = new Logger();
const notificationService = new NotificationService();

const notificatationMediator = new NotificatationMediator(notificationService, logger, eventHandler);
eventHandler.setMediator(notificatationMediator);
eventHandler.myEvent(); 
```
---------------------------------------------------------
**Command:**

```
class User {
	constructor(public userId: number) {}
}

class CommandHistory {
	public commands: Command[] = [];
	
	push(command: Command) {
		this.commands.push(command);
	}
	
	remove(command: Command) {
		this.commands = this.commands.filter(c => c.commandId !== command.commandId);
	}
}

abstract class Command {
	public commandId: number;
	
	abstract execute(): void;
	
	constructor(public history: CommandHistory) {
		this.commandId = Math.random();
	}
}

class AddUserCommand extends Command {	
	constructor(
		private user: User,
		private receiver: UserService,
		history: CommandHistory
	) {
		super(history);
	}
	
	execute: void {
		this.receiver.saveUser(this.user);
		this.history.push(this);
	}
	
	undo: void {
		this.receiver.deleteUser(this.user);
		this.history.remove(this);
	}
}

class UserService {
	saveUser(user: User) {
		console.log(`Saving user with id ${user.userId}`);
	}
	
	deleteUser(user: User) {
		console.log(`Deleting user with id ${user.userId}`);
	}
}

class Controller {
	receiver: UserService;
	history: CommandHistory = new CommandHistory();
	
	addReceiver(receiver: UserService) {
		this.receiver = receiver;
	}

	run() {
		const addUserCommand = new AddUserCommand(
			new User(1),
			this.receiver,
			this.history
		);
		
		addUserCommand.execute();
		console.log(addUserCommand.history);
		addUserCommand.undo();
		console.log(addUserCommand.history);
	}
}

const controller = new Controller();
controller.addReceiver(new UserService());
controller.run();
```
---------------------------------------------------------
**State:**

```
class DocumentItem {
	public text: string;
	public state: DocumentItemState;
	
	constructor() {
		this.setState(new DraftDocumentItemState());
	}
	
	getState() {
		return this.state;
	}
	
	setState(state: DocumentItemState) {
		this.state = state;
		this.state.setContext(this);
	}
	
	publishDoc() {}
	
	deleteDoc() {}
}

abstract class DocumentItemState {
	public name: string;
	public item: DocumentItem;
	
	public setContext(item: DocumentItem) {
		this.item = item;
	}
	
	public abstract publish(): void;
	public abstract delete(): void;
}

class DraftDocumentItemState extends DocumentItemState {
	constructor() {
		super();
		this.name = 'DraftDocument';
	}
	
	public publish(): void {
		console.log('Text was sent');
		this.item.setState(new PublishDocumentItemState());
	}
	
	public delete(): void {
		console.log('Document was removed');
	}
}

class PublishDocumentItemState extends DocumentItemState {
	constructor() {
		super();
		this.name = 'PublishDocument';
	}
	
	public publish(): void {
		console.log('Published document could not be published');
	}

	public delete(): void {
		console.log('Status was changed to Draft');
		this.item.setState(new DraftDocumentItemState());
	}
}

const documentItem = new DocumentItem();
item.text = 'My post';
console.log(item.getState());
item.publish();
console.log(item.getState());
item.delete();
```
---------------------------------------------------------
**Strategy:**

```
class User {
	githubToken: string;
	jwnToken: string;
}

interface AuthStrategy {
	auth(user: User): boolean;
}

class Auth {
	constructor(private strategy: AuthStrategy) {}
	
	setStrategy(strategy: AuthStrategy) {
		this.strategy = strategy;
	}
	
	public authUser(user: User): boolean {
		return this.strategy.auth(user);
	}
}

class JWTStrategy implements AuthStrategy {
	auth(user: User): boolean {
		if (user.jwnToken) {
			return true;
		}
		
		return false;
	}
}

class GithubStrategy implements AuthStrategy {
	auth(user: User): boolean {
		if (user.githubToken) {
			return true;
		}
		
		return false;
	}
}

const user = new User();
user.jwnToken = 'jwnToken';
const auth = new Auth(new JWTStrategy());
console.log(auth.authUser(user));
auth.setStrategy(new GithubStrategy());
console.log(auth.authUser(user));
```
---------------------------------------------------------
**Iterator:**

```
class Task {
	constructor(public priority: number) {}
}

class TaskList {
	private task: Task[];
	
	public sortByPriority {
		this.tasks = this.tasks.sort((a, b) => {
			if (a.priority > b.priority) {
				return 1;
			} else if (a.priority == b.priority) {
				return 0;
			} else {
				return -1;
			}
		});
	}
	
	public addTask(task: Task) {
		this.tasks.push(task);
	}
	
	public getTasks() {
		return this.tasks;
	}
	
	public count() {
		return this.tasks.length;
	}
	
	public getIterator() {
		return new PriorityTaskIterator(this);
	}
}

interface IIterator<T> {
	current(): T | undefined;
	next(): T | undefined;
	previous(): T | undefined;
	index(): number;
}

class PriorityTaskIterator implements IIterator<Task> {
	private position: number = 0;
	private taskList: TaskList;
	
	constructor(taskList: TaskList) {
		taskList.sortByPriority();
		this.taskList = taskList;
	}
	
	current(): Task | undefined {
		return this.taskList.getTasks()[this.position];
	}
	
	next(): Task | undefined {
		this.position += 1;
		return this.taskList.getTasks()[this.position];
	}
	
	previous(): Task | undefined {
		this.position -= 1;
		return this.taskList.getTasks()[this.position];
	}
	
	index: number {
		return this.position;
	}
}

const taskList = new TaskList();
taskList.addTask(new Task(8));
taskList.addTask(new Task(1));
taskList.addTask(new Task(3));
const iterator = taskList.getIterator();
console.log(iterator.current());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.previous());
console.log(iterator.index());
```
---------------------------------------------------------
**Template method:**

```
class Form {
	constructor(public name: string) {}
}

abstract class SaveForm<T> {
	public save(form: Form) {
		const result = this.fill(form);
		this.log(result);
		this.send(result);
	}
	
	protected abstract fill(form: Form): T;
	
	protected log(data: T): void {
		console.log(data);
	}
	
	protected abstract send(form: Form): void;
}

class FirstApi extends SaveForm<string> {
	protected fill(name: string): string {
		return form.name;
	}
	
	protected send(data: string): void {
		console.log(`Sending ${data}`);
	}
}

class SecondApi extends SaveForm<{ fullName: string}> {
	protected fill(name: string): { fullName: string} {
		return form.name;
	}
	
	protected send(data: { fullName: string}): void {
		console.log(`Sending ${data}`);
	}
}

const firstApi = new FirstApi();
firstApi.save(new Form('Ivan'));

const secondApi = new SecondApi();
secondApi.save(new Form('Ivan'));
```
---------------------------------------------------------
**Observer:**

```
inteface Observer {
	update(subject: Subject): void;
}

interface Subject {
	attach(observer: Observer): void;
	detach(observer: Observer): void;
	notify: void;
}

class Lead {
	constructor(public name: string, public phone: string) {}
}
class NewLead implements Subject {
	private observers: Observer[] = [];
	
	attach(observer: Observer): void {
		if (this.observers.includes(observer)) {
			return;
		}
		
		this.observers.push(observer);
	}
	
	detach(observer: Observer): void {
		const observerIndex = this.observers.indexOf(observer);
		if (observerIndex === -1) {
			return;
		}
		
		this.observers.splice(observerIndex, 1);
	}
	
	notify(): void {
		for (const observer of this.observers) {
			observer.update(this);
		}
	}
}

class NotificationService implements Observer {
	update(subject: Subject): void {
		console.log('NotificationService got notification');
		console.log(subject);
	}
}

class LeadService implements Observer {
	update(subject: Subject): void {
		console.log('LeadService got notification');
		console.log(subject);
	}
}

const subject = new NewLead();
subject.state = new Lead('Ivan', '1000');
const notificationService = new NotificationService();
const leadService = new LeadService();

subject.attach(notificationService);
subject.attach(leadService);
subject.notify();
subject.detach(notificationService);
subject.detach(leadService);
subject.notify();
```
