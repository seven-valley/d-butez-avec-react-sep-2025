# TP 00 Next génération Correction

## EXERCICES
**Excercice 1**  
Créer le tableau  **nouveauClients** à partir de personnes et clients  
utiliser <code>.filter</code> et <code>.find</code>
```js
const personnes =[
    {id:1,nom:'Brad',prenom:'PITT'},
    {id:2,nom:'Bruce',prenom:'WILLIS'},
    {id:3,nom:'Angelina',prenom:'Jolie'},
    {id:4,nom:'Tom',prenom:'CRUISE'}
];
const clients =[
    {id:1,nom:'BRAD',prenom:'PITT'},
    {id:3,nom:'Angelina',prenom:'Jolie',age:16}
];
// const nouveauClients =[
//         {id:2,nom:'Bruce',prenom:'WILLIS'},
//         {id:4,nom:'Tom',prenom:'CRUISE'}
//     ];
```
**Excercice 2**  
Créer le tableau  **dejaClients** à partir de personnes et clients  
utiliser <code>.filter</code> et <code>.find</code>
```js
const personnes =[
    {id:1,nom:'Brad',prenom:'PITT'},
    {id:2,nom:'Bruce',prenom:'WILLIS'},
    {id:3,nom:'Angelina',prenom:'Jolie'},
    {id:4,nom:'Tom',prenom:'CRUISE'}
];
const clients =[
    {id:1,nom:'BRAD',prenom:'PITT'},
    {id:3,nom:'Angelina',prenom:'Jolie',age:16}
];
// const dejaClients =[
//     {id:1,nom:'Brad',prenom:'PITT'},
//     {id:3,nom:'Angelina',prenom:'Jolie'},
//     ];
```

**Excercice 3**   
Créer le tableau  **majeurs** à partir de personnes  
utiliser <code>.fitler</code>
```js
const personnes =[
    {id:1,nom:'Brad',prenom:'PITT',age:18},
    {id:2,nom:'TOM',prenom:'CRUISE',age:15},
    {id:3,nom:'Angelina',prenom:'Jolie',age:16},
    {id:4,nom:'TOM',prenom:'CRUISE',age:61}
];
   
// const majeurs =[
//     {id:1,nom:'Brad',prenom:'PITT',age:18},
//     {id:4,nom:'TOM',prenom:'CRUISE',age:61}
//     ];
```


**Excercice 4**  
1 - Calucler le Total avec <code>.map</code>  
2 - calculer le Toatl avec <code>.reduce</code>
```js
const items = [
  { name: 'Apple', price: 1 },
  { name: 'Orange', price: 2 },
  { name: 'Mango', price: 3 },
];

let totalPrice = 0;

```

**Excercice 5**  
Créer 2 tableaux : fruit & légume avec <code>.reduce</code>

```js
const items = [
  { name: "Pomme", type: "fruit" },
  { name: "Carotte", type: "légume" },
  { name: "Banane", type: "fruit" },
  { name: "Brocoli", type: "légume" }
];

```

**Exercice 6**  
 Trouve les équipes de Bob

```js 
const teams=
[
{
    name:'team A',
users : [
  {id:1, name: "Alice", active: true },
  {id:2, name: "Bob", active: false },
  { id:3,name: "Charlie", active: true }
]},
   { name:'team B',
users : [
  { id:1,name: "Alice", active: true },
  { id:2,name: "Bob", active: false },
 
]},
]
const userId = 2;
// equipes =["team A", "team B"]

```