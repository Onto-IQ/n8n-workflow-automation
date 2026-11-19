# Lesson 25 — Self-Hosting n8n

เนื้อหาสอนประกอบ slide (slides 230–264 (หน้าจอ 223–257)) — ภาษาไทยอธิบาย, คำสั่ง/ชื่อเครื่องมือเป็นอังกฤษ

## Concepts
- ทางเลือก self-host: Docker (แนะนำ — isolate, อัปเกรด = เปลี่ยน image tag), Direct npm/PM2 (สเปกต่ำ, เสี่ยง permission), Desktop/NPM local (dev เท่านั้น)
- เตรียม HTTPS: จดโดเมน → เพิ่มใน Cloudflare (Free plan) → เปลี่ยน nameserver ที่ registrar (ปิด DNSSEC) → Zero Trust → Networks → Tunnels → Create (Cloudflared) → ตั้งชื่อ → เลือก Docker แล้ว copy token → Public hostname ชี้ http://n8n:5678
- ติดตั้ง: Docker Desktop (WSL update ถ้าถาม) → clone repo นี้ → cp .env.example .env → ใส่ POSTGRES_PASSWORD / N8N_HOST / WEBHOOK_URL / CLOUDFLARE_TUNNEL_TOKEN → docker compose up -d
- ใช้งาน: http://localhost:5678 สำหรับสร้าง flow, https://n8n.your-domain.com เป็น WEBHOOK_URL จริง — HTTPS จำเป็นกับ webhook/chat (เหตุผลใน SETUP.md)
- ดูแลระบบ: logs, อัปเดต, สำรอง data/ (postgres + encryption key) — รายละเอียดใน README หัวข้อการจัดการ n8n

## Demo / walkthrough
1. compose up ให้ทั้งห้องแล้วเข้าผ่านโดเมนของแต่ละคน

## Key takeaways
- HTTPS ไม่ใช่ออปชัน — webhook ทุกบริการต้อง https://

## Check understanding
- ถ้า Encryption Key หาย ต้องเกิดอะไรกับ credentials
