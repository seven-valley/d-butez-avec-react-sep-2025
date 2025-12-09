# correction TP Liste de course
```js
// itemStore.js
import { create} from 'zustand'

export const useListItem = create((set,get)=>({
    items:[],
    ajouter :(item)=>{
        set({items:[...get().items,item]})
    },
    enlever: (id)=>{
         set({ items: get().items.filter((item) => item.id !== id) })
    },
    changer: (id)=>{
        console.log(id);
        const updated = get().items.map(item =>
    item.id === id
      ? { ...item, status: !item.status }
      : item);
       set({items:updated})
    }
  
  
    
}))
```

```js
// App.jsx
import { useListItem } from "./stores/ItemStore";

export default function App() {
  const { items, ajouter, enlever, changer } = useListItem();
  const afficher = (formData) => {
    const article = formData.get("article");
    const item = { id: Date.now(), name: article, status: true };
    console.log(article);
    ajouter(item);
  };
  return (
    <>
      <div className="container">
        <div className="col-3">
          <form action={afficher}>
            <input
              className={`form-control my-3`}
              name="article"
              placeholder="article"
            />
            <button className="btn btn-primary" type="submit">
              Valider
            </button>
          </form>

          <table className="table">
            <thead>
              <tr>
                <th>Items</th>
              </tr>
            </thead>
            <tbody>
              {items.map((item) => (
                <tr
                  key={item.id}
                  className={`${
                    item.status ? "table-success" : "table-danger"
                  }`}
                >
                  <td>{item.name}</td>
                  <td>
                    <button
                      onClick={() => enlever(item.id)}
                      className="btn btn-danger"
                    >
                      <i className="fa fa-trash"></i>
                    </button>
                  </td>
                  <td>
                    <button
                      onClick={() => changer(item.id)}
                      className="btn btn-warning"
                    >
                      <i className="fa fa-check"></i>
                    </button>
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>
    </>
  );
}

```