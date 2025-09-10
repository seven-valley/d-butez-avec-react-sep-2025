# TP 00 Next génération Correction

## Ecercice 1 & 2
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
// excercice 1
const nouveauClients = personnes.filter(p => !clients.find(c => c.id === p.id));
console.log(nouveauClients);

// excercice 2
const dejaClients = personnes.filter(p => clients.find(c => c.id === p.id));
console.log(dejaClients);
```

## Ecercice 3
```js
const personnes =[
    {id:1,nom:'Brad',prenom:'PITT',age:18},
    {id:2,nom:'TOM',prenom:'CRUISE',age:15},
    {id:3,nom:'Angelina',prenom:'Jolie',age:16},
    {id:4,nom:'TOM',prenom:'CRUISE',age:61}
];
const majeur = personnes.filter((personne)=>{
    return personne.age>17
})
console.log(majeur)
```

## Ecercice 4
```js
const items = [
  { name: 'Apple', price: 1 },
  { name: 'Orange', price: 2 },
  { name: 'Mango', price: 3 },
];
const total = items.reduce((total, item) => total + item.price, 0);
console.log(total)

const total2 = items.map((item) => item.price).reduce((a, b) => a + b);
console.log(total);

let total3 =0
items.map((item) => total3 += item.price); 
console.log(total3);
```

## Exercice 5 
Classer des objets en groupes selon une category :
```js
const items = [
  { name: "Pomme", type: "fruit" },
  { name: "Carotte", type: "légume" },
  { name: "Banane", type: "fruit" },
  { name: "Brocoli", type: "légume" }
];

const grouped = items.reduce((acc, item) => {
  if (!acc[item.type]) {
    acc[item.type] = [];
  }
  acc[item.type].push(item.name);
  return acc;
}, {});

console.log(grouped);
// {
//   fruit: ["Pomme", "Banane"],
//   légume: ["Carotte", "Brocoli"]
// }
```

## Exercice 6
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
const equipes = teamsWithUser.reduce((arr, equipe) => {
    if (equipe.users.some(user => user.id === userId))
   arr.push(equipe.name)
  return arr
}, [])
console.log(equipes);

// autres solutions
const teamNamesWithUser = teams
  .filter(team => team.users.some(user => user.id === userId))
  .map(team => team.name)

console.log(teamNamesWithUser)

```