- Life cycle: https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/
- https://habr.com/ru/post/429712/
- https://habr.com/ru/company/ruvds/blog/444348/
---------------------------------------------------------
- Функциональные компоненты.
- Children компоненты.
- Hooks (Хуки): useState(), useEffect(), useContext(), useRef(), useMemo(), userCallback(), useReducer()
- Component based framework
- jsx-синтаксис
---------------------------------------------------------
- `npm install -g create-react-app`
- `create-react-app <react-app-name>`
---------------------------------------------------------
```
<div id="root"></div>

<script type="text/babel">
    function Car(props) {
      return (
        <div className="car">
          <h3>{props.name}</h3>
          <p>Year: <strong>{props.year}</strong></p>
            <small>This is car</small>
        </div>
      )
    }

    const App = (
      <div>
        <Car name="Ford Focus" year="2017" />
        <Car name="Audi A8" year="2015" />
        <Car name="Mazda 3" year="2010" />
      </div>
    )

    ReactDOM.render(
      App,
      document.querySelector('#root')
    )
</script>
```
---------------------------------------------------------
```
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <h1>Hello world!</h1>
      </div>
    );
  }
}

export default App;
```

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
registerServiceWorker();
```
---------------------------------------------------------
```
class App extends Component {
  render() {
    return (
      <div className="App">
        <h1>Hello world!</h1>
      </div>
    );

    // return React.createElement(
    //   'div',
    //   {
    //     className: 'App'
    //   },
    //   React.createElement(
    //     'h1',
    //     null,
    //     'Hello world!'
    //   )
    // )
  }
}
```
---------------------------------------------------------
**Не разрешено:**

```
return (
  <div className="App">
	<h1>Hello world!</h1>
  </div>
  <p>Hello</p>
);
```

**Должно быть обернуто в корневой div:**

```
return (
  <div>
	<div className="App">
		<h1>Hello world!</h1>
		</div>
	<p>Hello</p>
  </div>
);
```
---------------------------------------------------------
**Inline styles:**

`'font-size' = fontSize`

```
class App extends Component {
  render() {
    const divStyle = {
      textAlign: 'center'
    }

    return (
      <div style={divStyle}>
        <h1 style={{color: 'blue', fontSize: '20px'}}>Hello world!</h1>
      </div>
    );
  }
}
```

```
class App extends Component {
  render() {
    const divStyle = {
      'text-align': 'center'
    }

    return (
      <div style={divStyle}>
        <h1 style={{color: 'blue', 'font-size': '20px'}}>Hello world!</h1>
      </div>
    );
  }
}
```
---------------------------------------------------------
```
import React from 'react'

// function car() {
//   return (
//     <div>This is car component</div>
//   )
// }

// const car = () => {
//   return (
//     <div>This is car component</div>
//   )
// }

// const car = () => (
//   <div>
//     This is car component
//     <strong>test</strong>
//   </div>
// )

export default () => (
  <div>
    This is car component
    <strong>test</strong>
  </div>
)
```

```
import React, { Component } from 'react';
import './App.css';
import Car from './Car/Car'

class App extends Component {
  render() {
    const divStyle = {
      textAlign: 'center'
    }

    return (
      <div style={divStyle}>
        <h1>Hello world!</h1>

        <Car />
      </div>
    );
  }
}
```
---------------------------------------------------------
```
export default () => (
  <div>
    <p>This is car component</p>
    <p>Number: <strong>{Math.round(Math.random() * 100)}</strong></p>
  </div>
)
```
---------------------------------------------------------
**Передача контента (children):**

```
class App extends Component {
  render() {
    const divStyle = {
      textAlign: 'center'
    }

    return (
      <div style={divStyle}>
        <h1>Hello world!</h1>

        <Car name={'Ford'} year={2018}>
          <p style={{color: 'blue'}}>COLOR</p>
        </Car>
        <Car name="Audi" year={2016}>
          <p style={{color: 'red'}}>COLOR</p>
        </Car>
        <Car name={'Mazda'} year={2010} />
      </div>
    );
  }
}
```

```
export default props => (
  <div>
    <h3>Сar name: {props.name}</h3>
    <p>Year: <strong>{props.year}</strong></p>
    { props.children }
  </div>
)
```
---------------------------------------------------------
**State:**

```
class App extends Component {
  state = {
    cars: [
      {name: 'Ford', year: 2018},
      {name: 'Audi', year: 2016},
      {name: 'Mazda', year: 2010}
    ],
    pageTitle: 'React components'
  }

  render() {
    const divStyle = {
      textAlign: 'center'
    }

    const cars = this.state.cars

    return (
      <div style={divStyle}>
        <h1>{this.state.pageTitle}</h1>

        <Car name={cars[0].name} year={cars[0].year} />
        <Car name={cars[1].name} year={cars[1].year} />
        <Car name={cars[2].name} year={cars[2].year} />
      </div>
    );
  }
}
```
---------------------------------------------------------
**Изменение state:**

```
class App extends Component {
  state = {
    cars: [
      {name: 'Ford', year: 2018},
      {name: 'Audi', year: 2016},
      {name: 'Mazda', year: 2010}
    ],
    pageTitle: 'React components'
  }

  changeTitleHandler = (newTitle) => {
    this.setState({
      pageTitle: newTitle
    })
  }

