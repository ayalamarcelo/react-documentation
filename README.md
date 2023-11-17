# React JSComponentes
**Propiedades**

Un componente ***React*** puede recibir propiedades como parámetros desde un componente padre para poder insertar valores y eventos en su **HTML**.

Imagina que tienes un componente que representa un menú con varias opciones, y éstas opciones las pasamos por parámetros como una propiedad llamada **Options**.

```js
import React from 'react'
class App extends React.Component {
 constructor() {
   super( )
 }
  render( ) {
   let menuOptions = ['Opción 1', 'Opción 2', 'Opción 3']
   return <Menu options={menuOptions} />
 }
}
```
¿Cómo accedemos a estas propiedades en el componente hijo a la hora de renderizarlo? Por medio de las props. Veamos como con el código del componente `<Menu />`:

```js
import React from 'react'
class Menu extends React.Component {
    constructor(props){
        super(props)
    }
    render(){
        let options = this.props.oprtions
        return (
            <ul>
            {oprtions.map(option => <li>{option}</li>)}
            </ul>
        )
    }
}
```
En el método render creamos una variable **options** con el vslor que tenga `this.props.options`. Este **options** dentro de props es el mismo atributo **options** que tiene el componente `<Menu />` y es a través de props como le pasamos el valor desde el padre al componente hijo.

```js 
import React from 'react'
import ReactDOM from 'react-dom'

 class App extends React.Component {
  constructor(props) {
  super(props)
  }
  render() {
  let menuOptions = ['Opción 1', 'Opción 2', 'Opción 3']
  return <Menu options={menuOptions} />
  }
 }
 class Menu extends React.Component {
  constructor(props) {
  super(props)
  }
  render( ) {
  let options = this.props.options
  return (
  <ul>
  {options.map(option => <li>{option}</li>)}
  </ul>
 )
 }
}

ReactDOM.render(<App />, document.getElementById('app'))
```
En el caso de ser un componente de tipo función las propiedades las recibimos como parámetro de la misma:

```jsx
function Welcome(props){
    return <h1>Hello, {props.name}</h1>;
}
```

## Estados

Además de las props, los componentes en React pueden tener estado. Lo característico del estado es que si éste cambia, el componente se renderiza automáticamente. Veamos un ejemplo de esto.
Si tomamos el código anterior y en el componente ` <App />` guardamos en su estado las opciones de menú, el código de App sería así:

```js
class App extends React.Component {
    constructor(props){
        super(props)
        this.state = {
            menuOptions:['Option 1', 'Option 2', 'Option 3']
        }
    }
    render(){
        return <Menu options={this.state.menuOptions}>
    }
} 
```

De ésta manera, las "opciones" pertenecen al estado de la aplicación (App) y se pueden pasar a componentes hijos (Menú) a través de las props.
Ahora, si queremos cambiar el estado, añadiendo una nueva opción al menú tenemos a nuestra disposición la función `setState`, que nos permite modificarlo.
Aprovechando esto, vamos a modificar el estado a través de un evento disparado desde el componente hijo hacia el padre.

## Eventos

Si las propiedades pasan de padres a hijos, es decir hacia abajo, los eventos se disparan hacia arriba, es decir de hijos a padres. Un evento que dispare un componente, puede ser recogido por el padre.
Veámoslo con un ejemplo. El componente `<Menu />` va a tener una nueva propiedad llamada `onAddOption`:

```js
render() {
    return (
        <Menu 
        options={this.state.menuOptions}
        onAddoption={this.handleAddOption.bind(this)}
        />
    )
}
```
Esta propiedad va a llamar a la función `handleAddOption` en `<App />` para poder modificar el estado:

```js
handleAddoption(){
    this.setState({
        menuOptions:this.state.menuOptions.concat(['Nueva Opcion'])    
        })
}
```
Cada vez que se lame a la función, añadirá al estado el ítem Nueva Opción. Como dijimos al inicio, cada vez que se modifique el estado, se "re-renderiza" el componente y veremos en el navegador la nueva opción añadida.

Para poder llamar a esa función, necesitamos disparar un evento desde el hijo. Voy a añadir un elemento `<button>` y utilizar el evento `onClick` de JSX, que simula al listener de click del mouse y ahí llamaré a la función "propiedad" `onAddOption` del padre.
JSX es una extensión de JS que se utiliza en React para definir la estructura de los componentes. La sintaxis JSX permite escribir componentes utilizando etiquetas HTML-like, lo que facilita la creación de interfaces de usuario y la separación de la lógica y la presentación de los componentes.

El código completo es:

```js
class App extends React.Component {
    constructor(props){
        super(props)
        this.state = {
            menuOptions:['Option 1', 'Option 2', 'Option 3']
        }
    }
    render(){
        return (
            <Menu
            options={this.state.menuOptions}
            onAddOption={this.handleAddOption.bind(this)}
            />
        )
    }
    handleAddOption(){
        this.setState({
            this.setState({
                menuOptions:this.state.menuOptions.concat(['Nueva Option'])
            })
        })
    }
}
```

```js
class Menu extends React.Component{
    constructor(props) {
        super(props)
    }
    render(){
        let options = this.props.options
        return(
            <div>
             <ul>
              {options.map(option => <li>{option}</li>)}
             </ul>
             <button onClick={this.props.onAddOption}>Nueva Opción</button>
            </div>)
    }
}

ReactDOM.render(<App />, document.getElementById('app'))
```

Cada vez que hagamos click en el botón, llamará a la función que le llega por props. Esta función, llama en el componente padre (App) a la función `handleAddOption` y la bindeamos con `this`, para que pueda llamar a `this.setState` dentro de la función. Este `setState` modifica el estado y llama internamente a la función render lo que provoca que se vuelva a  "pintar" todo de nuevo.

## Componentes

Los componentes permiten separar la interfaz de usuario en piezas independientes, reutilizables y pensar en cada pieza de forma aislada. Esta página proporciona una introducción a la idea de componentes.
Conceptualmente, los componentes son como las funciones de JS. Aceptan entradas arbitrarias (llamadas "props") y retornan elementos de React que describem lo que debe aparecer en la pantalla.

**Componentes funcionales**

La forma más sencilla de definir un componente es escribir una función de JS:

```js
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}
```

Esta función es un componete de React válido porque acepta un solo argumento de objeto "props" (que proviene de propiedad) con datos y devuelve un elemento de React. Llamamos a dichos componentes "funcionales" porque literalmente son funciones JS.
También puedes utilizar una clase de ES6 para definir un componente:

