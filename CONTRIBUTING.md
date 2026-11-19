# Contributing / การร่วมพัฒนาเนื้อหา

Repo นี้เป็นคอร์สขององค์กร **Onto-IQ** (topic family: AI) สร้างบนรูปแบบ [course-template](https://github.com/phakkhaphong/course-template) เดียวกัน

## เพิ่มหรือแก้หน่วยการเรียน (unit)

1. แก้ `COURSE.md` front matter ถ้าข้อมูลคอร์สเปลี่ยน (ชื่อ, repo, path) แล้วปรับ outline ใน `README.md` (รักษาลำดับหัวข้อเดิม 9 ส่วน)
2. หน่วยใหม่ต้องมี **คู่กันเสมอ**: `lessons/NN-slug/` (README.md + LESSON.md) และ `exercises/NN-slug/` (README.md + LAB.md + starter/ + solution/) — ชื่อโฟลเดอร์ `NN-slug` ตรงกันทั้งสองฝั่ง, NN = เลขสองหลัก, slug = lowercase อังกฤษ/ตัวเลข + ขีด
3. ไฟล์ประกอบ (slide, dataset, รูป, สคริปต์) ใส่ใต้ `other/` เท่านั้น — ชื่อไฟล์ไทยใช้ได้ใต้ `other/` แต่ **ห้าม** ใน lessons/exercises
4. เนื้อหาสอนให้สอดคล้องกับ deck ใน `other/slides/` — ระบุช่วง slide อ้างอิงไว้หัว lesson
5. ห้ามสร้าง top-level โฟลเดอร์ใหม่ (เช่น `modules/`, `labs/`) — ต่อโครงสร้างใต้ `other/` แทน
6. ห้าม commit secrets (`.env`, API key) หรือไฟล์ใหญ่เกิน 100 MB (GitHub บล็อก); binary ใหญ่ใช้ link ใน `other/datasets/README.md`

## ตรวจก่อนเปิด PR

```bash
bash other/scripts/check_structure.sh
```

CI รันเช็คนี้ทุก push/PR ผ่าน `.github/workflows/structure-check.yml` (คัดลอกจาก `other/scripts/structure-check.workflow.yml` แล้ว)
