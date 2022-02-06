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

- ```ng g d style2 --skipTests``` (```style2``` - имя директивы)
- - ```ng generate directive style2 --skipTests```

- ```ng g s localservice --skipTests``` (```localservice``` - имя директивы)
- - ```ng generate service localservice --skipTests```
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
```
<ul style="list-style: none">
  <li *ngFor="let post of objs">
    <p>{{post.title}} <b>{{post.author}}</b></p>
    <ul>
      <li *ngFor="let comment of post.comments">
        <div>
          <small>{{comment.name}}</small>
          <p>{{comment.text}}</p>
        </div>
      </li>
    </ul>
  </li>
</ul>
```

```
export class AppComponent {
  arr = [1, 1, 2, 3, 5, 8, 13]
  objs = [
    {title: 'Post 1', author: 'Vladilen', comments: [
        {name: 'Max', text: 'lorem 1'},
        {name: 'Max', text: 'lorem 2'},
        {name: 'Max', text: 'lorem 3'},
      ]},
    {title: 'Post 2', author: 'Vladilen 2', comments: [
        {name: 'Max 2', text: 'lorem 1'},
        {name: 'Max 2', text: 'lorem 2'},
        {name: 'Max 2', text: 'lorem 3'},
      ]}
  ]
}
```
-------------------------------
```
<p>
  {{ now | date:'long' | uppercase | lowercase }}
</p>
```

```
export class AppComponent {
  now: Date = new Date()
}
```
-------------------------------
```
<app-post
    *ngFor="let p of posts"
    [post]="p"
  ></app-post>
```

```
<div class="card">
  <h2>{{post.title}}</h2>
  <p>{{post.text}}</p>
</div>
```

```
export class PostComponent implements OnInit {
  @Input() post: Post
  constructor() { }
  ngOnInit() {
  }
}
```
-------------------------------
```
<app-post
    *ngFor="let p of posts"
    [post]="p">
</app-post>
```

```
export class PostFormComponent implements OnInit {
  @Output() onAdd: EventEmitter<Post> = new EventEmitter<Post>()
  title = ''
  text = ''

  constructor() { }
  ngOnInit() { }

  addPost() {
    if (this.text.trim() && this.title.trim()) {
      const post: Post = {
        title: this.title,
        text: this.text
      }
      this.onAdd.emit(post)
      this.title = this.text = ''
    }
  }
}
```

```
<div>
  <input
    type="text"
    class="form-control"
    placeholder="Title..."
    [(ngModel)]="title"
  >
  <input
    type="text"
    class="form-control"
    placeholder="Text..."
    [(ngModel)]="text"
  >

  <button class="btn" (click)="addPost()">Добавить пост</button>
</div>
```

```
export class PostComponent implements OnInit {
  @Input() post: Post
  constructor() { }
  ngOnInit() {  }

}
```

```
export class AppComponent {
  posts: Post[] = [
    {title: 'Хочу выучить Angular компоненты', text: 'Я все еще учу компоненты', id: 1},
    {title: 'Следующий блок', text: 'Будет про директивы и еще про пайпы', id: 2}
  ]

  updatePosts(post: Post) {
    this.posts.unshift(post)
  }
}
```

```
<app-post-form
    (onAdd)="updatePosts($event)">
</app-post-form>

<hr />

<app-post
    *ngFor="let p of posts"
    [post]="p">
</app-post>
```
-------------------------------
```
export class PostFormComponent {
  @ViewChild('titleInput', {static: false}) inputRef: ElementRef

  focusTitle() {
    this.inputRef.nativeElement.focus()
  }
}
```

```
<input
    type="text"
    class="form-control"
    placeholder="Title..."
    [(ngModel)]="title"
    #titleInput>

<input
    type="text"
    class="form-control"
    placeholder="Text..."
    [(ngModel)]="text">

<button class="btn" (click)="addPost()">Добавить пост</button>
<button class="btn" (click)="focusTitle()">Focus title</button>
```
-------------------------------
```
<app-post
    *ngFor="let p of posts"
    [post]="p">
    
<small *ngIf="p.text.length > 10; else short">Пост длинный</small>
<ng-template #short>
  <small>Пост короткий</small>
</ng-template>
</app-post>
```
-------------------------------
```
<app-post
    *ngFor="let p of posts"
    [post]="p">
    <div #info>
      <small *ngIf="p.text.length > 10; else short">Пост длинный</small>
      <ng-template #short>
        <small>Пост короткий</small>
      </ng-template>
    </div>
</app-post>
```

```
export class PostComponent implements OnInit {
  @Input() post: Post
  @ContentChild('info', {static: true}) infoRef: ElementRef

  constructor() { }

  ngOnInit() {
    console.log(this.infoRef.nativeElement)
  }
}
```
-------------------------------
```
export class PostComponent implements
  OnInit,
  OnChanges,
  DoCheck,
  AfterContentInit,
  AfterContentChecked,
  AfterViewInit,
  AfterViewChecked,
  OnDestroy
{

  @Input() post: Post
  @Output() onRemove = new EventEmitter<number>()
  @ContentChild('info', {static: true}) infoRef: ElementRef

  removePost() {
    this.onRemove.emit(this.post.id)
  }

  ngOnChanges(changes: SimpleChanges): void {
    console.log('ngOnChanges', changes)
  }

  ngOnInit() {
    console.log('ngOnInit')
  }

  ngDoCheck(): void {
    console.log('ngDoCheck')
  }

  ngAfterContentInit(): void {
    console.log('ngAfterContentInit')
  }

  ngAfterContentChecked(): void {
    console.log('ngAfterContentChecked')
  }

  ngAfterViewInit(): void {
    console.log('ngAfterViewInit')
  }

  ngAfterViewChecked(): void {
    console.log('ngAfterViewChecked')
  }

  ngOnDestroy(): void {
    console.log('ngOnDestroy')
  }
}
```
-------------------------------
```
@Component({
  ...,
  ...,
  changeDetection: ChangeDetectionStrategy.OnPush
})
```
-------------------------------
```
@Component({
  ...,
  ...,
  encapsulation: ViewEncapsulation.None
})
```
-------------------------------
```
import {Directive, ElementRef, Renderer2} from '@angular/core'

@Directive({
  selector: '[appStyle]'
})
export class StyleDirective {
  constructor(private el: ElementRef, private r: Renderer2) {
    this.r.setStyle(this.el.nativeElement, 'color', 'blue')
  }
}
```

