# NPM
```
npm install zustand
````

## Version simple
Le store `itemStore.js`
```js
//itemStore.js
import { create } from 'zustand'

export const useListeItem = create((set, get) => ({
    items:[],
    ajouter: (item)=>{
        set({items:[...get().items,item]})
    }

}))

```
`App.jsx`
```js
import { useForm } from "react-hook-form";
import { useListeItem } from './itemStore'

export default function App() {
  const { items,ajouter } = useListeItem()



  const afficher = (formData) => {
    const item = formData.get('item');
    ajouter(item);
    console.log(items);
  }
  return (
    <>
      <div className="container">
        <div className="col-3">
          <form action={afficher}>
            <input 
            className={`form-control my-3`} 
            name="item"
            placeholder="item" />
            
            
          
            <table className="table">
              <thead>
                
                <tr>
                  <th>Items</th>
                </tr>
                
              </thead>
              <tbody>
                { items.map ( item=>
                <tr>
                  <td>{item}</td>
                </tr>)
                }
              </tbody>
            </table>
            <button className="btn btn-primary" type="submit">
            Valider
          </button>
          </form>
        </div>
      </div>
    </>
  );
}
```

### Javascript
```js
// cartStore.js
import { create } from 'zustand'

export const useCartStore = create((set, get) => ({
  cart: [],
  addToCart: (product) => {
    const cart = get().cart
    const existing = cart.find((item) => item.id === product.id)

    if (existing) {
      set({
        cart: cart.map((item) =>
          item.id === product.id
            ? { ...item, quantity: item.quantity + 1 }
            : item
        ),
      })
    } else {
      set({ cart: [...cart, { ...product, quantity: 1 }] })
    }
  },
  removeFromCart: (id) =>
    set({ cart: get().cart.filter((item) => item.id !== id) }),
  clearCart: () => set({ cart: [] }),
  total: () =>
    get().cart.reduce((sum, item) => sum + item.price * item.quantity, 0),
}))
```

```ts
// CartApp.jsx
import React from 'react'
import { useCartStore } from './cartStore'

const products = [
  { id: 1, name: '🍎 Pomme', price: 1 },
  { id: 2, name: '🍌 Banane', price: 2 },
  { id: 3, name: '🍊 Orange', price: 1.5 },
]

export default function CartApp() {
  const { cart, addToCart, removeFromCart, clearCart, total } = useCartStore()

  return (
    <div style={{ padding: 20, maxWidth: 400, margin: 'auto' }}>
      <h1>🛒 Mon Panier</h1>

      <h2>Produits disponibles :</h2>
      <ul>
        {products.map((p) => (
          <li key={p.id} style={{ marginBottom: 10 }}>
            {p.name} - {p.price} €
            <button
              onClick={() => addToCart(p)}
              style={{ marginLeft: 10 }}
            >
              Ajouter
            </button>
          </li>
        ))}
      </ul>

      <h2>Panier :</h2>
      {cart.length === 0 ? (
        <p>Votre panier est vide.</p>
      ) : (
        <ul>
          {cart.map((item) => (
            <li key={item.id}>
              {item.name} x {item.quantity}
              <button
                onClick={() => removeFromCart(item.id)}
                style={{ marginLeft: 10 }}
              >
                Supprimer
              </button>
            </li>
          ))}
        </ul>
      )}

      <h3>Total : {total().toFixed(2)} €</h3>

      <button onClick={clearCart}>Vider le panier</button>
    </div>
  )
}

```
# Asynchrone
```js
// postStore.js
import { create } from 'zustand'

export const usePostStore = create((set) => ({
  posts: [],
  loading: false,
  error: null,
  fetchPosts: async () => {
    set({ loading: true, error: null })
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/posts?_limit=5')
      const data = await res.json()
      set({ posts: data, loading: false })
    } catch (err) {
      set({ error: 'Erreur lors du chargement', loading: false })
    }
  },
}))
```

```ts
// PostApp.jsx
import React, { useEffect } from 'react'
import { usePostStore } from './postStore'

export default function PostApp() {
  const { posts, loading, error, fetchPosts } = usePostStore()

  useEffect(() => {
    fetchPosts()
  }, [fetchPosts])

  if (loading) return <p>⏳ Chargement...</p>
  if (error) return <p style={{ color: 'red' }}>{error}</p>

  return (
    <div style={{ padding: 20 }}>
      <h1>📰 Derniers articles</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.id} style={{ marginBottom: 10 }}>
            <strong>{post.title}</strong>
            <p>{post.body}</p>
          </li>
        ))}
      </ul>
    </div>
  )
}
```

# Type Script
```ts
// cartStore.ts
import { create } from 'zustand'

interface Product {
  id: number
  name: string
  price: number
}

interface CartItem extends Product {
  quantity: number
}

interface CartState {
  cart: CartItem[]
  addToCart: (product: Product) => void
  removeFromCart: (id: number) => void
  clearCart: () => void
  total: () => number
}

export const useCartStore = create<CartState>((set, get) => ({
  cart: [],
  addToCart: (product) => {
    const cart = get().cart
    const existing = cart.find((item) => item.id === product.id)

    if (existing) {
      set({
        cart: cart.map((item) =>
          item.id === product.id
            ? { ...item, quantity: item.quantity + 1 }
            : item
        ),
      })
    } else {
      set({ cart: [...cart, { ...product, quantity: 1 }] })
    }
  },
  removeFromCart: (id) =>
    set({ cart: get().cart.filter((item) => item.id !== id) }),
  clearCart: () => set({ cart: [] }),
  total: () =>
    get().cart.reduce((sum, item) => sum + item.price * item.quantity, 0),
}))
```

```ts
// CartApp.tsx
import React from 'react'
import { useCartStore } from './cartStore'

const products = [
  { id: 1, name: '🍎 Pomme', price: 1 },
  { id: 2, name: '🍌 Banane', price: 2 },
  { id: 3, name: '🍊 Orange', price: 1.5 },
]

export default function CartApp() {
  const { cart, addToCart, removeFromCart, clearCart, total } = useCartStore()

  return (
    <div className="p-6 max-w-lg mx-auto">
      <h1 className="text-2xl font-bold mb-4">🛒 Mon Panier</h1>

      <div className="mb-6">
        <h2 className="font-semibold mb-2">Produits disponibles :</h2>
        <ul className="space-y-2">
          {products.map((p) => (
            <li key={p.id} className="flex justify-between border p-2 rounded">
              <span>{p.name} - {p.price}€</span>
              <button
                onClick={() => addToCart(p)}
                className="px-3 py-1 bg-blue-500 text-white rounded"
              >
                Ajouter
              </button>
            </li>
          ))}
        </ul>
      </div>

      <div>
        <h2 className="font-semibold mb-2">Panier :</h2>
        {cart.length === 0 ? (
          <p>Votre panier est vide.</p>
        ) : (
          <ul className="space-y-2">
            {cart.map((item) => (
              <li key={item.id} className="flex justify-between border p-2 rounded">
                <span>
                  {item.name} x {item.quantity}
                </span>
                <button
                  onClick={() => removeFromCart(item.id)}
                  className="text-red-500 hover:underline"
                >
                  Supprimer
                </button>
              </li>
            ))}
          </ul>
        )}
      </div>

      <div className="mt-4 font-bold">
        Total: {total().toFixed(2)} €
      </div>

      <button
        onClick={clearCart}
        className="mt-3 px-4 py-2 bg-gray-700 text-white rounded"
      >
        Vider le panier
      </button>
    </div>
  )
}

```
