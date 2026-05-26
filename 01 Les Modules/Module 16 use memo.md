# UseMemo
## Exemple ultra simple : doubler un nombre avec useMemo


```js
import { useState, useMemo } from "react";

export default function App() {
  const [count, setCount] = useState(0);

  const double = useMemo(() => {
    console.log("Calcul exécuté !");
    return count * 2;
  }, [count]);

  return (
    <div>
      <h2>useMemo simple</h2>

      <p>Compteur : {count}</p>
      <p>Compteur x 2 : {double}</p>

      <button onClick={() => setCount(count + 1)}>
        +1
      </button>
    </div>
  );
}
```

Résumé

`double` est recalculé seulement quand `count` change.

Le `console.log` te montre quand `useMemo` s'exécute.

C’est parfait pour comprendre la base du hook.