```
<p appStyle>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi, laborum!</p>
```
-------------------------------
```
import {Directive, ElementRef, HostListener, Renderer2} from '@angular/core'

@Directive({
  selector: '[appStyle]'
})
export class StyleDirective {
  constructor(private el: ElementRef, private r: Renderer2) {

  }

  @HostListener('click', ['$event.target']) onClick(event: Event) {
    console.log(event)
  }

  @HostListener('mouseenter') onEnter() {
    this.r.setStyle(this.el.nativeElement, 'color', 'blue')
  }

  @HostListener('mouseleave') onLeave() {
    this.r.setStyle(this.el.nativeElement, 'color', null)
  }
}

```

```
<p appStyle>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi, laborum!</p>
```
-------------------------------
```
import {Directive, ElementRef, HostListener, Input, Renderer2} from '@angular/core'

@Directive({
  selector: '[appStyle]'
})
export class StyleDirective {
  @Input('appStyle') color: string = 'blue'
  @Input() dStyles: {border?: string, fontWeight?: string, borderRadius?: string}

  constructor(private el: ElementRef, private r: Renderer2) {

  }

  @HostListener('click', ['$event.target']) onClick(event: Element) {
    console.log(event)
  }

  @HostListener('mouseenter') onEnter() {
    this.r.setStyle(this.el.nativeElement, 'color', this.color)
    this.r.setStyle(this.el.nativeElement, 'fontWeight', this.dStyles.fontWeight)
    this.r.setStyle(this.el.nativeElement, 'border', this.dStyles.border)
    this.r.setStyle(this.el.nativeElement, 'borderRadius', this.dStyles.borderRadius)
  }

  @HostListener('mouseleave') onLeave() {
    this.r.setStyle(this.el.nativeElement, 'color', null)
    this.r.setStyle(this.el.nativeElement, 'fontWeight', null)
    this.r.setStyle(this.el.nativeElement, 'border', null)
    this.r.setStyle(this.el.nativeElement, 'borderRadius', null)
  }
}
```

```
<div class="container">
  <h1>Angular Directives</h1>


  <p [appStyle]="'red'" [dStyles]="{border: '1px solid blue', borderRadius: '5px'}">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi, laborum!
  </p>

  <p [appStyle]="'blue'" [dStyles]="{border: '1px solid red', borderRadius: '15px'}">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi, laborum!
  </p>
</div>
```
-------------------------------
```
import {Directive, ElementRef, HostBinding, HostListener, Input, Renderer2} from '@angular/core'

@Directive({
  selector: '[appStyle]'
})
export class StyleDirective {
  @Input('appStyle') color: string = 'blue'
  @Input() dStyles: {border?: string, fontWeight?: string, borderRadius?: string}

  @HostBinding('style.color') elColor = null

  constructor(private el: ElementRef, private r: Renderer2) {
  }

  @HostListener('click', ['$event.target']) onClick(event: Element) {
    console.log(event)
  }

  @HostListener('mouseenter') onEnter() {
    this.elColor = this.color
  }

  @HostListener('mouseleave') onLeave() {
    this.elColor = null
  }
}

```

```
<div class="container">
  <h1>Angular Directives</h1>


  <p [appStyle]="'red'" [dStyles]="{border: '1px solid blue', borderRadius: '5px'}">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi, laborum!
  </p>

  <p [appStyle]="'blue'" [dStyles]="{border: '1px solid red', borderRadius: '15px'}">
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Excepturi, laborum!
  </p>
</div>
```
-------------------------------
```
import {Directive, Input, TemplateRef, ViewContainerRef} from '@angular/core'

@Directive({
  selector: '[appIfnot]'
})
export class IfnotDirective {

  @Input('appIfnot') set ifNot(condition: boolean) {
    if (!condition) {
      // Показать элементы
      this.viewContainer.createEmbeddedView(this.templateRef)
    } else {
      // Скрыть
      this.viewContainer.clear()
    }
  }

  constructor(private templateRef: TemplateRef<any>,
              private viewContainer: ViewContainerRef) { }
}
```

```
<div class="container">
  <button class="btn" (click)="isVisible = !isVisible">Toggle</button>

<!--  <div *ngIf="isVisible" class="wrap">-->
<!--    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequuntur cum ea et ex hic incidunt itaque maiores quos sint veritatis!</p>-->
<!--  </div>-->

<!--  <ng-template [ngIf]="isVisible">-->
<!--    <div class="wrap">-->
<!--      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequuntur cum ea et ex hic incidunt itaque maiores quos sint veritatis!</p>-->
<!--    </div>-->
<!--  </ng-template>-->

<!--  <div class="wrap" *appIfnot="!isVisible">-->
<!--    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequuntur cum ea et ex hic incidunt itaque maiores quos sint veritatis!</p>-->
<!--  </div>-->

  <ng-template [appIfnot]="!isVisible">
    <div class="wrap">
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequuntur cum ea et ex hic incidunt itaque maiores quos sint veritatis!</p>
    </div>
  </ng-template>
</div>
```
-------------------------------
```
import {Component} from '@angular/core'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  e: number = Math.E
}
```

```
<p>
    {{ e | number:'1.1-5' }}
</p>
<p>
    {{ e | number:'3.1-2' }}
</p>
<p>
    {{ e | number:'1.0-0' }}
</p>
```
-------------------------------
```
...
export class AppComponent {
  str = 'hello world'
  date: Date = new Date()
  float = 0.42

  obj = {
    a: 1,
    b: {
      c: 2,
      d: {
        e: 3,
        f: 4
      }
    }
  }
}
...
```

