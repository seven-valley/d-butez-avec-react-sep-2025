
# Mise en place d'une classe Business Object

La documentation officielle
https://www.typescriptlang.org/fr/docs/handbook/2/classes.html

## Création Basique
```ts
class Personne {
  public nom: string;
  public age: number;

  constructor(nom: string, age: number) {
    this.nom = nom;
    this.age = age;
  }

  sePresenter(): void {
    console.log(`Bonjour, je m'appelle ${this.nom} et j'ai ${this.age} ans.`);
  }
}
```
## Création avec l'implémentation unique avec une signature de surcharge

TypeScript permet d'écrire plus concis avec des modificateurs dans le constructeur :
```ts
class Voiture {
  constructor(public marque: string, public annee: number) {}
}
```
# <code>?</code> (point d’interrogation) – Propriété optionnelle
Le symbole ? indique que la **propriété est optionnelle** : elle **peut exister ou non**.
En TypeScript, on **ne** peut **pas** créer plusieurs constructeurs comme en Java (pas d’overloading classique).  
Mais on peut simuler plusieurs constructeurs en combinant :
- une signature de surcharge (overload)
- un unique constructeur réel avec de la logique conditionnelle

:white_check_mark: Exemple : Classe Personne avec plusieurs "constructeurs"
On veut pouvoir instancier une Personne :
- Soit avec un nom seulement
- Soit avec un nom et un âge

:mortar_board: Code TypeScript :
```ts

class Personne {
  nom: string;
  age?: number;

  // Signatures surchargées "overloading"  
  // /!\ PAS POSSIBLE en Type Script /!\ 
  //constructor(nom: string);
  //constructor(nom: string, age: number);

// Alors voici comment on fait :)
  // Implémentation unique
  constructor(nom: string, age?: number) {
    this.nom = nom;
    if (age !== undefined) {
      this.age = age;
    }
  }

  sePresenter(): void {
    if (this.age !== undefined) {
      console.log(`Je m'appelle ${this.nom} et j'ai ${this.age} ans.`);
    } else {
      console.log(`Je m'appelle ${this.nom}.`);
    }
  }
}
```

:heart_eyes_cat: Utilisation :
```ts
const p1 = new Personne("Alice");
const p2 = new Personne("Bob", 30);

p1.sePresenter(); // Je m'appelle Alice.
p2.sePresenter(); // Je m'appelle Bob et j'ai 30 ans.
```
⚠️ **À retenir :**
- TypeScript permet de déclarer plusieurs signatures, mais il faut une seule implémentation dans le corps de la classe.
- Vous devez gérer manuellement la logique des cas (vérification de undefined, types, etc.)


-------

En TypeScript, les symboles <code>?</code> et <code>!</code> dans un constructeur ou dans une déclaration de propriété ont des **significations très différentes**, bien qu’ils soient souvent confondus.



## <code>!</code> (non-null assertion) – Suppression du contrôle d'initialisation
Le symbole ! indique à TypeScript que tu garantis toi-même que la propriété sera initialisée, même si le compilateur ne le voit pas.

```ts

class Product {
  name!: string; // TypeScript n'affichera pas d'erreur même si non initialisé ici
}
```
✅ Utilisation typique :
Pour éviter l'erreur Property 'name' has no initializer and is not definitely assigned.

⚠️ Attention :
Vous prenez la responsabilité d'initialiser cette propriété plus tard. Sinon, tu risques une erreur à l'exécution (undefined).



| Symbole | Signification                  | Valeur possible              | Initialisation requise ? |
| ------- | ------------------------------ | ---------------------------- | ------------------------ |
| `?`     | Propriété **optionnelle**      | Type ou `undefined`          | ❌ Non                    |
| `!`     | **Suppression** du contrôle TS | Tu affirmes qu'elle existera | ✅ Oui (à toi de gérer)   |


------------------
------------------


# Type script 
## définir plusieurs type
```ts
let mot : string | null;
mot ='hello' ;
mot = null;
```
## Nullish coalescing
En TypeScript (comme en JavaScript moderne), l’opérateur nullish coalescing <code>??</code> sert à fournir une valeur par défaut uniquement si la valeur de gauche est <code>null</code> ou <code>undefined</code>.
```ts
let resultat = valeur ?? valeurParDefaut;
```

```ts
let nom: string | null = null;
let userName = nom ?? "Anonyme";
console.log(userName); // "Anonyme"

```
### Différence avec ||
```ts
let age = 0;

let avecOr = age || 18;   // → 18 (car 0 est falsy)
let avecNullish = age ?? 18; // → 0 (car 0 n’est pas null/undefined)

console.log(avecOr);      // 18
console.log(avecNullish); // 0
```
👉 <code>||</code> considère toute valeur falsy (0, false, "", NaN) comme “vide”.
👉 <code>??</code> ne réagit qu’à null et undefined.

## typer les tableaux
```ts
let fruit:string[];
fruit = ['pomme','poire','cerise'];
```

Il est possible d'assigner plusieur type
```ts
let info:(string|number)[];
info = [-1,'poire','cerise'];

let info2:any[];
info2 = ['pomme',-2,'cerise'];
```

```ts
let info:Array<string|number>;
info = -1,'poire','cerise';
```

## Les litterals

Il est possible de prédéfinir les valeurs
```ts
let userRole :'admin'|'user'|'guest' ='admin' 
```
Si l'on doit utiliser plusieurs fois le Role
```ts
type Role = 'admin'|'user'|'guest'
let userRole :Role = 'admin'
```


## Les tuples
Il est possible de définir le contenu du tableau avec les tuples
```ts
let val [number,number];
val =[-1,1];
```



Les tuples + litterals
```ts
let val2 [-1|1,-1|1];
val =[-1,1];

```

## Enum
Les énumérations avec Type Script
```ts 
enum Role ={
  Admin,
  Editor,
  Guest
}
let userRole :Role = 0 // admin
userRole= Role.Editor // 1
```