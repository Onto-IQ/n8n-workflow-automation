# Lesson 04 — Flow Control: IF, Switch, Merge

เนื้อหาสอนประกอบ slide (slides 61–64 (หน้าจอ 54–57)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- AND = จริงทุกข้อจึงผ่าน / OR = จริงข้อเดียวก็ผ่าน (ยกตัวอย่างลงทะเบียน+จ่ายเงิน)
- IF Node: true/false สองทาง (เช่น type = vip?)
- Switch Node: หลายทางตาม expression เช่น {{ $json.score >= 80 ? 0 : ($json.score >= 50 ? 1 : 2) }} → เกรด A/B/F
- Merge Node mode Append: รวมผลจากทุกสายงานกลับเป็น list เดียว

## Demo / walkthrough
1. Import 02-Flow-Control-Demo.json → Execute ดูข้อมูลวิ่งคนละสายตาม score/type

## Key takeaways
- VIP ผ่านอัตโนมัติ (IF) ส่วนคนทั่วไปเข้า Switch จัดเกรด แล้ว Merge รวมผล

## Check understanding
- ถ้าต้องแยก 4 กรณี ใช้ node อะไรดีกว่า IF ซ้อนหลายตัว
