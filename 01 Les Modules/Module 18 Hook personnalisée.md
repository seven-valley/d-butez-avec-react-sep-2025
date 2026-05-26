#  Custom Hook ultra simple : `useToggle`

Ce hook permet juste de basculer entre true et false.
https://fr.react.dev/reference/react/hooks

```js
// useToggle.js
import { useState } from "react";

export function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);

  const toggle = () => setValue((v) => !v);

  return { value, toggle };
}
```

```js
import { useToggle } from "./useToggle";

export default function App() {
  const { value, toggle } = useToggle();

  return (
    <div>
      <h2>Custom Hook simple</h2>

      <p>Valeur actuelle : {value ? "ON" : "OFF"}</p>

      <button onClick={toggle}>Basculer</button>
    </div>
  );
}
```

# Pourquoi ce hook est intéressant ?

- Il résume le principe d’un hook :  
extraire une logique réutilisable dans une fonction.

- Il ne dépend d’aucune API externe.

- Il se comprend en 5 secondes.

- Il montre que l’on peut retourner des valeurs, des fonctions, ou ce qu’on veut.