```
<p>
	{{ str | uppercase | lowercase | titlecase }}
</p>
<p>
	{{ str | titlecase | slice:1:-2 }}
</p>
<p>
	{{ date | date:'MMMM dd, yyy, HH:mm:ss' }}
</p>
<p>{{ float }}</p>
<p>{{ float | currency }}</p>
<p>{{ float | percent: '2.0-0' }}</p>
<pre>{{ obj | json }}</pre>
```
-------------------------------
```
import {Pipe, PipeTransform} from '@angular/core'

@Pipe({
  name: 'mult'
})
export class MultByPipe implements PipeTransform {
  transform(num: number, pow: number = 2): number {
    return num * pow
  }
}
```

```
<p>{{ 10 | mult }}</p>
<p>{{ 10 | mult:2 }}</p>
<p>{{ 10 | mult:3 }}</p>
<p>{{ 10 | mult:5 }}</p>
<p>{{ 10 | mult:8 }}</p>
<p>{{ 10 | mult:13 }}</p>
```
-------------------------------
```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'exMarks'
})
export class ExMarksPipe implements PipeTransform {
  transform(str: string): string {
    return `${str.trim()}!!!!`;
  }
}
```

```
<p>{{ 'Hello World     ' | exMarks }}</p>
```
-------------------------------
```
Параметр pure:
@Pipe({
  name: 'filter',
  pure: false
})
```

```
import {Pipe, PipeTransform} from '@angular/core'
import {Post} from '../app.component'

@Pipe({
  name: 'filter',
  pure: false
})
export class FilterPipe implements PipeTransform {
  transform(posts: Post[], search: string = '', field: string = 'title'): Post[] {
    if (!search.trim()) {
      return posts
    }

    return posts.filter(post => {
      return post[field].toLowerCase().includes(search.toLowerCase())
    })
  }
}
```

```
<button class="btn" (click)="searchField = 'title'">Title</button>
<button class="btn" (click)="searchField = 'text'">Text</button>

<input type="text" [(ngModel)]="search">

<div
*ngFor="let post of posts | filter:search:searchField"
class="card"
>
<h2>{{post.title}}</h2>
<p>{{post.text}}</p>
</div>
```
-------------------------------
```
import {Component, OnInit} from '@angular/core'
import {Observable} from 'rxjs'

export interface Post {
  title: string
  text: string
}

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {

  p: Promise<string> = new Promise<string>(resolve => {
    setTimeout(() => {
      resolve('Promise Resolved')
    }, 4000)
  })

  date$: Observable<Date> = new Observable(obs => {
    setInterval(() => {
      obs.next(new Date())
    }, 1000)
  })

  date: Date

  ngOnInit(): void {
  }
}
```

```
<p>Wait for it... {{ p | async }}</p>
<p>Date: {{ date$ | async | date:'HH:mm:ss yyyy' }}</p>
```
-------------------------------
```
import {Injectable} from '@angular/core'

@Injectable({providedIn: 'root'})
export class AppCounterService {
  counter = 0

  increase() {
    this.counter++
  }

  decrease() {
    this.counter--
  }
}
```

```
import {BrowserModule} from '@angular/platform-browser'
import {NgModule} from '@angular/core'

import {AppComponent} from './app.component'
import {FormsModule} from '@angular/forms';
import {AppCounterService} from './services/app-counter.service'

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  providers: [
    AppCounterService
  ],
  bootstrap: [AppComponent]
})
export class AppModule {
}
```

```
<h2>App Counter: {{appCounterService.counter}}</h2>
<button class="btn" (click)="appCounterService.increase()">+</button>
<button class="btn" (click)="appCounterService.decrease()">-</button>
```
-------------------------------
```
import { Injectable } from '@angular/core';

@Injectable()
export class LocalCounterService {
  counter = 0

  increase() {
    this.counter++
  }

  decrease() {
    this.counter--
  }
}
```

(Без регистрации в app.module)
```
import {Component} from '@angular/core'
import {AppCounterService} from './services/app-counter.service'
import {LocalCounterService} from './services/local-counter.service'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss'],
  providers: [LocalCounterService]
})
export class AppComponent {
  constructor(
    private appCounterService: AppCounterService,
    private localCounterService: LocalCounterService
  ) {}
}
```
-------------------------------
```
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LogService {
  log(text) {
    console.log(`Log: ${text}`)
  }
}
```

```
import {Injectable} from '@angular/core'
import {LogService} from './log.service'

@Injectable({providedIn: 'root'})
export class AppCounterService {
  counter = 0

  constructor(private logService: LogService) {
  }
  
  increase() {
    this.logService.log('increase counter...')
    this.counter++
  }

  decrease() {
    this.logService.log('decrease counter...')
    this.counter--
  }
}
```
-------------------------------
```
import {Component, OnInit} from '@angular/core'
import {FormGroup} from '@angular/forms'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {
  form: FormGroup

  ngOnInit() {
    this.form = new FormGroup({})
  }

  submit() {
    console.log('Form submitted: ', this.form)
  }
}
```

(Импорт ReactiveFormsModule)
```
import {BrowserModule} from '@angular/platform-browser'
import {NgModule} from '@angular/core'

import {AppComponent} from './app.component'
import {FormsModule, ReactiveFormsModule} from '@angular/forms'

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
    FormsModule,
    ReactiveFormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {
}
```

```
<div class="container">
  <form class="card" [formGroup]="form" (ngSubmit)="submit()">
    <h1>Angular Forms</h1>

    <div class="form-control">
      <label>Email</label>
      <input type="text" placeholder="Email">
      <div class="validation"></div>
    </div>

    <div class="form-control">
      <label>Пароль</label>
      <input type="password" placeholder="Пароль">
      <div class="validation"></div>
    </div>

    <div class="card">
      <h2>Адрес</h2>

      <div class="form-control">
        <label>Страна</label>

        <select>
          <option value="ru">Россия</option>
          <option value="ua">Украина</option>
          <option value="by">Беларусь</option>
        </select>
      </div>

      <div class="form-control">
        <input type="text">
      </div>

      <button class="btn" type="button">Выбрать столицу</button>
    </div>

    <div class="card">
      <h2>Ваши навыки</h2>
      <button class="btn" type="button">Добавить умение</button>
      <div class="form-control">
        <label></label>
        <input type="text">
      </div>
    </div>

    <button class="btn" type="submit">Отправить</button>
  </form>
</div>
```
-------------------------------
```
import {Component, OnInit} from '@angular/core'
import {FormControl, FormGroup, Validators} from '@angular/forms'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {
  form: FormGroup

  ngOnInit() {
    this.form = new FormGroup({
      email: new FormControl('', [
        Validators.email,
        Validators.required
      ]),
      password: new FormControl(null, [
        Validators.required,
        Validators.minLength(6)
      ])
    })
  }

  submit() {
    if (this.form.valid) {
      console.log('Form: ', this.form)
      const formData = {...this.form.value}

      console.log('Form Data:', formData)
    }
  }
}
```

