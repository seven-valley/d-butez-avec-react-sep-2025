# TP 03 - Domotique

```
|-- src
        |-- models
            |-- Apppareil.js
```

## Appareil.js
```jsx
export default class Appareil{
    constructor(name){
        this.name= name
        this.status = true
    }
}
```

```
|-- src
        |-- components
            |-- ApppareilComponents.jsx
```

## AppareilComponent.jsx
```jsx
export default function AppareilComponent({appareil,indice,switchOne}) {
    return (
        <li className={`list-group-item list-group-item-${appareil.status ? 'success' :'danger'}`}>
            <h4>{appareil.name} -- {appareil.status ? 'Allumé' :'Eteint'}</h4>

            <button 
            className={`btn btn-${appareil.status ? 'danger' :'success'} me-3`} 
            onClick={()=>switchOne(indice)}>
                {appareil.status ? 'OFF' :'ON'}
                </button>

            
        </li>
    )
}
```

## App.jsx
```jsx
import { useEffect, useState } from "react";
import AppareilComponent from "./components/AppareilComponent";
import Appareil from "./models/Appareil.js";


export default function App() {
  const [appareils,setAppareils]= useState([]);
  useEffect(()=>{
    console.log('useEffect');
    const a = new Appareil('PlayStation 5');
    const appareils2 =[]
    appareils2.push(a);
    setAppareils(appareils2)
  },[])
  const ajouter = (formData) => {
    const nom = formData.get('nom');
    const appareil = new Appareil(nom);
    console.log(appareil);
    setAppareils([...appareils,appareil])
  }
  const switchOne=(indice)=>{
    appareils[indice].status =  !appareils[indice].status
    setAppareils([...appareils])
  }
  const switchAll=(status)=>{
   appareils.map(a => a.status =status);
   setAppareils([...appareils])
  }
  return (
    <>
      <div className="container">
        <div className="row">
          <div className="col-4">
            <h2>Les Appareils</h2>
            <form action={ajouter}>
              <input 
              type="text" 
              className="form-control" 
              placeholder="Appareil"
              name="nom"
              />
              <button className="btn btn-secondary my-3" type="submit">
                <i className="fa fa-plus"></i>
              </button>
            </form>
            <ul className="list-group">
              {
              appareils.map((appareil,i)=><AppareilComponent
              appareil={appareil}
              indice={i}
              switchOne={switchOne}
              key={i}
              />)
              }
            </ul>
            <br />
            <button 
            onClick={()=>switchAll(true)}
            className="btn btn-success me-3">ALL ON</button>

            <button 
            onClick={()=>switchAll(false)}
            className="ml-2 btn btn-danger">ALL OFF</button>
          </div>
        </div>
      </div>
    </>

  )
}
```

## App.jsx avec react hook form
```jsx
import { useEffect, useRef, useState } from "react"
import { useForm } from "react-hook-form"
import Appareil from './models/Appareil'
import AppareilComponent from "./components/AppareilComponent";

export default function App() {

  const [appareils, setAppareils] = useState([]);

  const {
    register,
    handleSubmit,
    formState: { errors }
  } = useForm();
  const ajouter = (data) => {
    const name = data.appareil;
    const appareil = new Appareil(name);
    setAppareils([...appareils, appareil])
  }
  useEffect(() => {
    const appareils2 = [
      { name: 'Tv Oled', status: true }
    ]
    setAppareils(appareils2)
  }, [])
  const switchAll=(status)=>{
    const appareils2 =[...appareils];
    appareils2.map(a=> a.status=status);
     setAppareils(appareils2)
  }
    const switchOne=(indice)=>{
    const appareils2 =[...appareils];
    appareils2[indice].status = !appareils2[indice].status;
     setAppareils(appareils2);
  }
  return (
    <>
      <div className="container">
        <div className="col-4">
          <h2>Les Appareils</h2>
          <form onSubmit={handleSubmit(ajouter)}>

            <input
              placeholder="Appareil"
              type="text"
              className={`form-control  my-2 ${errors.appareil && 'is-invalid'}`}
              id="appareil"
              {...register('appareil', {
                required: 'Veillez remplir ce champ',
                minLength: {
                  value: 3, message: '3 caractères minimun',
                  
                }
                pattern: { value:/^[A-Za-z]+$/i, message: 'svp pas de chiffres' }
              })} />
            <div className="invalid-feedback">
              {errors.appareil && errors.appareil.message}
            </div>
            <button className="btn btn-success">GO</button>
          </form>
          <ul className="list-group my-3">
              {
              appareils.map((a,i)=>
              <AppareilComponent 
              appareil={a}
              indice={i}
              switchOne={switchOne}
              key={i}
              />)
            }
          </ul>
          <button 
            onClick={()=>switchAll(true)}
            className="btn btn-success me-3">ALL ON</button>

            <button 
            onClick={()=>switchAll(false)}
            className="ml-2 btn btn-danger">ALL OFF</button>
        </div>
      </div>
    </>
  )
}
```