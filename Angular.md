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
-------------------------------
- **Angular-interview-questions-RU:** https://github.com/FedorovAlexander/Angular-interview-questions-RU