```
<button class="btn" type="submit" [disabled]="form.invalid">Отправить</button>
```
-------------------------------
- Встроенные CSS-классы:
`ng-untouched`, `ng-touched`, `ng-pristine`, `ng-invalid`, `ng-valid`, `ng-dirty`
-------------------------------
```
<div class="form-control">
  <label>Email</label>
  <input type="text" placeholder="Email" formControlName="email">

  <div
	*ngIf="form.get('email').invalid && form.get('email').touched"
	class="validation"
  >
	<small *ngIf="form.get('email').errors.required">
	  Поле email не может быть пустым
	</small>

	<small *ngIf="form.get('email').errors.email">
	  Введите корректный email
	</small>
  </div>
</div>

<div class="form-control">
  <label>Пароль</label>
  <input type="password" placeholder="Пароль" formControlName="password">

  <div
	*ngIf="form.get('password').invalid && form.get('password').touched"
	class="validation"
  >
	<small *ngIf="form.get('password').errors.required">
	  Пароль не может быть пустым
	</small>

	<small *ngIf="form.get('password').errors.minlength">
	  Длинна должна быть не менее {{form.get('password').errors.minlength.requiredLength}}.
	  Сейчас количество символов {{form.get('password').errors.minlength.actualLength}}
	</small>
  </div>
</div>
```
-------------------------------
```
import {Component, OnInit} from '@angular/core'
import {FormControl, FormGroup, Validators} from '@angular/forms'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {
  form: FormGroup

  ngOnInit() {
    this.form = new FormGroup({
      email: new FormControl('', [
        Validators.email,
        Validators.required
      ]),
      password: new FormControl(null, [
        Validators.required,
        Validators.minLength(6)
      ]),
      address: new FormGroup({
        country: new FormControl('by'),
        city: new FormControl('Минск', Validators.required)
      })
    })
  }

  submit() {
    if (this.form.valid) {
      console.log('Form: ', this.form)
      const formData = {...this.form.value}

      console.log('Form Data:', formData)
    }
  }

  setCapital() {
    const cityMap = {
      ru: 'Москва',
      ua: 'Киев',
      by: 'Минск'
    }

    const cityKey = this.form.get('address').get('country').value
    const city = cityMap[cityKey]

    this.form.patchValue({address: {city}})
  }
}
```

```
<button class="btn" type="button" (click)="setCapital()">Выбрать столицу</button>
```
-------------------------------
```
<div class="card" formGroupName="skills">
  <h2>Ваши навыки</h2>
  <button class="btn" type="button" (click)="addSkill()">Добавить умение</button>

  <div
	class="form-control"
	*ngFor="let control of form.get('skills').controls; let idx = index"
  >
	<label>Умение {{idx + 1}}</label>
	<input type="text" [formControlName]="idx">
  </div>
</div>
```

```
addSkill() {
    const control = new FormControl('', Validators.required);
    // (<FormArray>this.form.get('skills'))
    (this.form.get('skills') as FormArray).push(control)
}
```
-------------------------------
```
import {FormControl} from '@angular/forms'

export class MyValidators {
  static restrictedEmails(control: FormControl): {[key: string]: boolean} {
    if (['v@mail.ru', 'test@mail.ru'].includes(control.value)) {
      return {restrictedEmail: true}
    }
	
    return null
  }
}
```

```
export class AppComponent implements OnInit {
  form: FormGroup

  ngOnInit() {
    this.form = new FormGroup({
      email: new FormControl('', [
        Validators.email,
        Validators.required,
        MyValidators.restrictedEmails
      ]),
      password: new FormControl(null, [
        Validators.required,
        Validators.minLength(6)
      ]),
      address: new FormGroup({
        country: new FormControl('by'),
        city: new FormControl('Минск', Validators.required)
      }),
      skills: new FormArray([])
    })
  }
}
```
-------------------------------
```
import {FormControl} from '@angular/forms'
import {Observable} from 'rxjs'

export class MyValidators {
  static restrictedEmails(control: FormControl): {[key: string]: boolean} {
    if (['v@mail.ru', 'test@mail.ru'].includes(control.value)) {
      return {restrictedEmail: true}
    }
    return null
  }

  static uniqEmail(control: FormControl): Promise<any> | Observable<any> {
    return new Promise(resolve => {
      setTimeout(() => {
        if (control.value === 'async@mail.ru') {
          resolve({uniqEmail: true})
        } else {
          resolve(null)
        }
      }, 1000)
    })
  }
}
```

