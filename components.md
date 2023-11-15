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