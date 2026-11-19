# Setup / เตรียมเครื่อง

ขั้นตอนที่ผู้เรียนต้องทำ **ก่อนวันแรกของอบรม** — สั้น กระชับ copy-paste ได้

## Accounts / บัญชีที่ต้องมี

- บัญชี Google (ใช้ตัวเดียวกับที่จะลงแบบฝึกหัดทั้งหมด)
- บัญชี LINE (สำหรับ LINE Developers Console)
- n8n — อบรมเตรียม account ให้แล้ว **ดูในกระดานสื่อสาร**; ถ้า self-host เอง ทำตามหัว Docker ด้านล่าง
- (ระหว่างเรียนจะสร้างร่วมกัน) OpenAI, OpenRouter, Google AI Studio, Pinecone

## Software / ซอฟต์แวร์

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (สำหรับ unit 25 + รัน n8n เอง)
- โดเมนของตัวเอง ([Namecheap](https://www.namecheap.com/) แนะนำ) + บัญชี [Cloudflare](https://dash.cloudflare.com/) ฟรี
- Git สำหรับ clone repo

## Verify / ตรวจสอบก่อนเริ่ม

```bash
docker --version          # Docker version 24+
docker compose version    # v2+
git --version
```

เข้า n8n ของคุณได้ทั้ง `http://localhost:5678` และ `https://n8n.your-domain.com` (ถ้าตั้ง Tunnel แล้ว)

## Self-host เต็มขั้น (หรือเรียน unit 25 แล้วค่อยทำ)

1. จดโดเมน → เพิ่มใน Cloudflare (Free plan) → เปลี่ยน Nameserver ที่ registrar (ปิด DNSSEC)
2. Cloudflare **Zero Trust → Networks → Tunnels → Create a tunnel (Cloudflared)** → ตั้งชื่อ → เลือก **Docker** แล้วคัดลอก token
3. Public hostname: `n8n.your-domain.com` → Service: HTTP → `n8n:5678`
4. Clone แล้วรัน:

```bash
git clone https://github.com/Onto-IQ/n8n-workflow-automation.git
cd n8n-workflow-automation
cp .env.example .env
# แก้: POSTGRES_PASSWORD, N8N_HOST, WEBHOOK_URL=https://n8n.your-domain.com/, CLOUDFLARE_TUNNEL_TOKEN
docker compose up -d
```

> **ทำไมต้อง HTTPS:** Production webhook ของ LINE/Telegram/GitHub ฯลฯ รับเฉพาะ `https://` และฟีเจอร์ chat ของ n8n ต้องการ secure context — จึงต้องมี Tunnel เมื่อเปิด webhook ให้ภายนอก

จัดการต่อ (stop/log/update/backup) ดูหัว "Self-host รัน n8n ของคุณเอง" ใน [README.md](README.md)

จบแล้ว → ดูตารางหน่วยการเรียนใน [README.md](README.md) และเริ่มที่ [lessons/01-what-is-n8n](lessons/01-what-is-n8n/)