```
import {Component, OnInit} from '@angular/core'
import {FormArray, FormControl, FormGroup, Validators} from '@angular/forms'
import {MyValidators} from './my.validators'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {
  form: FormGroup

  ngOnInit() {
    this.form = new FormGroup({
      email: new FormControl('', [
        Validators.email,
        Validators.required,
        MyValidators.restrictedEmails
      ], [MyValidators.uniqEmail]),
      password: new FormControl(null, [
        Validators.required,
        Validators.minLength(6)
      ]),
      address: new FormGroup({
        country: new FormControl('by'),
        city: new FormControl('Минск', Validators.required)
      }),
      skills: new FormArray([])
    })
  }
}
```
-------------------------------
```
export class AppComponent implements OnInit {
  form: FormGroup

  submit() {
    if (this.form.valid) {
      console.log('Form: ', this.form)
      const formData = {...this.form.value}
      console.log('Form Data:', formData)

      this.form.reset()
    }
  }
}
```
-------------------------------
```
import {Component, forwardRef, Provider} from '@angular/core'
import {ControlValueAccessor, NG_VALUE_ACCESSOR} from '@angular/forms'

const VALUE_ACCESSOR: Provider = {
  provide: NG_VALUE_ACCESSOR,
  useExisting: forwardRef(() => SwitchComponent),
  multi: true
}

@Component({
  selector: 'app-switch',
  templateUrl: './switch.component.html',
  styleUrls: ['./switch.component.scss'],
  providers: [VALUE_ACCESSOR]
})
export class SwitchComponent implements ControlValueAccessor {

  state = 'off'

  private onChange = (value: any) => {}

  setState(state: string) {
    this.state = state

    this.onChange(this.state)
  }

  registerOnChange(fn: any): void {
    this.onChange = fn
  }

  registerOnTouched(fn: any): void {

  }

  setDisabledState(isDisabled: boolean): void {
  }

  writeValue(state: string): void {
    this.state = state
  }
}
```

```
<div>
  <button [class.active]="state === 'on'" (click)="setState('on')">On</button>
  <button [class.active]="state === 'off'" (click)="setState('off')">Off</button>
</div>
```
-------------------------------
```
import {Component, OnInit} from '@angular/core'
import {HttpClient} from '@angular/common/http'

export interface Todo {
  completed: boolean
  title: string
  id?: number
}

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {

  todos: Todo[] = []

  constructor(private http: HttpClient) {}

  ngOnInit() {
    this.http.get<Todo[]>('https://jsonplaceholder.typicode.com/todos?_limit=2')
      .subscribe(todos => {
        console.log('Response', todos)
        this.todos = todos
      })
  }
}
```

```
import {BrowserModule} from '@angular/platform-browser'
import {NgModule} from '@angular/core'

import {AppComponent} from './app.component'
import {FormsModule} from '@angular/forms';
import {HttpClientModule} from '@angular/common/http'

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {
}
```
-------------------------------
```
import {Component, OnInit} from '@angular/core'
import {HttpClient} from '@angular/common/http'

export interface Todo {
  completed: boolean
  title: string
  id?: number
}

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {

  todos: Todo[] = []
  todoTitle = ''
  constructor(private http: HttpClient) {}

  addTodo() {
    if (!this.todoTitle.trim()) {
      return
    }

    const newTodo: Todo = {
      title: this.todoTitle,
      completed: false
    }

    this.http.post<Todo>('https://jsonplaceholder.typicode.com/todos', newTodo)
      .subscribe(todo => {
        this.todos.push(todo)
        this.todoTitle = ''
      })
  }
}
```

```
<div class="card">
    <div class="form-control">
      <input type="text" placeholder="Название" [(ngModel)]="todoTitle">
    </div>
    <button class="btn" (click)="addTodo()">Добавить</button>
    <button class="btn">Загрузить</button>
  </div>
```
-------------------------------
```
import {Component, OnInit} from '@angular/core'
import {HttpClient} from '@angular/common/http'
import {delay} from 'rxjs/operators'

export interface Todo {
  completed: boolean
  title: string
  id?: number
}

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {
  todos: Todo[] = []
  loading = false
  todoTitle = ''
  constructor(private http: HttpClient) {}

  ngOnInit() {
    this.fetchTodos()
  }

  fetchTodos() {
    this.loading = true
    this.http.get<Todo[]>('https://jsonplaceholder.typicode.com/todos?_limit=2')
      .pipe(delay(1500))
      .subscribe(todos => {
        this.todos = todos
        this.loading = false
      })
  }
}
```

```
<div *ngIf="!loading; else loadingBlock">
    <div class="card" *ngFor="let todo of todos">
      <p>
        <span [class.completed]="todo.completed">{{todo.title | titlecase}}</span>
        <span>
          <button class="btn btn-danger">Удалить</button>
          <button class="btn" [disabled]="todo.completed">Завершить</button>
        </span>
      </p>
    </div>
</div>

<ng-template #loadingBlock>
	<p>Loading...</p>
</ng-template>
```
-------------------------------
```
removeTodo(id: number) {
    this.http.delete<void>(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .subscribe(() => {
        this.todos = this.todos.filter(t => t.id !== id)
      })
}
```
-------------------------------
```
import {Injectable} from '@angular/core'
import {HttpClient} from '@angular/common/http'
import {Observable} from 'rxjs'
import {delay} from 'rxjs/operators'

export interface Todo {
  completed: boolean
  title: string
  id?: number
}

@Injectable({providedIn: 'root'})
export class TodosService {
  constructor(private http: HttpClient) {}

  addTodo(todo: Todo): Observable<Todo> {
    return this.http.post<Todo>('https://jsonplaceholder.typicode.com/todos', todo)
  }

  fetchTodos(): Observable<Todo[]> {
    return this.http.get<Todo[]>('https://jsonplaceholder.typicode.com/todos?_limit=2')
      .pipe(delay(500))
  }

  removeTodo(id: number): Observable<void> {
    return this.http.delete<void>(`https://jsonplaceholder.typicode.com/todos/${id}`)
  }
}
```

```
import {Component, OnInit} from '@angular/core'
import {HttpClient} from '@angular/common/http'
import {delay} from 'rxjs/operators'
import {Todo, TodosService} from './todos.service'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent implements OnInit {
  todos: Todo[] = []
  loading = false
  todoTitle = ''
  constructor(private todosService: TodosService) {}

  ngOnInit() {
    this.fetchTodos()
  }

  addTodo() {
    if (!this.todoTitle.trim()) {
      return
    }

    this.todosService.addTodo({
      title: this.todoTitle,
      completed: false
    }).subscribe(todo => {
      this.todos.push(todo)
      this.todoTitle = ''
    })
  }

  fetchTodos() {
    this.loading = true
    this.todosService.fetchTodos()
      .subscribe(todos => {
        this.todos = todos
        this.loading = false
      })
  }

  removeTodo(id: number) {
    this.todosService.removeTodo(id)
      .subscribe(() => {
        this.todos = this.todos.filter(t => t.id !== id)
      })
  }
}
```
-------------------------------
```
export class AppComponent implements OnInit {
  todos: Todo[] = []
  loading = false
  todoTitle = ''
  error = ''

  constructor(private todosService: TodosService) {}

  ngOnInit() {
    this.fetchTodos()
  }

  fetchTodos() {
    this.loading = true
    this.todosService.fetchTodos()
      .subscribe(todos => {
        this.todos = todos
        this.loading = false
      }, error => {
        this.error = error.message
      })
  }
}
```
-------------------------------
```
const headers = new HttpHeaders({
  'MyCustomHeader': Math.random().toString(),
})

return this.http.post<Todo>('https://jsonplaceholder.typicode.com/todos', todo, {
  headers
})
```
-------------------------------
```
fetchTodos(): Observable<Todo[]> {
let params = new HttpParams()
params = params.append('_limit', '4')
params = params.append('custom', 'anything')

return this.http.get<Todo[]>('https://jsonplaceholder.typicode.com/todos', {
  // params: new HttpParams().set('_limit', '3')
  params
})
  .pipe(
	delay(500),
	catchError(error => {
	  console.log('Error: ', error.message)
	  return throwError(error)
	})
  )
}
```
-------------------------------
```
fetchTodos(): Observable<Todo[]> {
let params = new HttpParams()
params = params.append('_limit', '4')
params = params.append('custom', 'anything')

return this.http.get<Todo[]>('https://jsonplaceholder.typicode.com/todos', {
  params,
  observe: 'response'
})
  .pipe(
	map(response => {
	  // console.log('Response', response)
	  return response.body
	}),
	delay(500),
	catchError(error => {
	  console.log('Error: ', error.message)
	  return throwError(error)
	})
  )
}

removeTodo(id: number): Observable<any> {
return this.http.delete<void>(`https://jsonplaceholder.typicode.com/todos/${id}`, {
  observe: 'events'
}).pipe(
  tap(event => {
	if (event.type === HttpEventType.Sent) {
	  console.log('Sent', event)
	}

	if (event.type === HttpEventType.Response) {
	  console.log('Response', event)
	}
  })
)
}

completeTodo(id: number): Observable<any> {
return this.http.put<Todo>(`https://jsonplaceholder.typicode.com/todos/${id}`, {
  completed: true
}, {
  responseType: 'json'
})
}
```
-------------------------------
```
import {HttpEvent, HttpHandler, HttpInterceptor, HttpRequest} from '@angular/common/http'
import {Observable} from 'rxjs'

export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    console.log('Intercept request', req)
    return next.handle(req)
  }
}
```

```
import {HTTP_INTERCEPTORS, HttpClientModule} from '@angular/common/http'
import {AuthInterceptor} from './auth.interceptor'

const INTERCEPTOR_PROVIDER: Provider = {
  provide: HTTP_INTERCEPTORS,
  useClass: AuthInterceptor,
  multi: true
}

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [INTERCEPTOR_PROVIDER],
  bootstrap: [AppComponent]
})
export class AppModule {
}
```
-------------------------------
```
import {HttpEvent, HttpEventType, HttpHandler, HttpInterceptor, HttpRequest} from '@angular/common/http'
import {Observable} from 'rxjs'
import {tap} from 'rxjs/operators'

export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    console.log('Intercept request', req)

    const cloned = req.clone({
      headers: req.headers.append('Auth', 'SOME RANDOM TOKEN')
    })

    return next.handle(cloned).pipe(
      tap(event => {
        if (event.type === HttpEventType.Response) {
          console.log('Interceptor response', event)
        }
      })
    )
  }
}
```
-------------------------------
```
import {NgModule} from '@angular/core'
import {RouterModule, Routes} from '@angular/router'
import {HomeComponent} from './home/home.component'
import {AboutComponent} from './about/about.component'
import {PostsComponent} from './posts/posts.component'

// http://localhost:4200/ -> HomeComponent
// http://localhost:4200/about -> AboutComponent
// http://localhost:4200/posts -> PostsComponent

const routes: Routes = [
  {path: '', component: HomeComponent},
  {path: 'about', component: AboutComponent},
  {path: 'posts', component: PostsComponent}
]

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {
}
```

```
import {AppRoutingModule} from './app-routing.module'

