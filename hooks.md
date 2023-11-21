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