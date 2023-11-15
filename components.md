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
¿Cómo accedemos a estas propiedades en el componente hijo a la hora de renderizarlo? Por medio de las props. Veamos como con el código del componente `js <Menu />`:

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
En el método render creamos una variable **options** con el vslor que tenga `js this.props.options`. Este **options** dentro de props es el mismo atributo **options** que tiene el componente `js <Menu />` y es a través de props como le pasamos el valor desde el padre al componente hijo.

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