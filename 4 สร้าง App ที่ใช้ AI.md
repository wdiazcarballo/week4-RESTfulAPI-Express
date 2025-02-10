# 4 สร้าง AI Web App เชื่อมต่อ API ขั้นตอนต่อขั้นตอน (React + Vite)
🔹 **วัตถุประสงค์ของบทเรียน**

- สร้าง **React Web App ด้วย Vite**
- เชื่อมต่อ API ของ **AI Services** (OpenAI, Hugging Face, Google Gemini)
- ใช้ **React Hooks (useState, useEffect)**
- ใช้ **fetch() และ axios** ดึงข้อมูลจาก API
- เรียนรู้วิธี **Deploy Web App**
  
## **📍 ขั้นตอนที่ 1: สร้างโปรเจกต์บน GitHub และโคลนมาที่เครื่อง**
### ✅ **1.1 สร้าง GitHub Repository**
1. ไปที่ **[GitHub](https://github.com/)**
2. คลิก **New Repository** (สร้างโปรเจกต์ใหม่)
3. ตั้งชื่อโปรเจกต์เป็น `ai-chatbot`
4. เลือก **Public** หรือ **Private**
5. **✅ เช็ค "Add a README file"**
6. คลิก **Create Repository**

---

### ✅ **1.2 โคลน Repository ลงเครื่อง**
📌 เปิด **Terminal** หรือ **Git Bash** แล้วรัน:
```bash
git clone https://github.com/your-username/ai-chatbot.git
cd ai-chatbot
```

---

### ✅ **1.3 ติดตั้ง Vite และแพ็กเกจที่จำเป็น**
```bash
npm create vite@latest . --template react
npm install
```
📌 **ตรวจสอบโครงสร้างโฟลเดอร์**:
```
ai-chatbot/
│── node_modules/
│── public/
│── src/
│   ├── App.jsx
│   ├── main.jsx
│   ├── components/
│   │   ├── AIChat.jsx
│── .gitignore
│── .env
│── package.json
│── vite.config.js
```

---

### ✅ **1.4 เพิ่ม .gitignore**
📌 เปิดไฟล์ `.gitignore` และเพิ่ม:
```
node_modules/
.env
dist/
```

---

### ✅ **1.5 อัพเดทโปรเจกต์ไปที่ GitHub**
📌 รันคำสั่ง:
```bash
git add .
git commit -m "Initial commit with Vite setup"
git push origin main
```
---

💡 **นักศึกษาสามารถทำ `git push` ทุกครั้งหลังแก้ไขโค้ดเพื่อให้ซิงค์กับ GitHub ได้ตลอดเวลา**  
🎯 **ขั้นตอนต่อไป** → ไปยัง **การตั้งค่า API Key และการพัฒนา Web App!**  

 ขั้นตอนที่ 2: ตั้งค่า API Key สำหรับ AI Services**

### ✅ **2.1 สร้าง `.env` เพื่อเก็บ API Key**

```bash
touch .env
```

👉 เปิดไฟล์ `.env` และเพิ่ม:

```
VITE_OPENAI_KEY=your_openai_api_key
VITE_HUGGINGFACE_KEY=your_huggingface_api_key
VITE_GEMINI_KEY=your_google_api_key
```

📌 **Vite ใช้ `VITE_` นำหน้าทุกตัวแปร** (หากใช้ `REACT_APP_` จะไม่ทำงานใน Vite)

---

## **📍 ขั้นตอนที่ 3: เขียนโค้ดเชื่อมต่อ AI API**

### ✅ **3.1 สร้าง Component `AIChat.jsx`**

📌 สร้างโฟลเดอร์ `src/components/` และสร้างไฟล์ `AIChat.jsx`

```jsx
import { useState } from "react";
import axios from "axios";

function AIChat() {
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");
  const API_KEY = import.meta.env.VITE_OPENAI_KEY; // ดึงค่าจาก .env

  const handleGenerate = async () => {
    setResponse("⏳ AI กำลังคิด...");
    try {
      const res = await axios.post(
        "https://api.openai.com/v1/completions",
        {
          model: "text-davinci-003",
          prompt: prompt,
          max_tokens: 100,
        },
        {
          headers: { Authorization: `Bearer ${API_KEY}` },
        }
      );
      setResponse(res.data.choices[0].text);
    } catch (error) {
      setResponse("❌ เกิดข้อผิดพลาด: " + error.message);
    }
  };

  return (
    <div>
      <h2>🤖 AI Chatbot</h2>
      <textarea
        value={prompt}
        onChange={(e) => setPrompt(e.target.value)}
        placeholder="พิมพ์ข้อความให้ AI ตอบ..."
      />
      <button onClick={handleGenerate}>🧠 ส่งไปให้ AI</button>
      <p><strong>คำตอบ:</strong> {response}</p>
    </div>
  );
}

export default AIChat;
```

---

### ✅ **3.2 เพิ่ม Component ใน `App.jsx`**

📌 เปิด `src/App.jsx` และแก้ไขโค้ด:

```jsx
import AIChat from "./components/AIChat";

function App() {
  return (
    <div>
      <h1>🛠️ ทดสอบ AI API</h1>
      <AIChat />
    </div>
  );
}

export default App;
```

---

## **📍 ขั้นตอนที่ 4: ทดสอบแอปพลิเคชัน**

### ✅ **4.1 รันเซิร์ฟเวอร์ด้วย Vite**

```bash
npm run dev
```

📌 Vite จะบอกว่าเซิร์ฟเวอร์รันที่ **[http://localhost:5173](http://localhost:5173/)**  
เปิด **เว็บเบราว์เซอร์** แล้วเข้าไปที่ **[http://localhost:5173](http://localhost:5173/)**

---

## **📍 ขั้นตอนที่ 5: Deploy แอปไปยัง Production**

### ✅ **5.1 ติดตั้ง Vercel CLI**

```bash
npm install -g vercel
```

### ✅ **5.2 Build โปรเจกต์**

```bash
npm run build
```

### ✅ **5.3 Deploy ไปยัง Vercel**

```bash
vercel
```

📌 หลังจาก **Deploy สำเร็จ** จะได้ URL เช่น:

```
https://ai-chatbot.vercel.app/
```

---

## **📍 ขั้นตอนที่ 6: Challenge ให้นักศึกษา**

✅ **Challenge 1:** ให้เปลี่ยน API เป็น **Google Gemini API หรือ Hugging Face API**  
✅ **Challenge 2:** เพิ่ม **UI ให้สามารถเลือกระหว่าง AI Model (ChatGPT, Gemini, Hugging Face)**  
✅ **Challenge 3:** ให้เพิ่ม **ฟังก์ชันสร้างภาพจากข้อความโดยใช้ OpenAI DALL·E**

---

🎯 **สรุปสิ่งที่นักศึกษาได้เรียนรู้** ✅ ใช้ **Vite** สร้าง React Web App  
✅ ใช้ **Postman และ fetch/axios** ทดสอบ API  
✅ เชื่อมต่อ **OpenAI API** และแสดงผล AI Response  
✅ ใช้ **.env เก็บ API Key**  
✅ Deploy **React App ไปยัง Vercel**
