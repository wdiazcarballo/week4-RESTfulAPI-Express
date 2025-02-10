# สัปดาห์ที่ 4 - การสร้าง REST API ด้วย Node.js และ Express.js
---
**📌 วัตถุประสงค์:**  
ภายในสัปดาห์นี้ นักศึกษาควรสามารถ:  
1. เข้าใจแนวคิดของ **REST API** และหลักการออกแบบ API  
2. พัฒนา REST API **พื้นฐาน** โดยใช้ **Node.js** และ **Express.js**  
3. เชื่อมต่อ API กับฐานข้อมูล **MongoDB**  
4. ทดลองใช้ API ในแอปพลิเคชัน **React** ผ่าน `fetch()` หรือ `Axios`  
5. ใช้ **Middleware** และ **Error Handling** เพื่อพัฒนา API ให้มีประสิทธิภาพ  

---

### **📝 โครงสร้างบทเรียน**
| **เวลา** | **หัวข้อ** | **กิจกรรม** |
|---------|----------|------------|
| 09:30 - 09:50 | แนะนำ REST API และ HTTP Methods | อธิบายแนวคิดเกี่ยวกับ API, Request/Response, JSON, Status Codes |
| 09:50 - 10:20 | การติดตั้งและตั้งค่าโปรเจค Express.js | นักศึกษาสร้างโปรเจค Express API ด้วย `npm init` |
| 10:20 - 10:50 | สร้าง REST API (CRUD Operations) | นักศึกษาพัฒนา API `GET`, `POST`, `PUT`, `DELETE` สำหรับจัดการข้อมูล |
| 10:50 - 11:10 | การเชื่อมต่อฐานข้อมูล MongoDB | นักศึกษาเพิ่ม Mongoose และออกแบบ **Schema** |
| 11:10 - 11:30 | การดึงข้อมูลจาก API ใน React | นักศึกษาฝึกใช้ `fetch()` เพื่อแสดงข้อมูลจาก API |
| 11:30 - 12:00 | **Workshop**: พัฒนา Mini Project | นักศึกษาทดลองสร้าง API ของตนเองและเชื่อมต่อกับ React |