@NgModule({
  declarations: [
    AppComponent,
    AboutComponent,
    HomeComponent,
    PostsComponent,
    PostComponent,
    AboutExtraComponent,
  ],
  imports: [
    BrowserModule,
    FormsModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {
}
```

```
<nav class="navbar">
  <h1>
    <a [routerLink]="['/']">Angular Routing</a>
  </h1>
  <ul>
    <li routerLinkActive="active" [routerLinkActiveOptions]="{exact: true}">
      <a [routerLink]="['/']">Home</a>
    </li>
    <li routerLinkActive="active"><a routerLink="/posts">Posts</a></li>
    <li routerLinkActive="active"><a [routerLink]="['/about']">About</a></li>

    <li><button class="btn">Login</button></li>
    <li><button class="btn">Logout</button></li>
  </ul>
</nav>
```
-------------------------------
```
import {Component} from '@angular/core'
import {Router} from '@angular/router'

@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.scss']
})
export class HomeComponent {
  constructor(private router: Router) {}

  goToPostsPage() {
    this.router.navigate(['/posts'])
  }
}
```

```
<div>
  <button class="btn" (click)="goToPostsPage()">Go to Posts</button>
</div>
```
-------------------------------
```
<div class="card" *ngFor="let post of postsService.posts">
  <h4>
    <a [routerLink]="['/posts', post.id]">
      <strong>(ID {{post.id}})</strong>
      {{post.title}}
    </a>
  </h4>
</div>
```

```
import {Injectable} from '@angular/core'

export interface Post {
  title: string
  text: string
  id: number
}

@Injectable({providedIn: 'root'})
export class PostsService {
  posts: Post[] = [
    {title: 'Post 1', text: 'Sample text for post 1', id: 11},
    {title: 'Post 2', text: 'Sample text for post 2', id: 22},
    {title: 'Post 3', text: 'Sample text for post 3', id: 33},
    {title: 'Post 4', text: 'Sample text for post 4', id: 44},
  ]

  getById(id: number) {
    return this.posts.find(p => p.id === id)
  }
}
```
-------------------------------
```
import {ActivatedRoute, Params, Router} from '@angular/router'
import {Post, PostsService} from '../posts.service'

@Component({
  selector: 'app-post',
  templateUrl: './post.component.html',
  styleUrls: ['./post.component.scss']
})
export class PostComponent implements OnInit {

  post: Post

  constructor(
    private route: ActivatedRoute,
    private router: Router,
    private postsService: PostsService
  ) {}

  ngOnInit(): void {
    this.route.params.subscribe((params: Params) => {
      this.post = this.postsService.getById(+params.id)
    })
  }

  loadPost() {
    this.router.navigate(['/posts', 44])
  }
}
```
-------------------------------
```
<button
  class="btn"
  [routerLink]="['/posts']"
  [queryParams]="{showIds: true}"
  fragment="fragment"
>
  Show Ids
</button>

<button class="btn" (click)="showIdsProgram()">
  Show Ids (program)
</button>

<div class="card" *ngFor="let post of postsService.posts">
  <h4>
    <a [routerLink]="['/posts', post.id]">
      <strong *ngIf="showIds">(ID {{post.id}})</strong>
      {{post.title}}
    </a>
  </h4>
</div>
```

```
import {ActivatedRoute, Params, Router} from '@angular/router'

@Component({
  selector: 'app-posts',
  templateUrl: './posts.component.html',
  styleUrls: ['./posts.component.scss']
})
export class PostsComponent implements OnInit {
  showIds = false

  constructor(
    private postsService: PostsService,
    private route: ActivatedRoute,
    private router: Router
  ) {}

  ngOnInit(): void {
    this.route.queryParams.subscribe((params: Params) => {
      this.showIds = !!params.showIds
    })

    this.route.fragment.subscribe(fragment => {
      console.log('Fragment', fragment)
    })
  }

  showIdsProgram() {
    this.router.navigate(['/posts'], {
      queryParams: {
        showIds: true
      },
      fragment: 'program-fragment'
    })
  }
}
```
-------------------------------
```
// http://localhost:4200/ -> HomeComponent
// http://localhost:4200/about -> AboutComponent
// http://localhost:4200/posts -> PostsComponent
// http://localhost:4200/about/extra -> PostsComponent

const routes: Routes = [
  {path: '', component: HomeComponent},
  {path: 'about', component: AboutComponent, children: [
      {path: 'extra', component: AboutExtraComponent}
    ]},
  {path: 'posts', component: PostsComponent},
  {path: 'posts/:id', component: PostComponent}
]

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {

}
```

```
<p><a [routerLink]="['/about', 'extra']">Show Extra</a></p>

<router-outlet></router-outlet>
```
-------------------------------
```
const routes: Routes = [
  {path: '', component: HomeComponent},
  {path: 'about', component: AboutComponent, children: [
      {path: 'extra', component: AboutExtraComponent}
    ]},
  {path: 'posts', component: PostsComponent},
  {path: 'posts/:id', component: PostComponent},
  {path: 'error', component: ErrorPageComponent},
  {path: '**', redirectTo: '/error'}
]
```
-------------------------------
```
import {ActivatedRouteSnapshot, CanActivate, Router, RouterStateSnapshot} from '@angular/router'
import {Observable} from 'rxjs'
import {Injectable} from '@angular/core'
import {AuthService} from './auth.service'

@Injectable({providedIn: 'root'})
export class AuthGuard implements CanActivate {

  constructor(
    private authService: AuthService,
    private router: Router
  ) {}

  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): Observable<boolean> | Promise<boolean> | boolean {
    return this.authService.isAuthenticated().then(isAuth => {
      if (isAuth) {
        return true
      } else {
        this.router.navigate(['/'], {
          queryParams: {
            auth: false
          }
        })
      }
    })
  }
}
```

```
import {Injectable} from '@angular/core'

@Injectable({providedIn: 'root'})
export class AuthService {
  private isAuth = false

  login() {
    this.isAuth = true
  }

  logout() {
    this.isAuth = false
  }

  isAuthenticated(): Promise<boolean> {
    return new Promise(resolve => {
      setTimeout(() => {
        resolve(this.isAuth)
      }, 1000)
    })
  }
}
```

```
<li><button class="btn" (click)="auth.login()">Login</button></li>
<li><button class="btn" (click)="auth.logout()">Logout</button></li>
```
-------------------------------
```
@Injectable({providedIn: 'root'})
export class AuthGuard implements CanActivate, CanActivateChild {

  constructor(
    private authService: AuthService,
    private router: Router
  ) {}

  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): Observable<boolean> | Promise<boolean> | boolean {
    return this.authService.isAuthenticated().then(isAuth => {
      if (isAuth) {
        return true
      } else {
        this.router.navigate(['/'], {
          queryParams: {
            auth: false
          }
        })
      }
    })
  }

  canActivateChild(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
  ): Observable<boolean> | Promise<boolean> | boolean  {
    return this.canActivate(route, state)
  }
}
```
-------------------------------
```
import {NgModule} from '@angular/core'
import {AboutPageComponent} from './about-page.component'
import {AboutExtraPageComponent} from './about-extra-page/about-extra-page.component'
import {SharedModule} from '../shared/shared.module'
import {CommonModule} from '@angular/common'
import {RouterModule} from '@angular/router'

@NgModule({
  declarations: [
    AboutPageComponent,
    AboutExtraPageComponent,
  ],
  imports: [
    CommonModule,
    SharedModule,
    RouterModule.forChild([
      {
        path: 'about', component: AboutPageComponent, children: [
          {path: 'extra', component: AboutExtraPageComponent}
        ]
      }
    ])
  ],
  exports: [RouterModule]
})
export class AboutPageModule {
}
```

```
import {NgModule} from '@angular/core'
import {ColorDirective} from './color.directive'
import {PageNamePipe} from './page-name.pipe'

