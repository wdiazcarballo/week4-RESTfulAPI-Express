# **สัปดาห์ที่ 4 - การสร้าง RESTful API และเชื่อมต่อ Web App**

## **📌 วัตถุประสงค์การเรียนรู้ **

ภายในสัปดาห์นี้ นักศึกษาจะสามารถ:

1. **เข้าใจและจัดการ DOM (Document Object Model)** – ศึกษาการเข้าถึงและเปลี่ยนแปลง HTML ผ่าน JavaScript  
2. **เข้าใจการทำงานของ JavaScript Asynchronous Calls** – ใช้ Callback, Promise, และ Async/Await  
3. **ใช้ React Developer Tools** – ตรวจสอบโครงสร้างของ React Component Tree และ Debugging  
4. **สร้าง CRUD Application ด้วย Express.js** – พัฒนา RESTful API สำหรับการจัดการข้อมูล  
5. **เชื่อมต่อ REST API กับ React และใช้ Advanced JavaScript** – ฝึกใช้งาน Fetch API และ Axios  
6. **ทดสอบ API ด้วย Postman** – ฝึกใช้ Postman หรือ Thunder Client เพื่อเรียกใช้งาน API  
7. **สร้าง Web App ที่ใช้ AI API** – ใช้งาน OpenAI API หรือ Hugging Face API  

---

## **📍 ตารางการเรียน (09:30 - 12:30)**
| เวลา               | หัวข้อ                                                   | กิจกรรม                                                              |
|------------------|--------------------------------------------------------|---------------------------------------------------------------------|
| 09:30 - 10:00   | **รู้จัก DOM และการจัดการ**                              | ทดลองใช้ JavaScript จัดการ DOM และสังเกตการเปลี่ยนแปลงผ่าน Console |
| 10:00 - 10:30   | **JS Asynchronous Calls**                               | ทดลองใช้ Callback, Promise, และ Async/Await ผ่านตัวอย่าง API      |
| 10:30 - 10:55   | ☕ **พักเบรก 25 นาที**                                  | นักศึกษาพักและเตรียมตัวสำหรับการเรียนต่อ                         |
| 10:55 - 11:20   | **การใช้ React Developer Tools**                        | ทดสอบ React Components, Props, และ State ผ่าน DevTools             |
| 11:20 - 11:50   | **การสร้าง CRUD Application using Express.js**          | สร้าง REST API ด้วย Express.js และเชื่อมต่อ MongoDB                |
| 11:50 - 12:20   | **การสร้าง Web App เชื่อมต่อ REST API ด้วย React**      | ใช้ Fetch API/Axios ใน React เพื่อดึงข้อมูลจาก API                 |
| 12:20 - 12:30   | **สรุปและ Q&A**                                        | นักศึกษาแชร์ประสบการณ์ ปรับปรุงโค้ด และสอบถามข้อสงสัย             |
---

## **📌 การบ้านสำหรับนักศึกษา**
1. **พัฒนา CRUD API ให้รองรับการอัปเดตและลบข้อมูล** (`PUT` / `DELETE`)  
2. **ใช้ React Form เพื่อเพิ่มข้อมูลลงในฐานข้อมูลผ่าน API**  
3. **ใช้ Postman ทดสอบ API และแก้ไขปัญหาที่พบ**  
4. **เชื่อมต่อ AI API (ChatGPT, Hugging Face) กับ Web App และแสดงผลลัพธ์**

## **🎉🍄‍🟫ของเล่นใหม่ PowerToy **
```python
class Person:
    """A simple class representing a person."""
    
    def __init__(self, name, age):
        """Constructor to initialize name and age attributes."""
        self.name = name
        self.age = age

    def greet(self):
        """Method to greet the person."""
        return f"Hello, my name is {self.name} and I am {self.age} years old."

    def have_birthday(self):
        """Method to increase age by 1 year."""
        self.age += 1
        return f"Happy Birthday {self.name}! You are now {self.age} years old."

# Example Usage
person1 = Person("Alice", 25)

print(person1.greet())  # Output: Hello, my name is Alice and I am 25 years old.
print(person1.have_birthday())  # Output: Happy Birthday Alice! You are now 26 years old.

```

