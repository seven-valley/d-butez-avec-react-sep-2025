# useCallback
## Exemple ultra simple : mémoriser une fonction d’incrément

`useCallback` sert à **mémoriser une fonction** pour éviter qu’elle soit recréée à chaque rendu.
Ici, on mémorise une fonction `increment`.
```js
import { useState, useCallback } from "react";

export default function App() {
  const [count, setCount] = useState(0);

  // useCallback mémorise la fonction
  const increment = useCallback(() => {
    setCount((c) => c + 1);
  }, []);

  return (
    <div>
      <h2>useCallback simple</h2>

      <p>Compteur : {count}</p>

      <button onClick={increment}>+1</button>
    </div>
  );
}
```

## Résumé

- Sans `useCallback`, la fonction `increment` serait recréée à chaque rendu du composant.
- Avec `useCallback([])`, la fonction est créée **une seule fois**.
- C’est utile ➝ **quand on passe une fonction en props** à un composant optimisé (React.memo).


