# 25 — Self-Hosting n8n (Docker + Cloudflare) / Self-hosting n8n

| | |
|--|--|
| บทเรียน | หน้านี้ (README.md) |
| ลงมือทำ | [exercises/25-self-hosting](../../exercises/25-self-hosting/README.md) |
| เวลาโดยประมาณ | ~90 นาที |
| อ้างอิง slide | N8N-L1-Onto-IQ-v7 หน้า 223–257 |
| ตั้งค่าเครื่องก่อน | [SETUP.md](../SETUP.md) |

หน่วยนี้ทำให้คุณ **เป็นเจ้าของ n8n ของตัวเอง** — รันด้วย Docker Compose (n8n + PostgreSQL + Cloudflare Tunnel) บนเครื่อง/VPS ได้ HTTPS จริงผ่านโดเมนของตัวเอง ควบคุมข้อมูล 100% และรู้วิธี backup/restore ที่ถูกต้อง HTTPS จากหน่วยนี้ยังเป็นเงื่อนไขของฟีเจอร์ **n8n Agents** ในหน่วยถัดไป (26) ด้วย

## ทำไมต้อง HTTPS (สรุปเหตุผล)

- Production webhook ของบริการภายนอก (LINE, Telegram, Shopify, GitHub) รับเฉพาะ `https://`
- ฟีเจอร์เบราว์เซอร์ที่ต้อง secure context (chat, notifications) ใช้ได้เฉพาะ HTTPS หรือ localhost
- ข้อมูลที่ไม่เข้ารหัสเสี่ยง MITM — โปรเจกต์นี้จึงใช้ **Cloudflare Tunnel** ให้ HTTPS โดยไม่ต้องจัด certificate เอง

## ทางเลือกการติดตั้ง

- **Docker** (แนะนำ) — isolate สะอาด อัปเกรดง่ายแค่เปลี่ยน image tag
- **Direct npm/PM2** — สเปกเครื่องต่ำได้ แต่เสี่ยงปัญหา permission
- **Desktop/local npm** — สำหรับ dev ลองของเท่านั้น ไม่ใช่ production

## ขั้นเตรียม Domain + Cloudflare

1. **จดโดเมน** — ผ่าน namecheap.com (หรือผู้ให้บริการอื่น)
2. **สมัคร Cloudflare (ฟรี)** → เพิ่มโดเมน → เลือก Free Plan
3. ที่ Namecheap: เปลี่ยน **Name servers** ไปเป็นของ Cloudflare และ **ปิด DNSSEC**
4. Cloudflare: Check name servers จนสถานะ active

## สร้าง Zero Trust Tunnel

1. Cloudflare Dashboard → **Zero Trust** → **Networks → Connectors → Tunnels**
2. **Create a tunnel** → ตั้งชื่อ (เช่น `phakkhaphong.fit`) → เลือก connector เป็น **Cloudflared** (ไม่ใช่ WARP)
3. เลือกวิธีติดตั้งเป็น **Docker** แล้วคัดลอก **Tunnel Token** (จะได้คำสั่งระบุ token มาให้ — เก็บไว้ใส่ `.env` ตอนต่อไป ไม่ต้องรันคำสั่งนั้นซ้ำ)
4. **Route Traffic** — Public hostname ชี้มาที่ service ชื่อ `n8n` port 5678 (HTTP)

## รัน n8n ด้วย Docker Compose

1. ติดตั้ง **Docker Desktop** (docker.com) — รวมขั้น WSL update/restart บน Windows ถ้าระบบแจ้ง
2. Clone/Download repo นี้ → เข้าโฟลเดอร์ → `cp .env.example .env` แล้วแก้ 5 ค่า: `POSTGRES_PASSWORD`, `N8N_HOST` (โดเมนของคุณ ไม่ใส่ https://), `WEBHOOK_URL` (เต็ม ๆ https://…), `CLOUDFLARE_TUNNEL_TOKEN`, `GENERIC_TIMEZONE`
3. **`docker compose up -d`** → เข้า `http://localhost:5678` ตั้ง Owner account และทดสอบผ่านโดเมน https ของคุณ (ตั้ง WEBHOOK_URL ให้ตรง)

## การดูแลระยะยาว

```bash
docker compose down                                # หยุด
docker compose logs -f n8n                         # ดู log
docker compose pull && docker compose up -d        # อัปเดตเวอร์ชัน
docker compose exec n8n n8n user-management:reset  # ลืมรหัสผ่าน
cp -r data data-backup-$(date +%Y%m%d)             # สำรอง
```

- **สำรองให้ครบคู่กัน**: `data/postgres/` (workflows, credentials, executions) และ `data/n8n/` (config + **Encryption Key** ใช้ถอดรหัส credentials) — ขาดใดขาดหนึ่ง restore ไม่ครบ
- **Restore**: นำโฟลเดอร์กลับมาเป็น `data/` ใช้ `.env` เดิม (อย่างน้อย POSTGRES_USER/PASSWORD/DB) แล้ว `docker compose up -d`
- อัปเกรด = เปลี่ยน image tag ใน `docker-compose.yml` (repo pin `n8nio/n8n:2.48.5` ไว้แล้ว) — อ่าน Migration Report ก่อนขยับ version ใหญ่

## Key takeaways

- HTTPS ไม่ใช่ออปชัน — webhook ของทุกบริการต้องเป็น `https://`
- ใช้ `http://localhost:5678` สำหรับสร้าง flow, โดเมน `https://` ของตัวเองสำหรับ webhook จริง

## ลงมือทำ

เปิด [exercises/25-self-hosting/LAB.md](../../exercises/25-self-hosting/LAB.md) — ติดตั้ง Docker, ตั้ง `.env`, รัน compose, ตั้ง owner, และทดสอบเข้าผ่านโดเมน HTTPS ของตัวเอง

## Check understanding

1. ทำไม self-host ต้องมี Cloudflare Tunnel — ถ้าไม่มี อะไรเสียก่อน
2. `data/n8n/` กับ `data/postgres/` เก็บอะไร และทำไม backup ต้องครบคู่
3. WEBHOOK_URL ผิดมีผลกับ workflow แบบไหน
4. ถ้า Encryption Key หาย จะเกิดอะไรขึ้นกับ credentials ที่เก็บไว้

## Next

→ [exercises/25-self-hosting](../../exercises/25-self-hosting/README.md) — เป็นเจ้าของ n8n ของคุณเอง พร้อมรองรับทุกฟีเจอร์ในหน่วยสุดท้าย
→ บทถัดไป: [26 — n8n Agents: Agent Builder](../26-agents/README.md)
