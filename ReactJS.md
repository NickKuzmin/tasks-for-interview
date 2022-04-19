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
