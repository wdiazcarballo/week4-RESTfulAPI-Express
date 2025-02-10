# **📌 กิจกรรมที่ 5: การสร้าง Web App เชื่อมต่อ REST API ด้วย React & Advanced JS**
**🔹 วัตถุประสงค์ของกิจกรรม:**  
- ทบทวนแนวคิด **React Components, Props, State, Fetch API**  
- ฝึกใช้ **JavaScript ขั้นสูง** เช่น **Async/Await, Higher-Order Functions, ES6 Modules**  
- สร้าง **Web App** ที่เชื่อมต่อ API **Express.js + MongoDB**  
- ใช้ **React Hooks** (`useEffect`, `useState`) และ **Context API**  
- ทำความเข้าใจ **Error Handling** และ **Debugging Tools**

---

### **📍 ขั้นตอนที่ 1: การทบทวน React (State & Props)**
ให้สร้างโครงสร้างพื้นฐานของแอป **React** ที่จะแสดงรายการข้อมูลที่ดึงมาจาก API  

📌 **สร้างไฟล์ `ProductList.jsx`** เพื่อแสดงสินค้าทั้งหมด
```jsx
import { useState, useEffect } from "react";

function ProductList({ apiUrl }) {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetch(apiUrl + "/products")
      .then((res) => res.json())
      .then((data) => setProducts(data))
      .catch((error) => console.error("Error fetching data:", error));
  }, [apiUrl]);

  return (
    <div>
      <h2>รายการสินค้า</h2>
      <ul>
        {products.map((p) => (
          <li key={p._id}>
            {p.name} - ราคา: {p.price} บาท
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ProductList;
```
📌 **ใน `App.jsx` ให้เรียกใช้ Component**
```jsx
import ProductList from "./ProductList";

function App() {
  return (
    <div>
      <h1>ร้านค้าสินค้าออนไลน์</h1>
      <ProductList apiUrl="http://localhost:5000" />
    </div>
  );
}

export default App;
```

---

### **📍 ขั้นตอนที่ 2: การเพิ่มข้อมูล (React Form + API Call)**
ให้นักศึกษา **สร้างฟอร์มเพิ่มข้อมูลสินค้า** โดยใช้ `useState` และ `fetch()`

📌 **สร้างไฟล์ `AddProduct.jsx`**
```jsx
import { useState } from "react";

function AddProduct({ apiUrl, onProductAdded }) {
  const [name, setName] = useState("");
  const [price, setPrice] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    const newProduct = { name, price: parseFloat(price) };

    const response = await fetch(apiUrl + "/products", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(newProduct),
    });

    if (response.ok) {
      setName("");
      setPrice("");
      onProductAdded(); // รีเฟรชรายการสินค้า
    } else {
      console.error("Error adding product");
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <h2>เพิ่มสินค้าใหม่</h2>
      <input type="text" placeholder="ชื่อสินค้า" value={name} onChange={(e) => setName(e.target.value)} required />
      <input type="number" placeholder="ราคา" value={price} onChange={(e) => setPrice(e.target.value)} required />
      <button type="submit">เพิ่มสินค้า</button>
    </form>
  );
}

export default AddProduct;
```

📌 **แก้ไข `App.jsx` เพื่อรวมฟอร์มและรีเฟรชรายการสินค้า**
```jsx
import { useState } from "react";
import ProductList from "./ProductList";
import AddProduct from "./AddProduct";

function App() {
  const [refresh, setRefresh] = useState(false);
  const apiUrl = "http://localhost:5000";

  return (
    <div>
      <h1>ร้านค้าสินค้าออนไลน์</h1>
      <AddProduct apiUrl={apiUrl} onProductAdded={() => setRefresh(!refresh)} />
      <ProductList apiUrl={apiUrl} key={refresh} />
    </div>
  );
}

export default App;
```

---

### **📍 ขั้นตอนที่ 3: ใช้ JavaScript ขั้นสูง (Async/Await & Higher-Order Functions)**
ให้ทบทวน **Async/Await** และเพิ่ม **Higher-Order Functions (`map`, `filter`)** เพื่อจัดการข้อมูลสินค้า

📌 **แก้ไข `ProductList.jsx` ให้สามารถค้นหาสินค้า**
```jsx
import { useState, useEffect } from "react";

function ProductList({ apiUrl }) {
  const [products, setProducts] = useState([]);
  const [search, setSearch] = useState("");

  useEffect(() => {
    async function fetchProducts() {
      try {
        const response = await fetch(apiUrl + "/products");
        const data = await response.json();
        setProducts(data);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    }
    fetchProducts();
  }, [apiUrl]);

  const filteredProducts = products.filter((p) =>
    p.name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div>
      <h2>รายการสินค้า</h2>
      <input type="text" placeholder="ค้นหาสินค้า" value={search} onChange={(e) => setSearch(e.target.value)} />
      <ul>
        {filteredProducts.map((p) => (
          <li key={p._id}>
            {p.name} - ราคา: {p.price} บาท
          </li>
        ))}
      </ul>
    </div>
  );
}

export default ProductList;
```

---

### **📍 ขั้นตอนที่ 4: การใช้ Context API เพื่อจัดการ State**
ในโครงการจริง **Context API** จะช่วยให้จัดการข้อมูลได้ง่ายขึ้นโดยไม่ต้องส่ง props หลายระดับ

📌 **สร้าง Context (`ProductContext.jsx`)**
```jsx
import { createContext, useState } from "react";

export const ProductContext = createContext();

export function ProductProvider({ children }) {
  const [products, setProducts] = useState([]);

  return (
    <ProductContext.Provider value={{ products, setProducts }}>
      {children}
    </ProductContext.Provider>
  );
}
```

📌 **แก้ไข `App.jsx` เพื่อใช้ Context**
```jsx
import { ProductProvider } from "./ProductContext";
import ProductList from "./ProductList";
import AddProduct from "./AddProduct";

function App() {
  return (
    <ProductProvider>
      <div>
        <h1>ร้านค้าสินค้าออนไลน์</h1>
        <AddProduct />
        <ProductList />
      </div>
    </ProductProvider>
  );
}

export default App;
```

---

### **🚀 งานช่วงเบรกสำหรับนักศึกษา**
✅ **Challenge 1:** เพิ่มฟีเจอร์ **แก้ไขสินค้า (PUT)**  
✅ **Challenge 2:** เพิ่มฟีเจอร์ **ลบสินค้า (DELETE)**  
✅ **Challenge 3:** ใช้ **Local Storage** เพื่อเก็บสินค้าชั่วคราว  

---
