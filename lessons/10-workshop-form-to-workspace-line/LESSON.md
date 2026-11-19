# Lesson 10 — Workshop #1: ฟอร์ม → Google Workspace + LINE

เนื้อหาสอนประกอบ slide (slides 92–99 (หน้าจอ 85–92)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- Business logic ของระบบรับเรื่อง: n8n Form รับข้อมูล → Code แปลง+ตั้ง Priority (HIGH เมื่อมีคำว่า เร่งด่วน) → Sheets เก็บ transaction → IF มีวันนัด → Calendar สร้าง event+เชิญอีเมล → Docs ออก brief → Drive สำรอง .txt → LINE แจ้งเฉพาะ HIGH
- เทคนิค: Dropdown/Date picker ควบคุมคุณภาพข้อมูล, Respond Mode = Response Node เผื่อแต่งหน้าขอบคุณ, แยก logic แจ้งเตือนลด noise ในกลุ่ม LINE

## Demo / walkthrough
1. Import workflow จาก solution/ แล้วไล่อ่านทีละบล็อกก่อนรันจริง

## Key takeaways
- จากฟอร์มใบเดียวกระจายไป 6 ปลายทางอัตโนมัติ — แพตเทิรับเรื่อง/จอง/ลงทะเบียนใช้ซ้ำได้ทั่วไป

## Check understanding
- ทำไมต้องคำนวณ Priority ใน Code node ก่อนแยกสาย
