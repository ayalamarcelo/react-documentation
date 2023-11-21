# Hooks
Son una nueva característica en React 16.8. Estos te permiten usar el estado y otras características de **React** sin escribir una clase.

*useState* es un hooj en reactm y el mismo lo utilizaremos para el manejo de estados.

```js
import React, { useState } from 'react';

function Example() {
    // Declara una nueva variable de estado, la cual llamaremos "count"

    const [count, setCount] = useState(0);

    return (
        <div>
        <p>You clicked {count} times</p>
        <button onClick={ => setCount(count + 1)}>
        Click me
        </button>
        </div>
    );
}
```
## Hooks de estados
Dentro de un componente funcional llamamos al método *useState* y de esta forma agregamos un estado local al mismo. React mantendrá este estado entre re-renderizados.

*useState* devuelve un par: el valor de estado actual y una función que le permite actualizarlo. Puedes llamar a esta función desde un controlador de eventos o desde otro lugar.
EL único argumento para *useState* es el estado inicial. El argumento de estado inicial solo se usa durante el primer renderizado.

```js
import React, { useState } from 'react';

function Example() {
    // Declara una nueva variable de estado, que llamaremos "count".

    const [count, setCount] = useState(0);

    return (
        <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
        Click me
        </button>
        </div>
    );
}
```

## Hooks de efectos
El hook de efecto, *useEffect*, agrega la capacidad de realizar efectos secundarios desde un componente funcional. Tiene el mismo propósito que **componentDidMount, componentDidUpdate y componentWillUnmount** en las clases React, pero unificadas en una sola API.
Declaramos la variable de estado count y le indicamos a react que necesitamos usar un efecto. Le pasamos una función al Hook *useEffect*. Detro de nuestro efecto actualizamos el título del documento usando la API del navegador document.title. Cuando React renderiza nuestro componente, recordará este efecto y lo ejecutará después de actualizar el DOM. Esto sucede en cada renderizado, incluyendo el primero.

```js
import React, { useState, useEffect } from 'react';

function Example() {
    const [count, setCount] = useState(0);

    useEffect(() => {
        document.title = `You clicked ${count} times`;
    });

    return (
        <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
        Click me
        </button>
        </div>
    );
}
```

## useReducer
Acepta un reducer de tipo (state, action) = newState y devuelve el estado actual emparejado con método dispatch.

**useReducer** a menudo es preferible a *useState* cuando se tiene una lógica compleja que involucra múltiples subvalores o cuando el próximo estado depende del anterior. *useReducer* además te permite optimizar el rendimiento para componentes que activan actualizaciones profundas, porque puedes pasar hacia abajo dispatch en lugar de callbacks.

hoja 6