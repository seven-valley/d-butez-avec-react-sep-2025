# Module 4 - Ma première application
![module-4](../img/04/module-4.png)
  
## 2 façon d'écrire "export default"
Peut s'écrire de 2 façon  
écomomise une ligne

```tsx
import './App.css'

function App() {
  return (
    <h1>hello World !</h1>
  )
}
export default App
```

## ou bien

```tsx
import './App.css'

export default function App() {
  return (
    <h1>hello World !</h1>
  )
}
```

## les balises fragments
```tsx
export default function App() {
  return (
    <> {/*balise framgments */}
     <h1>Hello</h1>
    <h2>Brad PITT !</h2>
    </>
  )
}
```

# Mise en place de ma première application
:one: Mise en place d’un formlaire  
:two: L’action : (le bouton) gestion du "submit"  
:three: Mise en place de useState  

## :one: Mise en place du formulaire
```tsx
return (
    <> 
    <form action={affiche}>
      <input name="prenom" />
      <input name="nom" />
      <button type="submit">Valider</button>
    </form>
    </>
  )
```
Ajouter des valeurs par défaults aux champs input  

```tsx
return (
    <> 
    <form action={affiche}>
      <input name="prenom" defaultValue="Brad" />
      <input name="nom" defaultValue="PITT" />
      <button type="submit">Valider</button>
    </form>
    </>
  )
```
## :two: L’action : (le bouton) gestion du "submit"



```tsx
export default function App() {
  function affiche(formData) {
    const prenom = formData.get('prenom');
    const nom = formData.get('nom');
    console.log(`${prenom} ${nom}`);
  };
  return (
    <>
      <form action={affiche}>
        <input name="prenom" defaultValue="Brad" />
        <input name="nom" defaultValue="PITT" />
        <button type="submit">Valider</button>
      </form>
    </>
  );
}
```
  
Encore mieux avec les fonctions fléchées : **arrow function**
  
```tsx
export default function App() {
  const affiche = (formData) => {
    const prenom = formData.get('prenom');
    const nom = formData.get('nom');
    console.log(`${prenom} ${nom}`);
  };
  return (
    <>
      <form action={affiche}>
        <input name="prenom" defaultValue="Brad" />
        <input name="nom" defaultValue="PITT" />
        <button type="submit">Valider</button>
      </form>
    </>
  );
}
```
## :three: Mise en place de useState  

```tsx
import "./App.css";
import {useState} from 'react'; // 1: importer

export default function App() {
  const [message,setMessage] = useState('') // 2: declarer
    const affiche = (formData) => {
    const prenom = formData.get('prenom');
    const nom = formData.get('nom');
    setMessage('Hello '+prenom + " " + nom);
  };
  
  return (
    <>
      <form action={affiche}>
        <input name="prenom" defaultValue="Brad" />
        <input name="nom" defaultValue="PITT" />
        <button type="submit">Valider</button>
      </form>
       <h1>{message}</h1> {/* 3: utiliser */}
    </>
  );
}
```

## Mise en place des littéraux de gabarit :heart_eyes:  

### :rocket: Avec la cerise sur le gateau : **${}**
```tsx
import "./App.css";
import {useState} from 'react';// 1: importer
export default function App() {
  const [message,setMessage] = useState('') // 2: declarer
  const affiche = (formData) => {
    const prenom = formData.get('prenom');
    const nom = formData.get('nom');
    setMessage(`Hello ${prenom} ${nom}`); // la cerise ;)
  };
  return (
    <>
      <form action={affiche}>
        <input name="prenom" defaultValue="Brad" />
        <input name="nom" defaultValue="PITT" />
        <button type="submit">Valider</button>
      </form>
      <h1>{message}</h1> {/* 3: utiliser */}
    </>
  );
}
```

### Modifier le CSS avec des "class" dynamiques dans className

```ts
import { useState } from "react";


export default function App() {
  // zone des variables et fonction
  // let info = 'test'; // cela ne marche pas
  const [info,setInfo]= useState({
    prenom:'',
    nom:'',
    age:'',
    myClass:''
  });
  const afficher =(formData)=>{
    const info2 ={};
    const prenom = formData.get('prenom');
    const nom = formData.get('nom');
    const age = formData.get('age');
    info2.prenom = prenom;
    info2.nom = nom;
    info2.age = age;
    if (age >= 18){
      info2.myClass='success'
    }else{
      info2.myClass='danger'
    }
    setInfo(info2)
    // info= `${prenom} ${nom}`;
  }
  // return jsx
  return (
    <>
      <div className="container">
        <div className="col-4">
          <h1>Formulaire</h1>
          <form action={afficher}>
          <input className="form-control my-2" type="text" name="prenom" placeholder="Prénom"/>
          <input className="form-control my-2" type="text" name="nom" placeholder="Nom" />
          <input className="form-control my-2" type="text" name="age" placeholder="Age" />
          <button className="btn btn-primary" type="submit"> GO </button>
          </form>
          <h2>{info.prenom} {info.nom}</h2>
          { info.prenom.length > 0 &&
            <div className={`alert alert-${info.myClass}`}>
              {
                info.age > 18 ? <p>ENTREZ</p>: <p>Interdit</p>
              }
            </div>
          }
          {/* <div className="alert alert-success">
            ENTREZ
          </div>
          <div className="alert alert-danger">
            Interdit !
          </div> */}
        </div>
      </div>
    </>
  )
}
```

## Ajouter Bootstrap et ses classes
```tsx
import "./App.css";
import {useState} from 'react';// 1: importer
export default function App() {
  const [message,setMessage] = useState('') // 2: declarer
  const affiche = (formData) => {
    const prenom = formData.get('prenom');
    const nom = formData.get('nom');
    setMessage(`Hello ${prenom} ${nom}`); // la cerise ;)
  };
  return (
    <div className="container">
      <div className="col-4">
        <h1> Démo</h1>
      <form action={affiche}>
        <input name="prenom" 
        className="form-control" 
        placeholder="Prénom"/>
        <input name="nom" 
        className="form-control my-3"
        placeholder="Nom" />
        <button type="submit" className="btn btn-primary">
          Valider</button>
      </form>
      <h1>{message}</h1> {/* 3: utiliser */}
      </div>
      </div>
  );
}
```

# Modifier le CSS avec les template de gabarits ${}
Remplacer la concaténation par **${}**  
<img src="../img/04/btn1.png" width="100"> <img src="../img/04/btn2.png" width="100">
  
<br>

```jsx
import { useState } from 'react'

export default function App() {
  const [etat,setEtat]= useState(true)

  const changer =()=>{
    setEtat(!etat)
  }
  return (
    <div className="container">
      {/* className="btn btn-success" OU className="btn btn-danger" */}
      <button 
        className={`btn btn-${etat? 'danger': 'success'}`} 
        onClick={changer}>{etat ? 'OFF' : 'ON'}</button>

      <h1>{etat ? 'ON' : 'off'}</h1>
    </div>
  )
}
```

