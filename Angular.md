- AngularJS vs Angular-2: https://angularjs.org vs https://angular.io
-------------------------------
- Angular Roadmap: https://vladilen.ru/Angular
- https://angdev.ru/guide/intro/start/
- https://angdev.ru/doc/setup-and-configuration/
- https://angdev.ru/cheatsheet/
-------------------------------
- ```npm install -g @angular/cli```
- ```ng new angular-basics``` (`<angular-basics` - application name-folder)
- ```cd angular-basics``` (`<angular-basics>` - application name-folder)
- ```npm start```
-------------------------------
- ```ng generate component post2``` (```post2``` - имя компонента)
- ```ng generate component post2 --skipTests``` (```post2``` - имя компонента)
- ```ng g c post2``` (```post2``` - имя компонента)
-------------------------------
- ```.editorconfig```
- ```.browserslistrc```
- ```karma.conf```
- ```package.json```
```
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "watch": "ng build --watch --configuration development",
    "test": "ng test"
}
```

- ```angular.json```

```
"configurations": {
    "production": {
      "fileReplacements": [
        {
          "replace": "src/environments/environment.ts",
          "with": "src/environments/environment.prod.ts"
        }
      ]
    }
}
```

- ```tsconfig.app.json```
```"extends": "./tsconfig.json",```
- ```tsconfig.spec.json```
-------------------------------
**src/main.ts:**
```
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

**src/app/app.module.ts:**
```
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

**src/app/app.component.ts:**
```
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  title = 'angular-basics';
}
```
-------------------------------
```
@Component({
  selector: 'app-post',
  templateUrl: './post.component.html'
})
export class PostComponent{

}
```

```
@Component({
  selector: 'app-post4',
  template: `
    <div class="post4">
      <h2>Post title</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsam, suscipit!</p>
    </div>
  `,
  styles: [`
    .post4 {
      padding: .5rem;
      border: 2px solid black;
    }

    h2 {
      font-size: 1rem;
    }
  `]
})
export class Post4Component {

}
```
-------------------------------
```
export class AppComponent {
  title = 'Dynamic title'
  number = 42
  arr = [1, 2, 3]
  obj = { a: 1, b: {c: 2} }
}
```

```
<p>{{ title }}</p>

<p><strong>{{number - 2}}</strong></p>
<p><strong>{{arr}}</strong></p>
<p><strong>{{obj.b.c}}</strong></p>

<p><strong>{{ 40 + 2 }}</strong></p>
<p><strong>{{ 'Hello' + ' World' }}</strong></p>

<img [src]="img" alt="">
```

```
export class AppComponent {
  img = 'https://google.com/image.png'
}
```

```
<img [src]="img" alt="">
```
-------------------------------
```
<button (click)="onClick()">Click me!</button>


<input
  type="text"
  (keyup.enter)="onInput($event)"
  (blur)="onBlur(myInput.value)"
  #myInput
>
<p><strong>{{inputValue}}</strong></p>
```

```
export class AppComponent {
  onInput(event: KeyboardEvent) {
    this.inputValue = (<HTMLInputElement>event.target).value
  }

  onBlur(str: string) {
    this.inputValue = str
  }

  onClick() {
    console.log('Click!')
  }
}
```
-------------------------------
```
<input type="text" [(ngModel)]="title">

<p>{{title}}</p>
```

```
export class AppComponent {
  title = 'Initial'
  onInput(event: any) {
    this.title = event.target.value
  }
}
```
-------------------------------
```
<button (click)="backgroundToggle = !backgroundToggle">Toggle</button>

<div [ngStyle]="{
  width: '200px',
  height: '200px',
  borderRadius: '5px',
  border: '1px solid #ccc',
  background: backgroundToggle ? 'red' : 'blue'
}">
```

```
export class AppComponent {
  backgroundToggle = false
}
```
-------------------------------
```
<p
  [class.blue]="!backgroundToggle"
  [class.red]="backgroundToggle"
>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequuntur, ratione.</p>
```

```
.red {
  background: red;
  font-weight: bold;
  color: #fff;
}

.blue {
  background: blue;
  font-size: 1.5rem;
  color: #fff;
}
```

```
export class AppComponent {
  backgroundToggle = false
}
```
-------------------------------
```
<button (click)="toggle = !toggle">Toggle</button>

<p *ngIf="toggle; else blueP" class="red">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Id, ratione.</p>

<ng-template #blueP>
  <p class="blue">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Architecto, in?</p>
</ng-template>
```

```
export class AppComponent {
  toggle = false
}
```
-------------------------------
```
<button (click)="toggle = !toggle">Toggle</button>
<button (click)="toggle = 111">Set 111</button>

<div [ngSwitch]="toggle">
  <p *ngSwitchCase="true" class="red">Lorem ipsum.</p>
  <p *ngSwitchCase="false" class="blue">Lorem ipsum. Lorem ipsum.</p>
  <p *ngSwitchDefault>Lorem ipsum.</p>
</div>
```

```
export class AppComponent {
  toggle: any = false
}
```
-------------------------------
**Data Binding Types:**
1. String Interpolation: ```Syntax: {{propertyname}}``` (```{{product.title}}```)
2. Property Binding: ```Syntax: property[value]``` (```[value]='myBlog'```)
3. Event Binding: ```Syntax: (eventname)" (```<img [src]="imgUrl" />```)
4. Two Way Data Binding: ```Syntax: [(ngModel)] = "[property of your component]"```
-------------------------------
**4 типа директив:**
1. Components directives
2. Structural directives
3. Attribute directives
4. Custom Directive
-------------------------------
- ```lorem20``` (+ tab) = <PLACEHOLDER>
- ```npm``` tab в WebStorm
-------------------------------
- RxJS
- angular.json
- browserlist.json
- dependency vs devDependency
- Интерполяция
- Рендеринг поля типа Array (array.join)
- Pipe (AsyncPipe, CurrencyPipe, DatePipe, UpperCasePipe and etc...)
- ```{{ obj | json }}``` - pipe
- ```<pre>{{ obj | json }}</pre>```
- double binding
- ```[src] = "imgUrl"```
- ```(click)```
- Директивы: структурные директивы, ...
- Интерфейсы для моделей
- Декораторы
- Односторонний биндинг, Event Binding    
-------------------------------
- **Angular-interview-questions-RU:** https://github.com/FedorovAlexander/Angular-interview-questions-RU
