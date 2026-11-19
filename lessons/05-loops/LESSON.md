# Lesson 05 — Loop การวนซ้ำ

เนื้อหาสอนประกอบ slide (slides 65–66 (หน้าจอ 58–59)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- ข้อมูลจาก DB มักมาเป็น 1 item ที่ข้างในมี array — ต้อง Split Out (Item Lists) ก่อน
- Loop ส่งทีละ 1 item (batch size = 1) ไปตามเส้นทาง และเมื่อหมดจะออกทาง done
- สำคัญ: ต้องลากเส้นจากท้ายงานกลับเข้า Loop node เสมอ เพื่อบอกว่ารอบจบแล้วให้รับ item ต่อไป

## Demo / walkthrough
1. Import 03-Flow-Control-Demo-Loop-V2.json → Execute แล้วดู execution วิ่งเป็นวงรอบ

## Key takeaways
- Split Out → Loop → ทำงาน → กลับ Loop → done

## Check understanding
- ถ้าลืมลากเส้นกลับเข้า Loop จะเกิดอะไรขึ้น
