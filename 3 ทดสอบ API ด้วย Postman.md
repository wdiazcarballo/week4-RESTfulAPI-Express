# **📌3 การทดสอบ RESTful API โดยใช้ Postman**
**🔹 วัตถุประสงค์ของบทเรียน:**  
1. เข้าใจแนวคิดของ **RESTful API** และ **HTTP Methods (GET, POST, PUT, DELETE)**
2. ใช้ **Postman** ในการ **ทดสอบ API** และดูโครงสร้างของ Request/Response
3. วิเคราะห์ **JSON Response** และ **Status Codes**
4. ฝึกใช้ **Headers และ Body** ในการส่งข้อมูล API
5. เชื่อมโยง API กับ **React (fetch, axios)**

---

## **📍 ขั้นตอนที่ 1: RESTful API คืออะไร?**
**📌 คำอธิบายพื้นฐาน**  
- **REST (Representational State Transfer)** เป็นรูปแบบการออกแบบ API ที่ใช้ HTTP Protocol
- **API (Application Programming Interface)** เป็นช่องทางให้แอปพลิเคชันสามารถสื่อสารกันได้

**📌 หลักการสำคัญของ RESTful API**
- **Stateless** → ไม่มีการเก็บสถานะของ Request เดิม
- **Resource-Based** → ใช้ URL เพื่อเข้าถึงข้อมูล (เช่น `/products`, `/users`)
- **Uses HTTP Methods**
  - `GET` → ดึงข้อมูล
  - `POST` → เพิ่มข้อมูล
  - `PUT` → แก้ไขข้อมูล
  - `DELETE` → ลบข้อมูล

**📌 ตัวอย่าง Endpoint API**
| **Method** | **Endpoint** | **คำอธิบาย** |
|------------|-------------|--------------|
| `GET` | `/api/products` | ดึงรายการสินค้าทั้งหมด |
| `GET` | `/api/products/:id` | ดึงข้อมูลสินค้าตาม ID |
| `POST` | `/api/products` | เพิ่มสินค้าใหม่ |
| `PUT` | `/api/products/:id` | อัปเดตข้อมูลสินค้า |
| `DELETE` | `/api/products/:id` | ลบสินค้า |

---

## **📍 ขั้นตอนที่ 2: ติดตั้งและใช้งาน Postman**
### **✅ ดาวน์โหลดและติดตั้ง Postman**
1. เข้าไปที่ [Postman Download](https://www.postman.com/downloads/)
2. ติดตั้งและเปิดโปรแกรม **Postman**

---

## **📍 ขั้นตอนที่ 3: ทดลองทดสอบ API ด้วย Postman**
### **1️⃣ ทดสอบ `GET /api/products`**
1. เปิด **Postman** และสร้าง **Request ใหม่**
2. เลือก **Method = GET**
3. ใส่ URL ของ API:
   ```
   http://localhost:5000/api/products
   ```
4. กดปุ่ม **Send**
5. ตรวจสอบ **JSON Response**:
   ```json
   [
      {
         "_id": "6611a2b3c9aefb0012b4d123",
         "name": "Laptop",
         "price": 25000
      },
      {
         "_id": "6611a2b3c9aefb0012b4d124",
         "name": "Smartphone",
         "price": 12000
      }
   ]
   ```
6. ตรวจสอบ **Status Code**
   - `200 OK` (หาก API ทำงานถูกต้อง)

---

### **2️⃣ ทดสอบ `POST /api/products`**
1. เปิด **Postman** และเลือก **Method = POST**
2. ใส่ URL:
   ```
   http://localhost:5000/api/products
   ```
3. ไปที่ **Body → raw** และเลือก **JSON**
4. ใส่ข้อมูลที่ต้องการเพิ่ม:
   ```json
   {
      "name": "Tablet",
      "price": 18000
   }
   ```
5. กด **Send** และดู **Response**
   ```json
   {
      "_id": "6611a2b3c9aefb0012b4d125",
      "name": "Tablet",
      "price": 18000
   }
   ```
6. ตรวจสอบ **Status Code**
   - `201 Created` (หากเพิ่มสำเร็จ)

---

### **3️⃣ ทดสอบ `PUT /api/products/:id`**
1. เปิด **Postman** และเลือก **Method = PUT**
2. ใส่ URL โดยใช้ `_id` ของสินค้าที่ต้องการแก้ไข:
   ```
   http://localhost:5000/api/products/6611a2b3c9aefb0012b4d125
   ```
3. ไปที่ **Body → raw** และเลือก **JSON**
4. แก้ไขข้อมูล:
   ```json
   {
      "name": "Tablet Pro",
      "price": 20000
   }
   ```
5. กด **Send** และดูผลลัพธ์
   - `200 OK` → อัปเดตสำเร็จ

---

### **4️⃣ ทดสอบ `DELETE /api/products/:id`**
1. เปิด **Postman** และเลือก **Method = DELETE**
2. ใส่ URL ของสินค้าที่ต้องการลบ:
   ```
   http://localhost:5000/api/products/6611a2b3c9aefb0012b4d125
   ```
3. กด **Send**
4. ตรวจสอบ **Status Code**
   - `200 OK` → ลบสำเร็จ
   - `404 Not Found` → ไม่พบสินค้า

---

## **📍 ขั้นตอนที่ 4: ใช้ React ดึงข้อมูลจาก API**
ให้นักศึกษาลอง **ใช้ React ดึงข้อมูลจาก API จริง** โดยใช้ `fetch()` หรือ `axios`

📌 **ตัวอย่าง React (fetch API)**
```jsx
import { useState, useEffect } from "react";

function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetch("http://localhost:5000/api/products")
      .then((res) => res.json())
      .then((data) => setProducts(data));
  }, []);

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

📌 **ตัวอย่าง React (axios)**
```jsx
import { useState, useEffect } from "react";
import axios from "axios";

function ProductList() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    axios.get("http://localhost:5000/api/products").then((response) => {
      setProducts(response.data);
    });
  }, []);

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

---

## **📍 สรุป**
✅ นักศึกษาเข้าใจ **RESTful API** และหลักการใช้งาน  
✅ นักศึกษาสามารถใช้ **Postman** ทดสอบ API จริง  
✅ นักศึกษาสามารถเชื่อม API กับ React โดยใช้ **fetch หรือ axios**  

---
