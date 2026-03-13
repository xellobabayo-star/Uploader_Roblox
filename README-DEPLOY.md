# 🚀 XELLO Audio — Panduan Deploy

## ✅ Rekomendasi: Railway (TERBAIK untuk app ini)

App ini menggunakan:
- **SQLite** → butuh filesystem persisten
- **FFmpeg** → butuh binary di server
- **youtube-dl** → butuh binary di server
- **SSE streaming** → butuh koneksi long-running
- **express-session** → butuh state persisten

Railway mendukung semua itu secara native.

### Deploy ke Railway
1. Push ke GitHub
2. Buka [railway.app](https://railway.app) → New Project → Deploy from GitHub
3. Set environment variables di Railway dashboard:

```env
SESSION_SECRET=ganti_dengan_string_random_panjang
ADMIN_USERNAME=admin
ADMIN_PASSWORD=password_admin_kamu
TIER_TRIAL_LIMIT=3
TIER_BEGINNER_LIMIT=50
```

4. Railway otomatis mendeteksi `npm start` dan menjalankan app.

---

## ⚠️ Vercel (Ada Keterbatasan)

Vercel bisa digunakan tapi dengan **catatan penting**:

| Fitur | Status di Vercel |
|-------|-----------------|
| Web UI, Auth, Upload ke Roblox | ✅ Bisa |
| SQLite database | ⚠️ Data reset tiap cold start (pakai `/tmp`) |
| FFmpeg (tempo/pitch) | ✅ Bisa (via @ffmpeg-installer) |
| youtube-dl (fetch YouTube) | ❌ Tidak tersedia |
| SSE streaming upload | ⚠️ Timeout 10-60 detik di Vercel |
| Sessions | ⚠️ Tidak persist antar instances |

### Deploy ke Vercel
1. Install Vercel CLI: `npm i -g vercel`
2. Jalankan: `vercel`
3. Set env vars via Vercel dashboard atau `vercel env add`

> **Untuk produksi dengan banyak user, gunakan Railway.**

---

## 🐳 Docker (VPS/Self-host)

```bash
docker build -t xello-audio .
docker run -d -p 8080:8080 \
  -v $(pwd)/data:/app/data \
  -e SESSION_SECRET=xxx \
  -e ADMIN_USERNAME=admin \
  -e ADMIN_PASSWORD=xxx \
  xello-audio
```
