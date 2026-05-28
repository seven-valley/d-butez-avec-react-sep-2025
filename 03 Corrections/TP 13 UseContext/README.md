
cartContext.jsx
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
