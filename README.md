Siap, Fabian 💪 berikut versi lengkap dan profesional dari file **`README.md`** — sudah saya susun agar langsung cocok dipasang di GitHub repo Anda (`bantuku-api` atau nama apa pun).
Termasuk logo-style heading, deskripsi, arsitektur, setup, deploy ke Vercel, testing di Postman, integrasi Android, dan tips keamanan.

---

## 🟣 **README.md — BANTUKU API (Express.js + MySQL + Vercel)**

```markdown
# 🟣 BANTUKU API (Express.js + MySQL + Vercel)

> RESTful API untuk aplikasi **Donasi dan Kampanye Sosial** — dibuat oleh **Fabian Permadi Developer**.  
> Menggunakan **Express.js**, **MySQL**, dan **JWT RS256** untuk keamanan tingkat tinggi.  
> Didesain agar bisa diintegrasikan ke **Android Studio (Java / Kotlin)** maupun aplikasi web modern.

---

## 🚀 Fitur Utama

✅ Autentikasi Aman — JWT (RS256) + Password Hashing (bcrypt)  
✅ API Key Internal — `FABIANPERMADIDEVELOPER_2025_140524`  
✅ Modul Lengkap: Auth, Users, Campaigns, Donations  
✅ Rate Limiting & Helmet Security  
✅ CORS Whitelist Multi-domain  
✅ Siap Deploy di Vercel (Serverless Node.js)  
✅ Database MySQL / MariaDB  
✅ Struktur modular dan mudah dikembangkan  

---

## 🧱 Arsitektur Proyek

```

bantuku-api/
├─ index.js
├─ package.json
├─ vercel.json
├─ .env.example
├─ db.js
├─ routes/
│   ├─ auth.js
│   ├─ users.js
│   ├─ campaigns.js
│   └─ donations.js
├─ middleware/
│   ├─ auth.js
│   ├─ apiKey.js
│   └─ rateLimiter.js
└─ utils/
├─ jwt.js
└─ validators.js

````

---

## ⚙️ Instalasi Lokal

### 1️⃣ Clone Repository
```bash
git clone https://github.com/<username>/<repo-name>.git
cd bantuku-api
````

### 2️⃣ Install Dependensi

```bash
npm install
```

### 3️⃣ Jalankan Server

```bash
npm run dev
```

Server berjalan di:

```
http://localhost:3000
```

---

## ⚙️ Konfigurasi `.env`

Buat file `.env` berdasarkan `.env.example` dan isi seperti berikut:

```
DB_HOST=
DB_PORT=3306
DB_USER=
DB_PASSWORD=
DB_NAME=

JWT_PRIVATE_KEY=-----BEGIN PRIVATE KEY-----\nMIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQC5mPQ+zoevU0TI\n...\n-----END PRIVATE KEY-----
JWT_PUBLIC_KEY=-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAuZj0P...\n-----END PUBLIC KEY-----
JWT_EXPIRES_IN=1d

API_KEY=FABIANPERMADIDEVELOPER_2025_140524
CORS_ORIGINS=https://kubantuin.id,https://api.kubantuin.id,https://android.kubantuin.org,https://api-gray-rho-12.vercel.app

RATE_LIMIT_WINDOW=15
RATE_LIMIT_MAX=300
NODE_ENV=production
```

> ⚠️ Pastikan key JWT dalam **satu baris dengan `\n`**, bukan multiline.

---

## ☁️ Deploy ke Vercel

1. Push project ini ke GitHub
2. Masuk ke [https://vercel.com](https://vercel.com)
3. Klik **“Add New Project”**
4. Pilih repository Anda
5. Tambahkan **Environment Variables** dari `.env`
6. Klik **Deploy**

URL hasil deploy akan menjadi seperti:

```
https://bantuku-api.vercel.app
```

Cek status:

```
GET https://bantuku-api.vercel.app/health
```

Response:

```json
{ "status": "ok", "env": "production" }
```

---

## 🧪 Testing API di Postman

Gunakan base URL:

```
https://api-gray-rho-12.vercel.app
```

### 🔹 Register

```
POST /api/auth/register
```

**Body:**

```json
{
  "full_name": "Fabian Developer",
  "email": "fabian@example.com",
  "password": "Secret123",
  "phone_number": "08123456789"
}
```

### 🔹 Login

```
POST /api/auth/login
```

**Body:**

```json
{
  "email": "fabian@example.com",
  "password": "Secret123"
}
```

**Response:**

```json
{
  "token": "JWT_TOKEN_HERE",
  "user": { "id": 1, "full_name": "Fabian Developer", "role": "user" }
}
```

### 🔹 Get Profil

```
GET /api/users/me
```

**Headers:**

```
Authorization: Bearer <JWT_TOKEN_HERE>
```

### 🔹 List Campaigns

```
GET /api/campaigns?page=1
```

### 🔹 Donasi

```
POST /api/donations
```

**Body:**

```json
{
  "campaign_id": 1,
  "amount": 50000,
  "donor_name": "Anonim",
  "message": "Semoga berkah",
  "payment_method": "bank_transfer"
}
```

**Response:**

```json
{ "order_id": "DKS-1731063230-500" }
```

---

## 🔑 API Key (Internal)

Beberapa endpoint (admin/internal) bisa memakai header:

```
x-api-key: FABIANPERMADIDEVELOPER_2025_140524
```

---

## 📱 Integrasi ke Android Studio

### Java (OkHttp)

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
    .url("https://api-gray-rho-12.vercel.app/api/campaigns")
    .build();

client.newCall(request).enqueue(new Callback() {
  @Override public void onFailure(Call call, IOException e) { e.printStackTrace(); }
  @Override public void onResponse(Call call, Response response) throws IOException {
    String json = response.body().string();
    System.out.println(json);
  }
});
```

### Kotlin (Retrofit)

```kotlin
@GET("api/campaigns")
suspend fun listCampaigns(@Query("page") page: Int = 1): Response<CampaignList>
```

---

## 🛡️ Keamanan

* Semua password terenkripsi `bcrypt`
* JWT memakai **RS256 (asymmetric)** — private & public key terpisah
* Proteksi tambahan: Helmet, CORS, Rate Limiting, API Key
* Tidak menyimpan file di serverless (gunakan CDN / S3 untuk upload)
* Semua koneksi via HTTPS otomatis oleh Vercel

---

## 🧠 Tips Tambahan

* Gunakan **Vercel Secret** untuk key sensitif
* Backup database secara berkala
* Gunakan **Cloudflare** untuk proteksi DDoS & WAF
* Tambahkan log audit untuk transaksi dan login

---

## 🧾 Lisensi

MIT License © 2025
Developed by **Fabian Permadi Developer**

---

### 💬 Kontak

📧 Email: [fabian@example.com](mailto:fabian@example.com)
🌐 Website: [https://kubantuin.id](https://kubantuin.id)

```

---

## 📦 Selanjutnya  
Saya bisa bantu:
- Buatkan **ZIP project lengkap** (semua file kode + README ini)
- Siapkan **`vercel.json`** & `.env.example` otomatis  
- Tambahkan badge GitHub Actions (opsional CI/CD)

Apakah mau saya buatkan **ZIP project siap upload ke GitHub & deploy ke Vercel** dengan README ini di dalamnya?
```
