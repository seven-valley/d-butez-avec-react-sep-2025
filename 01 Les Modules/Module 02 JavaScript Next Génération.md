# Module 02 - JavaScript Next génération

## La portée du let est limité
```js
 let age = 18;
 if(age> 18){
     let info =2;
 }
 console.log(info); // undefined
```
## prise en main du const
le const c'est aussi un **tableau** ou un **objet**
```js
 const p1 ={nom:'PITT',prenom:'Brad'};
 const p2 = p1;
 p2.nom= 'CRUISE';
 console.log(p1);
```
## pour copier ou clonner un objet
:warning: Ceci ne marche pas !
```js
 const p1 ={nom:'PITT',prenom:'Brad'};
 const p2 = p1;
 p2.nom= 'CRUISE';
 console.log(p1); 
```
## Spread ... pour cloner une objet
```js
 const p1 ={nom:'PITT',prenom:'Brad',age:18};
 const p2 ={...p1,age:18};
 p2.nom= 'CRUISE';
 console.log(p1);
 ```
## Rest ... exemple
```js
 const ajouter=(...args)=>{
     const tab =[];
     for (let e of args){
         tab.push(e);
     }
     console.log(tab);
 }
 ajouter('pomme');
 ajouter('pomme','poire','cersie');
 ```
## les ${} Template literals ou en francais Littéraux de gabarits
Adieu la concaténation ... Bonjour **${}**
```js
console.log(p1.prenom + ' '+p1.nom);

console.log(`${p1.prenom} ${p1.nom} ${p1.age >17 && 'good'}`);
```
## Bonjour et vive le ternaire
```js
// if classique
if (p1.age > 17 ){
    console.log('GOOD')
}
p.age>17 && console.log('GOOD');
// SI  ALORS SINON
p1.age>17 ? console.log('GOOD') :console.log(' pas GOOD');
//if avec 2 conditions
p1.age>17 & p1.age < 19 ? console.log('GOOD') :console.log(' pas GOOD');
```

## Et enfin Littéraux de gabarits + ternaire
```js
console.log(`info ${p1.age >18 ? 'ok':'no good'}`);
```
------------------------------------------------------------------
------------------------------------------------------------------
------------------------------------------------------------------

# les fonctions sur les tableaux
- :one: <code>.find</code>
- :two: <code>.filter</code>
- :three: <code>.reduce</code>
- :four: <code>.some</code>
- :five: <code>.findIndex()</code>

## :one: <code>.find()</code>

- **But** : retourne **le premier élément** qui satisfait une condition.
-  **Retourne** : **un seul élément** (ou undefined si aucun n’est trouvé).
- **Arrête** la boucle dès qu’un élément est trouvé.

```js
const users = [
  { id: 1, name: 'Alice', active: true },
  { id: 2, name: 'Bob', active: false },
  { id: 3, name: 'Charlie', active: true },
]

const activeUser = users.find(user => user.active)
console.log(activeUser)
// { id: 1, name: 'Alice', active: true }
```

## :two: <code>.filter()</code>

- **But** : retourne **tous les éléments** qui satisfont une condition.
- **Retourne** : **un tableau** (vide si aucun élément ne correspond).
- **Parcourt tout le tableau** pour vérifier chaque élément.

```js
const activeUsers = users.filter(user => user.active)
console.log(activeUsers)
/*
[
  { id: 1, name: 'Alice', active: true },
  { id: 3, name: 'Charlie', active: true }
]
*/
```

## :three: <code>.some()</code>

- **But** : vérifie **si au moins un élément** satisfait une condition.
- **Retourne** : <code>true</code> ou <code>false</code>.
- **Parcours** : s’arrête dès qu’il trouve un élément correspondant.
```js
const id = 2 
const hasuser = users.some(u => u.id === 2)
console.log(hasEven) // true
```

## :four: <code>.reduce()</code>


- **But** : transforme un **tableau entier** en **une seule valeur** (accumulateur).
- **Retourne** : **la valeur finale** de l’accumulateur après avoir parcouru tous les éléments.
- **Parcours** : passe par tous les éléments du tableau.



**Compter le nombre d’utilisateurs actifs**
```js

const activeCount = users.reduce((count, user) => {
  return user.active ? count + 1 : count
}, 0)
console.log(activeCount) // 2
```

**Récupérer uniquement les utilisateurs actifs dans un nouveau tableau**
```js
const activeUsers = users.reduce((arr, user) => {
  if (user.active) arr.push(user)
  return arr
}, [])

console.log(activeUsers)
/*
[
  { id: 1, name: 'Alice', active: true },
  { id: 3, name: 'Charlie', active: true }
]
*/
```

**Créer 2 tableaux par catégorie**

```js
const grouped = users.reduce((acc, item) => {
  if (!acc[item.active]) {
    acc[item.active] = [];
  }
  acc[item.active].push(item);
  return acc;
}, {});
console.log(grouped)
/*
{
    "true": [
        {
            "id": 1,
            "name": "Alice",
            "active": true
        },
        {
            "id": 3,
            "name": "Charlie",
            "active": true
        }
    ],
    "false": [
        {
            "id": 2,
            "name": "Bob",
            "active": false
        }
    ]
}
*/
```
| Méthode     | Retourne                 | Parcours du tableau      | Usage typique                               |
| ----------- | ------------------------ | ------------------------ | ------------------------------------------- |
| `.find()`   | 1 élément (ou undefined) | Arrête dès qu’il trouve  | Chercher un élément précis                  |
| `.filter()` | Tableau (0..n éléments)  | Parcourt tout le tableau | Filtrer plusieurs éléments selon un critère |
| `.some()`   | true / false             | Arrête dès qu’il trouve  | Vérifier si **au moins un élément** correspond à une condition |
| `.reduce()` | Une seule valeur (accumulateur) | Transformer **tout le tableau** en une valeur unique (somme, objet, tableau filtré, etc.) |
| Méthode     | Retourne                        | Usage typique                                                                             |
| `.reduce()` | Une seule valeur (accumulateur) | Parcourt tout le tableau| Transformer **tout le tableau** en une valeur unique (somme, objet, tableau filtré, etc.) |


## :five: <code>.findIndex()</code>

**But** : retourne **l’index du premier élément** qui satisfait une condition.
```js
const index = users.findIndex(user => user.id === 2)
console.log(index) // 1
```