- https://github.com/XOP/css-codeguide
- https://github.com/chrisjames-work/css-guide

- LESS/SASS/SCSS
----------------------------------------
- https://csslayout.io/
----------------------------------------
*Questions*:
- What is the difference between SASS vs SCSS?
- LESS: Mixin vs Extend/Inheritance?
----------------------------------------
## LESS:

**Переменные в LESS:**
```
@header-font: Georgia;
h1, h2, h3, h4 {
    font-family: @header-font;
}
.large {
    font-family:@header-font;
}
```

**Цветовые операции:**
- Если вы хотите изменить значение цвета, то можете сделать это вычитанием или добавлением другого цвета.
```
@color: #941f1f;
button {
    background: #941f1f + #222222;
    border: #941f1f - #111111;
}
```

**Цветовые функции:**
```
@color: #3d82d1;
.left_box {
    background:lighten(@color, 20%);
}
.right_box {
    background:darken(@color, 20%);
}
```

**Примеси (mixins):**
-  Примеси – элементы многоразового использования, которые можно добавить к любому элементу как правило:
```
.rounded_top {
    -webkit-border-top-left-radius: 6px;
    -webkit-border-top-right-radius: 6px;
    -moz-border-radius-topleft: 6px;
    -moz-border-radius-topright: 6px;
    border-top-left-radius: 6px;
    border-top-right-radius: 6px;
}
.tab {
    background: #333;
    color:#fff;
    .rounded_top;
}
.submit {
    .rounded_top;
}
```

**Примеси с параметрами:**
```
.rounded_top(@radius) {
    -webkit-border-top-left-radius: @radius;
    -webkit-border-top-right-radius: @radius;
    -moz-border-radius-topleft: @radius;
    -moz-border-radius-topright: @radius;
    border-top-left-radius: @radius;
    border-top-right-radius: @radius;
}
.tab {
    background: #333;
    color:#fff;
    .rounded_top(6px);
}
.submit {
    .rounded_top(3px);
}
```

**Пространство имён:**
```
#my_framework {
    p {
        margin: 12px 0;
    }
    a {
        color:blue;
        text-decoration: none;
    }
    .submit {
        background: red;
        color: white;
        padding:5px 12px;
    }
}
```
