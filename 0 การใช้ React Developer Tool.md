## **📌 การใช้ React Developer Tools บน Chrome เพื่อดู DOM และการทำงานของ React**
---

### **🔹 1. React Developer Tools คืออะไร?**
📌 **React Developer Tools (React DevTools)** เป็น Chrome Extension ที่ช่วยให้เรา:
- **🔍 ตรวจสอบ DOM** และดูว่าแต่ละ Component ของ React ถูก Render อย่างไร
- **📌 ดูค่า State และ Props** ของแต่ละ Component แบบ Real-time
- **⚡ ตรวจสอบ Performance** ของ Component และดูว่ามีการ Re-Render โดยไม่จำเป็นหรือไม่
- **🔄 Debugging Component Tree** เพื่อหาข้อผิดพลาดในการใช้งาน React

---

### **📍 ขั้นตอนที่ 1: ติดตั้ง React Developer Tools**
1. เปิด **Google Chrome** แล้วไปที่ [React Developer Tools บน Chrome Web Store](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
2. คลิก **"Add to Chrome"** แล้วกด **"Add Extension"**
3. เปิด **DevTools** โดยกด `F12` หรือ `Ctrl + Shift + I` (`Cmd + Option + I` บน Mac)
4. คุณจะเห็น **แท็บ React** เพิ่มเข้ามาใน DevTools

---

### **📍 ขั้นตอนที่ 2: ทดสอบ React Developer Tools**
📌 **เปิดแอป React แล้วเข้าไปดูโครงสร้าง Component**
1. **รันแอป React**:
```bash
npm run dev
```
2. เปิด Chrome ไปที่ `http://localhost:5173` (หรือพอร์ตที่รันแอป)
3. เปิด DevTools (`F12` หรือ `Ctrl + Shift + I`)
4. คลิกที่ **แท็บ React** (ถ้าไม่เห็น ให้กด `>>` เพื่อแสดงแท็บเพิ่มเติม)
5. คุณจะเห็น **Component Tree** ของ React ทั้งหมดที่กำลังทำงาน

✅ **สามารถดู Component Structure ได้แบบ Real-time!**

---

### **📍 ขั้นตอนที่ 3: ดู State และ Props ของ Component**
📌 **ลองสร้าง Component `Counter.jsx` ที่มี State**
```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Count: {count}</h2>
      <button onClick={() => setCount(count + 1)}>➕ เพิ่ม</button>
      <button onClick={() => setCount(count - 1)}>➖ ลด</button>
    </div>
  );
}

export default Counter;
```

📌 **เพิ่ม `Counter` ใน `App.jsx`**
```jsx
import Counter from "./Counter";

function App() {
  return (
    <div>
      <h1>React Debugging</h1>
      <Counter />
    </div>
  );
}

export default App;
```

📌 **เปิด React DevTools แล้วดูที่แท็บ Components**
1. คลิกที่ `Counter` Component
2. ดูค่า `State` ของ `count` ที่เปลี่ยนแปลงเมื่อกดปุ่ม
3. ลองเปลี่ยนค่า `count` โดยแก้ไขจาก DevTools แล้วกด Enter → React จะอัปเดต UI ทันที!

✅ **นักศึกษาสามารถ Debug ค่า State ได้ทันทีโดยไม่ต้องแก้โค้ด!**

---

### **📍 ขั้นตอนที่ 4: ตรวจสอบ Performance และ Re-Render**
📌 **เพิ่ม Component `ProductList.jsx`**
```jsx
import { useState, useEffect } from "react";

function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts?_limit=5")
      .then((res) => res.json())
      .then((data) => setProducts(data));
  }, []);

  return (
    <div>
      <h2>Product List</h2>
      {products.map((p) => (
        <p key={p.id}>{p.title}</p>
      ))}
    </div>
  );
}

export default ProductList;
```

📌 **เพิ่ม `ProductList` ใน `App.jsx`**
```jsx
import ProductList from "./ProductList";

function App() {
  return (
    <div>
      <h1>React Debugging</h1>
      <ProductList />
    </div>
  );
}

export default App;
```

📌 **ดูว่า Component ไหน Re-Render บ่อยเกินไป**
1. เปิด **React DevTools**
2. ไปที่แท็บ **Profiler**
3. คลิก **Start Recording**
4. คลิกที่ปุ่มในแอป แล้วหยุด Recording
5. จะเห็นว่า Component ไหนถูก Render บ่อยเกินไปและใช้เวลานาน

✅ **ช่วยปรับปรุง Performance ของ React App ได้ง่ายขึ้น!**

---

### **📍 ขั้นตอนที่ 5: ทดสอบ React Strict Mode**
📌 **แก้ไข `main.jsx`**
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
📌 **StrictMode จะแสดง Warning ถ้าโค้ดมีปัญหา**
- Component Re-Render ซ้ำโดยไม่จำเป็น
- การใช้ State ที่ผิดพลาด
- การใช้ API ที่เลิกใช้งานแล้ว

✅ **React DevTools ช่วยให้เห็นปัญหาเหล่านี้ได้ง่าย!**

---

## **📌 สรุป**
✅ **ติดตั้ง React Developer Tools บน Chrome**  
✅ **ใช้ DevTools ดู Component Tree และค่า State/Props**  
✅ **Debug State และอัปเดตค่าแบบ Real-time**  
✅ **ใช้ Profiler วิเคราะห์ Performance ของ Component**  
✅ **ใช้ StrictMode เพื่อตรวจหาปัญหาโค้ด React**  

---
