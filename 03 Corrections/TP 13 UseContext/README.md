
CartContext.jsx
```js
import { createContext, useState } from "react";

export const CartContext = createContext();

export function CartProvider({ children }) {
  const [cart, setCart] = useState([]);

  function addToCart(product) {
    setCart([...cart, product]);
  }

  const total = cart.reduce(
    (sum, item) => sum + item.price,
    0
  );

  return (
    <CartContext.Provider value={{
      cart,
      addToCart,
      total
    }}>
      {children}
    </CartContext.Provider>
  );
}
```


Cart.jsx
```js
import { useContext } from "react";
import { CartContext } from "./CartContext";

export default function Cart() {
  const { cart, total } = useContext(CartContext);

  return (
    <div>
      <h2>Panier</h2>

      <p>Articles : {cart.length}</p>

      <p>Total : {total} €</p>
    </div>
  );
}
```

Product.jsx
```jsx
import { useCart } from "../context/CartContext";

const products = [
  { id: 1, name: "Laptop", price: 1200 },
  { id: 2, name: "Phone", price: 700 },
  { id: 3, name: "Headphones", price: 150 },
];

function ProductList() {
  const { addToCart } = useCart();

  return (
    <div>
      <h2>Produits</h2>

      {products.map((product) => (
        <div key={product.id}>
          <h3>{product.name}</h3>
          <p>{product.price} €</p>

          <button onClick={() => addToCart(product)}>
            Ajouter au panier
          </button>

          <hr />
        </div>
      ))}
    </div>
  );
}
```
export default ProductList;

App.jsx
```js
import { CartProvider } from "./CartContext";
import Products from "./Products";
import Cart from "./Cart";

export default function App() {
  return (
    <CartProvider>
      <Products />
      <Cart />
    </CartProvider>
  );
}
```
