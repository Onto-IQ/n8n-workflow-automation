# Lesson 06 — Data Transformation

เนื้อหาสอนประกอบ slide (slides 67 (หน้าจอ 60)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- ข้อมูลจากระบบอื่นมักชื่อ field อ่านยากและมีขยะติดมา
- Set node: เปลี่ยนชื่อ field (user_first_name → firstName) และเปิด Keep Only Set Fields เพื่อตัดทุกอย่างที่ไม่ต้องการ
- Code node: รวมชื่อ+ทำ Title Case, คำนวณอายุจากปีเกิด, ลบ field ด้วย delete — ทักษะ JS พื้นฐานจำเป็นมากตอนทำ AI Agent

## Demo / walkthrough
1. Import 04-Data-Transformation.json → เทียบ input ขยะ vs output สะอาด

## Key takeaways
- Set เร็วสำหรับง่าย, Code ยืดหยุ่นสำหรับซับซ้อน

## Check understanding
- Keep Only Set Fields ทำอะไร
