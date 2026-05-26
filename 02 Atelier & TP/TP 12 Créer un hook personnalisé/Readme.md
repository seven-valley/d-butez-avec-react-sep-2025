# Créer un hook :


Créer un hook useCounter() qui :  
  
initialise un compteur à 0  
  
retourne :
  
count → la valeur actuelle  
  
increment() → ajoute +1  
  
decrement() → enlève -1  
  
Utiliser ce hook dans un composant avec 2 boutons.  
  

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

--------------------------------



Créer un hook useLocalStorage(key, defaultValue) qui :



lit la valeur dans localStorage au montage  

sauvegarde automatiquement la valeur à chaque changement  

retourne [value, setValue]  

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
