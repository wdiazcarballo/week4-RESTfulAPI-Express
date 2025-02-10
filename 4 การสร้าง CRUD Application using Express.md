# **📌4 สร้าง REST API ด้วย Express และเชื่อมต่อ React**
### **🛠️ เครื่องมือที่ใช้ และเหตุผลในการใช้งาน**
✅ **Node.js** → ใช้เป็น Runtime Environment เพื่อรัน JavaScript นอกเว็บเบราว์เซอร์  
✅ **Express.js** → Framework ที่ช่วยให้การสร้าง API บน Node.js ง่ายขึ้น  
✅ **MongoDB (Mongoose)** → ฐานข้อมูล NoSQL ที่รองรับการเก็บข้อมูลแบบ JSON  
✅ **CORS** → Middleware ที่ช่วยให้ API รองรับการเรียกข้ามโดเมน (Cross-Origin Requests)  
✅ **dotenv** → ใช้จัดการตัวแปรแวดล้อม (`.env`) เพื่อเก็บ API Keys และ Config  
✅ **React.js** → ใช้สร้าง UI ฝั่ง Client และเรียก API แสดงผลข้อมูล  
✅ **Postman/Thunder Client** → ใช้ทดสอบ API ได้ง่ายขึ้น  
✅ **Render/Vercel** → ใช้ Deploy API และ React App เพื่อให้ใช้งานออนไลน์ได้  

---

