# Database Deployment Guide

คู่มือการ Deploy ฐานข้อมูล PostgreSQL ด้วย Docker สำหรับโปรเจค Full Stack

## ข้อกำหนดเบื้องต้น

- Docker และ Docker Compose ติดตั้งแล้ว
- Git (สำหรับ clone โปรเจค)

## วิธีการ Deploy

### 1. เตรียมไฟล์ Environment Variables

สร้างไฟล์ `.env` ในโฟลเดอร์ `pf-deploy/` และกำหนดค่าตัวแปรต่อไปนี้:

```env
# Project Name
PROJECT_NAME=

# PostgreSQL
POSTGRES_USER=
POSTGRES_PASSWORD=
POSTGRES_DB=
POSTGRES_APP_USER=
POSTGRES_APP_PASSWORD=
POSTGRES_HOST=localhost
POSTGRES_PORT=5432

BACKEND_IMAGE_NAME=
FRONTEND_IMAGE_NAME=

AUTH_SECRET=
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
AUTH_TRUST_HOST=

FRONTEND_PORT=
```

### 2. เริ่มต้น Database Service

เปิด Terminal/Command Prompt และไปยังโฟลเดอร์ `database/`:

```bash
cd pj-deploy
```

รัน Docker Compose เพื่อสร้างและเริ่มต้น PostgreSQL:

```bash
docker-compose up -d
```

### 3. ตรวจสอบสถานะ

ตรวจสอบว่า Container ทำงานอยู่:

```bash
docker-compose ps
```

ดู logs ของ database:

```bash
docker-compose logs postgres
```

### 4. เชื่อมต่อฐานข้อมูล

ใช้ข้อมูลต่อไปนี้ในการเชื่อมต่อจากแอปพลิเคชัน:

- **Host**: `localhost` (หรือ IP ของเซิร์ฟเวอร์)
- **Port**: ค่าที่กำหนดใน `POSTGRES_PORT`
- **Database**: ค่าที่กำหนดใน `POSTGRES_DB`
- **Username**: ค่าที่กำหนดใน `POSTGRES_APP_USER`
- **Password**: ค่าที่กำหนดใน `POSTGRES_APP_PASSWORD`

## คำสั่งที่มีประโยชน์

### หยุดการทำงาน
```bash
docker-compose down
```

### หยุดและลบข้อมูล (ระวัง!)
```bash
docker-compose down -v
```

### รีสตาร์ท
```bash
docker-compose restart
```

### เข้าใช้งาน PostgreSQL CLI
```bash
docker-compose exec postgres psql -U postgres -d your_database_name
```
