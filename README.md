# 🌐 Full-Stack Event & Post Platform

โปรเจกต์นี้เป็นระบบเว็บแอปพลิเคชัน **CMU Hub** เป็นเว็บบอร์ดมุ่งเน้นสำหรับ นักศึกษา ใน มหาลัยเชียงใหม่โดยเฉพาะ
เป็นพื้นที่สำหรับการสอบถาม, ให้ความรู้ ,ประกาศต่างๆในมหาวิทยาลัย,พูดคุย
และทำกิจกรรมร่วมกันภายในมหาวิทยาลัย

---

## 👥 สมาชิกในกลุ่ม
<div align="center"
     style="
       display: flex;
       justify-content: center;
       align-items: center;
       gap: 16px;
       flex-wrap: nowrap;
     ">
  <img src="./member/1.jpg"
       style="width: 160px; height: 160px; object-fit: cover; object-position: center; border-radius: 12px;" />
  <img src="./member/2.jpg"
       style="width: 160px; height: 160px; object-fit: cover; object-position: center; border-radius: 12px;" />
  <img src="./member/3.jpg"
       style="width: 160px; height: 160px; object-fit: cover; object-position: center; border-radius: 12px;" />
</div>

<table align="center">
  <tr>
    <td align="center" width="265px">
      <b>อภิวิชญ์ บุญฤทธิ์</b><br />
      <i>650612106</i><br />
    </td>
    <td align="center" width="285px">
      <b>อัฎษฎา วิริยา</b><br />
      <i>650612107</i><br />
    </td>
    <td align="center" width="265px">
      <b>อาทิตยา เที่ยงอารมณ์</b><br />
      <i>650612108</i><br />
    </td>
  </tr>
</table>


---

## 🛠️ **Technology Stack**

> ระบบนี้ถูกพัฒนาโดยใช้เทคโนโลยีสมัยใหม่แบบ Full-Stack เพื่อให้ได้ทั้งประสิทธิภาพ ความปลอดภัย และการดูแลรักษาง่ายในระยะยาว

| 🧩 **Layer** | ⚙️ **Technology Used** |
| :----------- | :--------------------- |
| **🎨 Frontend** | [Next.js](https://nextjs.org/) + [Tailwind CSS](https://tailwindcss.com/) + [shadcn/ui](https://ui.shadcn.com/) |
| **🚀 Backend (API)** | [Hono](https://hono.dev/) — running on [Bun](https://bun.sh/) |
| **🧠 ORM Layer** | [Prisma ORM](https://www.prisma.io/) |
| **🗄️ Database** | [PostgreSQL 17](https://www.postgresql.org/) |
| **🔐 Authentication** | [Auth.js](https://authjs.dev/) |
| **🐳 Deployment & Environment** | [Docker Compose](https://docs.docker.com/compose/) |

---

## วิธีการ Deploy

### 1. เตรียมไฟล์ Environment Variables

สร้างไฟล์ `.env` รูปแบบตาม `.env.local` และกำหนดค่าตัวแปร

### 2. เริ่มต้น

รัน Docker Compose เพื่อสร้างและเริ่มต้น:

```bash
docker compose -f docker-compose.yml up -d
```

## จะ Upgrade ตัวเองเป็น ADMIN

เมื่อยังไม่มี Admin และไม่สามารถมีใครให้ Admin ได้

```bash
# เข้าไปยัง PostgreSQL
docker-compose -f docker-compose.yml exec postgres psql -U [POSTGRES_USER] -d cmuhub

# เข้าหา id จากการหา email
SELECT id, email, role FROM public."User" WHERE email = '{Your email}';

# Update role ของตัวเอง
UPDATE public."User" SET "role"='ADMIN'::public."Role" WHERE id='{id ที่ได้จาก command ข้างบน}';
```

## 🧭 **ขั้นตอนการพัฒนาต่อ (Development Steps)**

> โปรเจกต์นี้ถูกแยกออกเป็น 2 ส่วนหลัก ได้แก่ **Backend** และ **Frontend**  
> เพื่อความสะดวกในการพัฒนา ดูแลระบบ และรองรับการขยายในอนาคต

---

### 🔹 **Repository หลัก**
- **Backend:** [https://github.com/261497-Full-Stack-1-68/pj-backend](https://github.com/261497-Full-Stack-1-68/pj-backend)  
- **Frontend:** [https://github.com/261497-Full-Stack-1-68/pj-frontend](https://github.com/261497-Full-Stack-1-68/pj-frontend)

---

# ⚙️ ขั้นตอนการพัฒนา (Development Steps)

## 1️⃣ Clone โปรเจกต์ทั้งสอง
```bash
git clone https://github.com/261497-Full-Stack-1-68/pj-backend
git clone https://github.com/261497-Full-Stack-1-68/pj-frontend
```
รัน postgres ใน docker-compose.yml ใน repo ปัจจุบันโดยลบ service อื่นทั้งหมด หรือปิดไว้ เหลือไว้แค่ service postgres

---

## 2️⃣ ตั้งค่า Environment Variables

### 🔧 env for backend
```bash
DATABASE_URL="postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:5433/cmuhub"
```

### 🔧 env for frontend
```bash
DATABASE_URL="postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:5433/cmuhub"
AUTH_SECRET=${AUTH_SECRET}
GOOGLE_CLIENT_ID=${GOOGLE_CLIENT_ID}
GOOGLE_CLIENT_SECRET=${GOOGLE_CLIENT_SECRET}
AUTH_TRUST_HOST=${AUTH_TRUST_HOST}
```

---

## 3️⃣ รันระบบด้วย npm หรือ bun ทั้งสอง
หลังจากตั้งค่า `.env` ทั้งสองโปรเจกต์เรียบร้อยแล้ว ให้รันระบบทั้งหมดด้วยคำสั่ง:
```bash
# ในโฟลเดอร์ backend และ frontend
bun install
# หรือ
npm install

# ตามด้วย
bun run dev
# หรือ
npm run dev
```

ระบบจะเริ่มต้นทั้ง **PostgreSQL**, **Backend (Hono)** และ **Frontend (Next.js)**  
จากนั้นสามารถเข้าทดสอบได้ที่  
🔗 **http://localhost:3005**

---