## **📍 ขั้นตอนที่ 1: ตั้งค่าโปรเจคและติดตั้งเครื่องมือ**
### ✅ **1.1 สร้าง GitHub Repository**
1. เข้า [GitHub](https://github.com/) → คลิก **New Repository**  
2. ตั้งชื่อ **express-api** → **เช็ค Add a README file**  
3. คลิก **Create Repository**  
4. เปิด **Terminal** และรันคำสั่งต่อไปนี้:
```bash
git clone https://github.com/your-username/express-api.git
cd express-api
```

### ✅ **1.2 ติดตั้ง Express และแพ็กเกจที่จำเป็น**
```bash
npm init -y
npm install express cors body-parser dotenv mongoose
```
📌 **อธิบายแพ็กเกจ**  
- **express** → ใช้สร้าง Web Server และ API  
- **cors** → ป้องกันปัญหาการเรียก API ข้ามโดเมน  
- **body-parser** → ช่วยแปลง JSON ที่ส่งมากับ `POST` request  
- **dotenv** → ใช้กำหนดค่า `.env` สำหรับเก็บตัวแปรแวดล้อม  
- **mongoose** → ช่วยจัดการฐานข้อมูล MongoDB ด้วย JavaScript  

---

## **📍 ขั้นตอนที่ 2: สร้างเซิร์ฟเวอร์ Express**
📌 **สร้างไฟล์ `index.js` และเพิ่มโค้ดต่อไปนี้**
```javascript
const express = require('express');
const cors = require('cors');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(bodyParser.json());

// เชื่อมต่อ MongoDB
mongoose.connect(process.env.MONGO_URI, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
}).then(() => console.log('✅ MongoDB Connected'))
  .catch(err => console.log('❌ MongoDB Error:', err));

// เส้นทางทดสอบ API
app.get('/', (req, res) => {
    res.send('🎉 Welcome to REST API!');
});

// เริ่มต้นเซิร์ฟเวอร์
app.listen(PORT, () => {
    console.log(`🚀 Server running on port ${PORT}`);
});
```

---

## **📍 ขั้นตอนที่ 3: ตั้งค่า MongoDB และสร้าง Model**
📌 **สร้างไฟล์ `.env` เพื่อเก็บ URL ของ MongoDB**
```env
MONGO_URI=your_mongodb_connection_string
PORT=5000
```
📌 **สร้างโฟลเดอร์ `models/` และเพิ่มไฟล์ `Product.js`**
```javascript
const mongoose = require('mongoose');

const ProductSchema = new mongoose.Schema({
    name: { type: String, required: true },
    price: { type: Number, required: true }
});

module.exports = mongoose.model('Product', ProductSchema);
```
📌 **อธิบาย Model**
- `name` และ `price` เป็น **Field** ในฐานข้อมูล  
- `required: true` บังคับว่าต้องมีค่า  

---

## **📍 ขั้นตอนที่ 4: กำหนด API Routes**
📌 **สร้างโฟลเดอร์ `routes/` และเพิ่มไฟล์ `productRoutes.js`**
```javascript
const express = require('express');
const Product = require('../models/Product');
const router = express.Router();

// 📌 ดึงข้อมูลสินค้าทั้งหมด
router.get('/products', async (req, res) => {
    try {
        const products = await Product.find();
        res.status(200).json(products);
    } catch (error) {
        res.status(500).json({ message: error.message });
    }
});

// 📌 เพิ่มสินค้าใหม่
router.post('/products', async (req, res) => {
    try {
        const newProduct = new Product(req.body);
        await newProduct.save();
        res.status(201).json(newProduct);
    } catch (error) {
        res.status(500).json({ message: error.message });
    }
});

module.exports = router;
```
📌 **แก้ไข `index.js` เพื่อให้ใช้ Routes**
```javascript
const productRoutes = require('./routes/productRoutes');
app.use('/api', productRoutes);
```

---

## **📍 ขั้นตอนที่ 5: ทดสอบ API ด้วย Postman**
### ✅ **5.1 ทดสอบ `GET /api/products`**
1. เปิด **Postman** → สร้าง **New Request**
2. เลือก **Method = GET**
3. ใส่ URL:
   ```
   http://localhost:5000/api/products
   ```
4. กด **Send** ✅ ควรเห็นข้อมูล JSON

### ✅ **5.2 ทดสอบ `POST /api/products`**
1. เปลี่ยน **Method เป็น POST**
2. ใส่ URL:
   ```
   http://localhost:5000/api/products
   ```
3. ไปที่ **Body → raw** และเลือก **JSON**
4. ใส่ข้อมูล:
   ```json
   {
      "name": "Laptop",
      "price": 25000
   }
   ```
5. กด **Send** ✅ ควรเห็นข้อมูลสินค้าที่เพิ่มสำเร็จ

---

## **📍 ขั้นตอนที่ 6: เชื่อมต่อ React กับ API**
📌 **แก้ไข `src/App.jsx`**
```jsx
import { useState, useEffect } from "react";

function App() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetch("http://localhost:5000/api/products")
      .then(res => res.json())
      .then(data => setProducts(data));
  }, []);

  return (
    <div>
      <h1>Product List</h1>
      {products.map(p => <p key={p._id}>{p.name} - ${p.price}</p>)}
    </div>
  );
}

export default App;
```
📌 **รัน React App**
```bash
npm run dev
```

---

## **📍 ขั้นตอนที่ 7: อัพโหลดโค้ดไปยัง GitHub**
```bash
git add .
git commit -m "Initial commit - Express API and React Integration"
git push origin main
```

---

## **📍 การบ้านสำหรับนักศึกษา**
✅ **Challenge 1:** เพิ่มฟังก์ชัน `PUT` และ `DELETE`  
✅ **Challenge 2:** เพิ่ม **Form** ใน React เพื่อเพิ่มสินค้าใหม่  
✅ **Challenge 3:** Deploy API ไปยัง **Render หรือ Vercel**  

---

🎯 **สรุป**
✅ ใช้ **Express.js** สร้าง REST API  
✅ เชื่อมต่อ **MongoDB** และเก็บข้อมูลสินค้า  
✅ ใช้ **React** เพื่อดึงข้อมูลจาก API  
✅ ทดสอบ API ด้วย **Postman**  
✅ ซิงค์โค้ดกับ **GitHub**  

