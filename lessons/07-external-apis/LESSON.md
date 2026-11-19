# Lesson 07 — เรียกใช้ External APIs

เนื้อหาสอนประกอบ slide (slides 68 (หน้าจอ 61)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- GET ดึงข้อมูล (ทดลองกับ official-joke-api.appspot.com/random_joke — ไม่ต้อง key)
- POST ส่งข้อมูล (ทดสอบปลายทางที่ httpbin.org/post พร้อม body JSON)
- API จริง (LINE, OpenAI) ต้องมี key — ตั้งได้ที่ Authentication: Basic Auth, Header Auth (X-API-KEY), Bearer Token — พื้นฐานสำคัญก่อนสร้าง AI Agent ที่ใช้ Tools

## Demo / walkthrough
1. สร้าง HTTP Request GET มุก → Set แยก setup/punchline → POST ไป httpbin

## Key takeaways
- HTTP Request node คือสวิสอาร์มีนีฟ — ต่อได้ทุกบริการที่มี REST API

## Check understanding
- Bearer token ใส่ตรงไหนของ HTTP Request node
