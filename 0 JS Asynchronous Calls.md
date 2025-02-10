### **📌 การจัดการ Asynchronous Calls ใน JavaScript (Async/Await & Promises)**
---

### **🔹 1. การทำงานของ JavaScript เป็นแบบ Single-Threaded และ Asynchronous**
📌 **JavaScript ใช้ Event Loop จัดการคำสั่งแบบ Asynchronous**
- JavaScript **ไม่ได้** รันคำสั่งทีละบรรทัดแบบ Synchronous
- ใช้ **Event Loop** + **Callback Queue** + **Microtask Queue** ในการจัดการคำสั่งที่ใช้เวลา เช่น:
  - การดึงข้อมูลจาก API (`fetch()`)
  - การอ่านไฟล์ (`fs.readFile`)
  - การใช้ `setTimeout()`

🔹 **Synchronous Code (Blocking)**  
```javascript
console.log("Start");
for (let i = 0; i < 5; i++) {
  console.log(i);
}
console.log("End");
```
📌 **Output:**
```
Start
0
1
2
3
4
End
```
✅ **รันทีละคำสั่ง จนครบทั้งหมด ก่อนทำคำสั่งต่อไป**

---

### **🔹 2. ทำไมต้องใช้ Promises และ Async/Await?**
🚀 **ปัญหา Callback Hell เมื่อใช้โค้ดแบบดั้งเดิม**
```javascript
setTimeout(() => {
  console.log("Step 1");
  setTimeout(() => {
    console.log("Step 2");
    setTimeout(() => {
      console.log("Step 3");
    }, 1000);
  }, 1000);
}, 1000);
```
📌 **ปัญหา:** อ่านยากและซ้อนกันหลายระดับ → ใช้ `Promise` แทน

---

### **🔹 3. การใช้ Promises**
🔹 **Promise คือ Object ที่ทำงานแบบ Asynchronous แล้วส่งค่าผ่าน `.then()`**
```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data loaded!");
    }, 2000);
  });
};

fetchData()
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```
📌 **Output หลังจาก 2 วินาที:**
```
Data loaded!
```
✅ **ใช้ `.then()` และ `.catch()` เพื่อจัดการผลลัพธ์**

---

### **🔹 4. เปลี่ยนจาก Promises → Async/Await**
🔹 **Async/Await ทำให้โค้ดอ่านง่ายขึ้น**
```javascript
const fetchData = async () => {
  try {
    const data = await new Promise((resolve) => {
      setTimeout(() => resolve("Data loaded!"), 2000);
    });
    console.log(data);
  } catch (error) {
    console.error(error);
  }
};

fetchData();
```
✅ **ข้อดีของ Async/Await**
1. **อ่านง่ายกว่า `.then()`**
2. **ใช้โค้ดแบบ Synchronous แต่ทำงาน Asynchronous**
3. **สามารถใช้ `try/catch` จัดการ Error ได้ง่าย**

📌 **Output หลังจาก 2 วินาที:**
```
Data loaded!
```

---

### **🔹 5. เปรียบเทียบ Fetch API แบบ `then()` vs `async/await`**
**🔸 แบบ `.then()`**
```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Error:", error));
```

**🔸 แบบ `async/await`**
```javascript
const getPost = async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts/1");
    const data = await res.json();
    console.log(data);
  } catch (error) {
    console.error("Error:", error);
  }
};

getPost();
```
✅ **Async/Await ดูเรียบร้อยกว่าและเข้าใจง่าย**

---

### **🔹 6. การจัดการหลาย Requests ด้วย Promise.all()**
📌 **เรียก API พร้อมกัน ลดเวลาในการโหลด**
```javascript
const fetchUser = fetch("https://jsonplaceholder.typicode.com/users/1").then(res => res.json());
const fetchPost = fetch("https://jsonplaceholder.typicode.com/posts/1").then(res => res.json());

Promise.all([fetchUser, fetchPost])
  .then(([user, post]) => {
    console.log("User:", user);
    console.log("Post:", post);
  })
  .catch((error) => console.error("Error:", error));
```
✅ **ข้อดีของ `Promise.all()`**
- ลดเวลา **เพราะไม่ต้องรอทีละ Request**
- ถ้า Request ไหนพัง ทุกตัวจะพัง (Fail Fast)

---

### **🔹 7. Async/Await + Multiple Requests**
🔹 **ใช้ `await Promise.all()` เพื่อให้รอคำตอบทั้งหมด**
```javascript
const fetchUserAndPost = async () => {
  try {
    const [user, post] = await Promise.all([
      fetch("https://jsonplaceholder.typicode.com/users/1").then(res => res.json()),
      fetch("https://jsonplaceholder.typicode.com/posts/1").then(res => res.json())
    ]);
    console.log("User:", user);
    console.log("Post:", post);
  } catch (error) {
    console.error("Error:", error);
  }
};

fetchUserAndPost();
```
📌 **Async/Await จะรอทั้งคู่ก่อนถึงทำงานต่อ**

---

### **🔹 8. ใช้ Async/Await กับ MongoDB (Mongoose)**
📌 **ใน API Routes เราใช้ `await` เพื่อดึงข้อมูลจากฐานข้อมูล**
```javascript
router.get('/products', async (req, res) => {
    try {
        const products = await Product.find(); // รอการดึงข้อมูลจาก DB
        res.status(200).json(products);
    } catch (error) {
        res.status(500).json({ message: error.message });
    }
});
```
✅ **ลดปัญหา Callback Hell และจัดการ Error ได้ง่าย**

---

### **📌 สรุป**
✅ **`Promise`** ใช้ `.then()` และ `.catch()` จัดการผลลัพธ์  
✅ **`Async/Await`** ทำให้โค้ดอ่านง่ายและเหมือนโค้ด Synchronous  
✅ **`Promise.all()`** ช่วยเรียก API หลายตัวพร้อมกัน  
✅ **ใช้ `await` กับ MongoDB (Mongoose) เพื่อจัดการฐานข้อมูล**  
✅ **`try/catch` ช่วยจัดการ Error ให้มีโครงสร้างที่ชัดเจน**  

🚀 **ตอนนี้นักศึกษาควรเข้าใจ Asynchronous Calls และพร้อมจะใช้งานกับ API ได้แล้ว!** 🚀  