@NgModule({
  declarations: [
    ColorDirective,
    PageNamePipe
  ],
  exports: [
    ColorDirective,
    PageNamePipe
  ]
})
export class SharedModule {
}
```

```
import {NgModule} from '@angular/core'
import {RouterModule} from '@angular/router'
import {HomePageComponent} from './home-page/home-page.component'

@NgModule({
  imports: [RouterModule.forRoot([
    {path: '', component: HomePageComponent, pathMatch: 'full'}
  ])],
  exports: [RouterModule]
})
export class AppRoutingModule {
}
```

```
import {BrowserModule} from '@angular/platform-browser'
import {NgModule} from '@angular/core'

import {AppComponent} from './app.component'
import {FormsModule} from '@angular/forms'
import {HomePageComponent} from './home-page/home-page.component'
import {AppRoutingModule} from './app-routing.module'
import {AboutPageModule} from './about-page/about-page.module'
import {SharedModule} from './shared/shared.module'

@NgModule({
  declarations: [
    AppComponent,
    HomePageComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    AppRoutingModule,
    AboutPageModule,
    SharedModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {
}
```
-------------------------------
```
@NgModule({
  imports: [RouterModule.forRoot([
    {path: '', component: HomePageComponent, pathMatch: 'full'},
    {path: 'about', loadChildren: './about-page/about-page.module#AboutPageModule'}
  ])],
  exports: [RouterModule]
})
export class AppRoutingModule {
}
```
-------------------------------
```
import {Component, EventEmitter, Input, OnInit, Output} from '@angular/core'

@Component({
  selector: 'app-modal',
  templateUrl: './modal.component.html',
  styleUrls: ['./modal.component.scss']
})
export class ModalComponent implements OnInit {

  @Input() title = 'Default title'
  @Output() close = new EventEmitter<void>()

  constructor() { }

  ngOnInit() {
  }
}
```

```
<div class="modal">
  <nav class="navbar">
    <h1>{{ title }}</h1>
  </nav>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sequi, sint.
  </p>

  <button class="btn" (click)="close.emit()">Close</button>
</div>
```

```
<div class="container">
  <div class="card">

    <h1>Some content</h1>

    <button class="btn" (click)="modal = true">Show modal</button>

    <app-modal
      *ngIf="modal"
      title="Modal window"
      (close)="modal = false"
    ></app-modal>
  </div>
</div>
```
-------------------------------
```
import {Component, ComponentFactoryResolver, ViewChild} from '@angular/core'
import {ModalComponent} from './modal/modal.component'
import {RefDirective} from './ref.directive'

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {

  @ViewChild(RefDirective, {static: false}) refDir: RefDirective

  constructor(private resolver: ComponentFactoryResolver) {}

  showModal() {
    const modalFactory = this.resolver.resolveComponentFactory(ModalComponent)
    this.refDir.containerRef.clear()

    const component = this.refDir.containerRef.createComponent(modalFactory)

    component.instance.title = 'Dynamic title'
    component.instance.close.subscribe(() => {
      this.refDir.containerRef.clear()
    })
  }
}
```

```
import {Directive, ViewContainerRef} from '@angular/core'

@Directive({
  selector: '[appRef]'
})
export class RefDirective {
  constructor(public containerRef: ViewContainerRef) {
  }
}
```

```
import {BrowserModule} from '@angular/platform-browser'
import {NgModule} from '@angular/core'

import {AppComponent} from './app.component'
import {FormsModule} from '@angular/forms'
import {ModalComponent} from './modal/modal.component'
import {RefDirective} from './ref.directive'

@NgModule({
  declarations: [
    AppComponent,
    ModalComponent,
    RefDirective
  ],
  imports: [
    BrowserModule,
    FormsModule,
  ],
  providers: [],
  entryComponents: [ModalComponent],
  bootstrap: [AppComponent]
})
export class AppModule {
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
Каждый компонент имеет свой жизненный цикл (**Component Lifecycle**), в процессе которого вызываются ряд описывающих текущий этап методов (Angular Hooks):

- **OnChanges** - устанавливаются или изменяются значения входных свойств класса компонента;
- **OnInit** - устанавливаются "обычные" свойства; вызывается единожды вслед за первым вызовом OnChanges();
- **DoCheck** - происходит изменения свойства или вызывается какое-либо событие;
- **AfterContentInit** - в шаблон включается контент, заключенный между тегами компонента;
- **AfterContentChecked** - аналогичен DoCheck(), только используется для контента, заключенного между тегами компонента;
- **AfterViewInit** - инициализируются компоненты, которые входят в шаблон текущего компонента;
- **AfterViewChecked**- аналогичен DoCheck(), только используется для дочерних компонентов;
- **OnDestroy** - компонент "умирает", т. е. удаляется из DOM-дерева
-------------------------------
В Angular есть два варианта работы алгоритма отслеживания изменений:

- **OnPush**
- **Default (используется по умолчанию)**
-------------------------------
**ViewEncapsulation**:

- **Emulated: 0**. Emulates a native Shadow DOM encapsulation behavior by adding a specific attribute to the component's host element and applying the same attribute to all the CSS selectors provided via styles or styleUrls. This is the default option.

- **None: 2**. Doesn't provide any sort of CSS style encapsulation, meaning that all the styles provided via styles or styleUrls are applicable to any HTML element of the application regardless of their host Component.

- **ShadowDom: 3**. Uses the browser's native Shadow DOM API to encapsulate CSS styles, meaning that it creates a ShadowRoot for the component's host element which is then used to encapsulate all the Component's styling.
-------------------------------
- ```@Input() (```@Input() post: Post```)
- ```@Output()``` (```@Output() onAdd: EventEmitter<Post> = new EventEmitter<Post>()```)
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
- Область видимости сервисов и локальных сервисов в рамках компонента
- Реактивные формы
- Интерсептор
- routerLink
- routerLinkActive
- routerLinkActiveOptions
- router-outlet
- `implements CanActivate, CanActivateChild`
- Routing Resolver
- Lazy Load Module
- `Preloading Strategy` for imports
- `ng-template`
- `@ViewChild`
-------------------------------
- **Angular-interview-questions-RU:** https://github.com/FedorovAlexander/Angular-interview-questions-RU