  render() {
    const divStyle = {
      textAlign: 'center'
    }

    const cars = this.state.cars

    return (
      <div style={divStyle}>
        <h1>{this.state.pageTitle}</h1>

        <button
          onClick={this.changeTitleHandler.bind(this, 'Changed!')}
        >Change title</button>

        <Car
          name={cars[0].name}
          year={cars[0].year}
          onChangeTitle={this.changeTitleHandler.bind(this, cars[0].name)}
        />
        <Car
          name={cars[1].name}
          year={cars[1].year}
          onChangeTitle={() => this.changeTitleHandler(cars[1].name)}
        />
        <Car
          name={cars[2].name}
          year={cars[2].year}
          onChangeTitle={() => this.changeTitleHandler(cars[2].name)}
        />
      </div>
    );
  }
}
```
---------------------------------------------------------
**Синтаксис функций:**

```
changeTitleHandler: function() {
    console.log(this.name);
}
```

```
changeTitleHandler() {
	console.log(this.name);
}
```

```
changeTitleHandler = () => {
    console.log(this.name);
}
```
---------------------------------------------------------
**Изменение State:**

**Не изменять вручную:**
```
changeTitleHandler: function() {
    this.state.pageTitle = 'Changed';
}
```

**Необходимо через setState:**
```
changeTitleHandler: function() {
	const oldTitle = this.state.pageTitle;
	const newTitle = oldTitle + ' (changed)';
	
	this.setState({
		pageTitle: newTitle
	});
}
```
---------------------------------------------------------
**Обработка Input:**

```
class App extends Component {

  state = {
    cars: [
      {name: 'Ford', year: 2018}
    ]
  }

  handleInput = (event) => {
    this.setState({
      pageTitle: event.target.value
    })
  }

  render() {
    return (
       <input type="text" onChange={this.handleInput} />
    );
  }
}
```
---------------------------------------------------------
**Работа со списками:**

```
class App extends Component {
  state = {
    cars: [
      {name: 'Ford', year: 2018},
      {name: 'Audi', year: 2016},
      {name: 'Mazda', year: 2010}
    ]
  }

  render() {
    return (
      <div>
        { this.state.cars.map((car, index) => {
          return (
            <Car
              key={index}
              name={car.name}
              year={car.year}
              onChangeTitle={() => this.changeTitleHandler(car.name)}
            />
          )
        }) }
      </div>
    );
  }
}
```
---------------------------------------------------------
**Работа с условными операторами:**

```
class App extends Component {
  state = {
    cars: [
      {name: 'Ford', year: 2018},
      {name: 'Audi', year: 2016},
      {name: 'Mazda', year: 2010}
    ],
    showCars: false
  }

  toggleCarsHandler = () => {
    this.setState({
      showCars: !this.state.showCars
    })
  }

  render() {
    let cars = null

    if (this.state.showCars) {
      cars = this.state.cars.map((car, index) => {
        return (
          <Car
            key={index}
            name={car.name}
            year={car.year}
            onChangeTitle={() => this.changeTitleHandler(car.name)}
          />
        )
      })
    }

    return (
      <div>
        <h1>{this.state.pageTitle}</h1>

        <button
          onClick={this.toggleCarsHandler}
        >Toggle cars</button>

        { cars }
      </div>
    );
  }
}
```
---------------------------------------------------------
**Динамические списки:**

```
class App extends Component {
  state = {
    cars: [
      {name: 'Ford', year: 2018},
      {name: 'Audi', year: 2016},
      {name: 'Mazda', year: 2010}
    ],
    pageTitle: 'React components',
    showCars: false
  }

  toggleCarsHandler = () => {
    this.setState({
      showCars: !this.state.showCars
    })
  }

  onChangeName(name, index) {
    const car = this.state.cars[index]
    car.name = name
    const cars = [...this.state.cars]
    cars[index] = car
    this.setState({cars})
  }

  deleteHandler(index) {
    const cars = this.state.cars.concat()
    cars.splice(index, 1)

    this.setState({cars})
  }

  render() {
    let cars = null

    if (this.state.showCars) {
      cars = this.state.cars.map((car, index) => {
        return (
          <Car
            key={index}
            name={car.name}
            year={car.year}
            onDelete={this.deleteHandler.bind(this, index)}
            onChangeName={event => this.onChangeName(event.target.value, index)}
          />
        )
      })
    }

    return (
      <div
        <h1>{this.state.pageTitle}</h1>

        <button
          onClick={this.toggleCarsHandler}
        >Toggle cars</button>

        { cars }
      </div>
    );
  }
}
```
---------------------------------------------------------
**Контекст в хендлерах:**

```
deleteHandler() {
    const cars = this.state.cars.concat()
    cars.splice(index, 1)

    this.setState({cars})
}

<Car key={index}
    onDelete={this.deleteHandler.bind(this)}
    onChangeName={event => this.onChangeName(event.target.value, index)} />
```

**Либо использование стрелочной функции:**
```
deleteHandler = () => {
    const cars = this.state.cars.concat()
    cars.splice(index, 1)

    this.setState({cars})
}

<Car key={index}
    onDelete={this.deleteHandler}
    onChangeName={event => this.onChangeName(event.target.value, index)} />
```
---------------------------------------------------------
**Inline styles:**

```
render() {
	return (
	  <div style={{
		  width: 400,
		  margin: 'auto',
		  paddingTop: '20px'
		}}>
	);
}
```
