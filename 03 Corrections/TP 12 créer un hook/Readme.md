# TP 12 Créer un hook 





Créer un hook useCounter() qui :  
  
initialise un compteur à 0  
  
retourne :
  
count → la valeur actuelle  
  
increment() → ajoute +1  
  
decrement() → enlève -1  
  
Utiliser ce hook dans un composant avec 2 boutons.  
  

```js
import { useState } from "react";

export function useCounter() {
  const [count, setCount] = useState(0);

  const increment = () => setCount(prev => prev + 1);
  const decrement = () => setCount(prev => prev - 1);

  return { count, increment, decrement };
}
```

```js
import { useCounter } from "./useCounter";

export default function App() {
  const { count, increment, decrement } = useCounter();

  return (
    <div>
      <h1>Compteur : {count}</h1>

      <button onClick={increment}>+1</button>
      <button onClick={decrement}>-1</button>
    </div>
  );
}

```

-----------------------------
Créer un hook useLocalStorage(key, defaultValue) qui :  
  
lit la valeur dans localStorage au montage  

sauvegarde automatiquement la valeur à chaque changement  

retourne [value, setValue]  


```js
import { useState, useEffect } from "react";

export function useLocalStorage(key, defaultValue) {
  const [value, setValue] = useState(() => {
    const stored = localStorage.getItem(key);
    return stored !== null ? JSON.parse(stored) : defaultValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}

```

```js
import { useLocalStorage } from "./useLocalStorage";

export default function App() {
  const [name, setName] = useLocalStorage("username", "");

  return (
    <div>
      <input 
        value={name}
        onChange={e => setName(e.target.value)}
        placeholder="Ton nom..."
      />
      <p>Bonjour {name}</p>
    </div>
  );
}

```