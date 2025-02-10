# **📌 1 การเรียนรู้ BOM และ DOM พร้อม Form Interaction**
🎯 **วัตถุประสงค์ของบทเรียน**  
✅ เข้าใจ **BOM (Browser Object Model)** และ **DOM (Document Object Model)**  
✅ ใช้ **JavaScript Console** เพื่อสังเกต **DOM Changes**  
✅ เรียนรู้การใช้ **Forms** เพื่อรับข้อมูลจากผู้ใช้  
✅ ใช้ **Template Literals (`${}`)** เพื่อแสดงค่าที่ผู้ใช้ป้อน  

---

## **🔹 1. ใช้ Console เพื่อสังเกตการเปลี่ยนแปลงของ DOM**
📌 **ให้นักศึกษาเปิด DevTools (`F12` → Console) แล้วพิมพ์คำสั่งเหล่านี้**  
```javascript
console.log(document.title); // ดู Title ของหน้าเว็บ
console.log(document.body.innerHTML); // ดู HTML ทั้งหมดใน <body>
console.log(document.querySelector("h1")); // ดู Element <h1>
console.dir(document.querySelector("h1")); // แสดง Properties ของ <h1>
```
✅ **สังเกตผลลัพธ์ใน Console เพื่อดูโครงสร้างของ DOM!**  

---

## **🔹 2. สร้างไฟล์ HTML พร้อม Form**
📌 **สร้างไฟล์ `index.html`**  
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM & BOM Tutorial</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin: 50px; }
        .box { width: 100px; height: 100px; background: blue; margin: 20px auto; }
    </style>
</head>
<body>
    <h1 id="title">Hello DOM</h1>

    <button id="changeText">Change Text</button>
    <button id="changeColor">Change Color</button>
    <button id="showInfo">Show Browser Info</button>
    
    <div class="box"></div>

    <h2>🔹 Form Interaction</h2>
    <form id="userForm">
        <label for="name">ชื่อของคุณ:</label>
        <input type="text" id="name" placeholder="กรอกชื่อของคุณ">
        <button type="submit">Submit</button>
    </form>

    <p id="output"></p>

    <script src="script.js"></script>
</body>
</html>
```
---

## **🔹 3. เขียน JavaScript เพื่อสังเกต DOM Changes**
📌 **สร้างไฟล์ `script.js` และเพิ่มโค้ดต่อไปนี้**
```javascript
// สังเกต DOM Changes ผ่าน Console
console.log("Initial Title:", document.title);
console.log("Initial H1 Text:", document.querySelector("h1").innerText);

// เปลี่ยนข้อความของ <h1> และดูการเปลี่ยนแปลงผ่าน Console
document.getElementById("changeText").addEventListener("click", function() {
    document.getElementById("title").innerText = "Hello JavaScript!";
    console.log("Updated H1 Text:", document.getElementById("title").innerText);
});

// เปลี่ยนสีของ .box แบบสุ่ม และ log ผลลัพธ์
document.getElementById("changeColor").addEventListener("click", function() {
    let colors = ["red", "green", "blue", "purple", "orange"];
    let randomColor = colors[Math.floor(Math.random() * colors.length)];
    document.querySelector(".box").style.backgroundColor = randomColor;
    console.log("Box Color Changed To:", randomColor);
});

// แสดงข้อมูล Browser ผ่าน BOM
document.getElementById("showInfo").addEventListener("click", function() {
    alert(`🌍 Browser: ${navigator.userAgent}\n📏 Screen Size: ${window.innerWidth} x ${window.innerHeight}`);
});
```
✅ **นักศึกษาควรสังเกตค่าที่เปลี่ยนแปลงใน Console ทุกครั้งที่กดปุ่ม!**  

---

## **🔹 4. ใช้ Form + Template Literal แสดงค่าจากผู้ใช้**
📌 **เพิ่มโค้ดใน `script.js` เพื่อดึงค่าจาก Form และแสดงผล**
```javascript
document.getElementById("userForm").addEventListener("submit", function(event) {
    event.preventDefault(); // ป้องกันการรีโหลดหน้าเว็บ
    let name = document.getElementById("name").value;

    // ใช้ Template Literal แสดงผลลัพธ์
    document.getElementById("output").innerHTML = `<strong>👋 สวัสดี, ${name}!</strong>`;
    
    console.log(`User Entered: ${name}`); // Log ไปที่ Console
});
```
✅ **เมื่อนักศึกษากรอกชื่อ และกด Submit ควรเห็นข้อความเปลี่ยนแปลงและค่า log ใน Console!**

---

## **📌 ภารกิจให้นักศึกษา**
✅ **Challenge 1:** สร้างปุ่ม **"ซ่อน/แสดง ข้อความ"** ที่สามารถเปิด/ปิด `#output` ได้  
✅ **Challenge 2:** เพิ่ม **ปุ่มรีเซ็ต Form** และล้างค่า `#output`  
✅ **Challenge 3:** ใช้ `setInterval()` ทำให้ `.box` เปลี่ยนสีอัตโนมัติทุก 2 วินาที  

---

## **📌 สรุป**
✅ ใช้ **Console Log** เพื่อสังเกตการเปลี่ยนแปลงของ DOM  
✅ ใช้ **JavaScript DOM Methods** เพื่อแก้ไข HTML และ CSS  
✅ ใช้ **Forms และ Template Literals** เพื่อรับและแสดงค่าจากผู้ใช้  
✅ ฝึก **Event Handling** และสร้าง Interaction บนหน้าเว็บ  

🚀 **ตอนนี้นักศึกษารู้จักวิธีในการสร้าง Web App แบบ Interactive แล้ว!**  
