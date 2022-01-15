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
- - ```ng generate component post2 --skipTests``` (```post2``` - имя компонента)
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
- ```lorem20``` (+ tab) = <PLACEHOLDER> 
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
