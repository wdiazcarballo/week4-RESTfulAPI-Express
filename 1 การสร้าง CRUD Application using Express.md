---

### **💻 การฝึกปฏิบัติ**
#### **1. สร้างและตั้งค่าโปรเจค Express**
```bash
mkdir express-api
cd express-api
npm init -y
npm install express cors body-parser dotenv mongoose
```

#### **2. สร้างไฟล์ `index.js` สำหรับเซิร์ฟเวอร์**
```javascript
const express = require('express');
const cors = require('cors');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 5000;

app.use(cors());
app.use(bodyParser.json());

app.get('/', (req, res) => {
    res.send('Welcome to REST API!');
});

app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

#### **3. ออกแบบโครงสร้างข้อมูล (`models/Product.js`)**
```javascript
const mongoose = require('mongoose');

const ProductSchema = new mongoose.Schema({
    name: String,
    price: Number
});

module.exports = mongoose.model('Product', ProductSchema);
```

#### **4. สร้าง API Routes (`routes/productRoutes.js`)**
```javascript
const express = require('express');
const Product = require('../models/Product');
const router = express.Router();

router.get('/products', async (req, res) => {
    const products = await Product.find();
    res.json(products);
});

router.post('/products', async (req, res) => {
    const newProduct = new Product(req.body);
    await newProduct.save();
    res.status(201).json(newProduct);
});

module.exports = router;
```

#### **5. เชื่อม API กับ React**
📌 ปรับ `App.jsx` ในโปรเจค React เพื่อดึงข้อมูลจาก API:
```jsx
import { useState, useEffect } from "react";

function App() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetch("http://localhost:5000/products")
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

---

### **🚀 การบ้านสำหรับนักศึกษา**
1. ขยาย API ให้รองรับ **Update (PUT)** และ **Delete (DELETE)**  
2. สร้าง **Form ใน React** เพื่อเพิ่มสินค้าใหม่ไปยังฐานข้อมูล  
3. ทดสอบ API โดยใช้ **Postman** หรือ **Thunder Client**  
4. **Deploy API** ไปยัง Render หรือ Vercel  
