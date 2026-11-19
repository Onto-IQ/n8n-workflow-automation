# Lesson 03 — JSON พื้นฐานสำหรับ n8n

เนื้อหาสอนประกอบ slide (slides 42–60 (หน้าจอ 35–53)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- JSON = การจับคู่ key (string เสมอ) กับ value (string/number/boolean/array/object/null)
- { } = 1 item, : คั่น key:value, ฟันหนูครอบ string, , คั่นบรรทัด
- n8n รับข้อมูลเป็น List เสมอ แม้ item เดียว และวน loop ตามจำนวน item ให้อัตโนมัติ
- Fixed fields (ค่าตายตัว) กับ Expression fields (ค่าดิ้นได้ตาม item)
- Expression: {{ $json.key }}, {{ $json["array"][0] }}, {{ $json.object.nestedKey }}, {{ $node["ชื่อ Node"].json.key }}

## Demo / walkthrough
1. เปิด workflow 01-Learn-JSON-Basics จาก solution/ แล้ว Execute ดู output ของแต่ละ node
2. ลองแก้ expression ใน Set node ให้ชี้ไป field อื่น

## Key takeaways
- "25" กับ 25 ต่างกัน — n8n แยก string กับ number เสมอ
- Expression คือพลังของ n8n: เชื่อมโยงข้อมูลระหว่าง node ได้ทุกจุด

## Check understanding
- [1,2,3] คือ data type อะไร ใช้เมื่อไร
- เขียน expression ดึง array สมาชิกตัวที่สามของ $json
