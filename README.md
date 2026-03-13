<div align="center">

```
██╗  ██╗███████╗██╗     ██╗      ██████╗     ███████╗████████╗██╗   ██╗██████╗ ██╗ ██████╗
╚██╗██╔╝██╔════╝██║     ██║     ██╔═══██╗    ██╔════╝╚══██╔══╝██║   ██║██╔══██╗██║██╔═══██╗
 ╚███╔╝ █████╗  ██║     ██║     ██║   ██║    ███████╗   ██║   ██║   ██║██║  ██║██║██║   ██║
 ██╔██╗ ██╔══╝  ██║     ██║     ██║   ██║    ╚════██║   ██║   ██║   ██║██║  ██║██║██║   ██║
██╔╝ ██╗███████╗███████╗███████╗╚██████╔╝    ███████║   ██║   ╚██████╔╝██████╔╝██║╚██████╔╝
╚═╝  ╚═╝╚══════╝╚══════╝╚══════╝ ╚═════╝     ╚══════╝   ╚═╝    ╚═════╝ ╚═════╝ ╚═╝ ╚═════╝
```

### 🎵 Roblox Audio Uploader — SaaS Platform

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org)
[![Express](https://img.shields.io/badge/Express-4.18-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com)
[![SQLite](https://img.shields.io/badge/SQLite-3-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://sqlite.org)
[![Railway](https://img.shields.io/badge/Deploy-Railway-0B0D0E?style=for-the-badge&logo=railway&logoColor=white)](https://railway.app)
[![License](https://img.shields.io/badge/License-MIT-00e5ff?style=for-the-badge)](LICENSE)

> **Platform SaaS untuk upload audio ke Roblox secara bulk — lengkap dengan audio processor, tier system, dan admin panel.**

</div>

---

## ✨ Fitur Unggulan

<table>
<tr>
<td width="50%">

### 🎵 Audio Engine
- Upload bulk MP3 ke Roblox API
- **Speed processor** 1×–16× (support lagu panjang)
- **Pitch shifter** ±24 semitone
- Waveform visualizer real-time
- Audio preview sebelum upload
- SSE streaming progress (anti-timeout)

</td>
<td width="50%">

### 🔐 Auth & Tier System
- Register/Login dengan invite code
- **3 Tier:** Trial · Beginner · Pro
- Quota upload per bulan otomatis reset
- Support Personal & **Group Account** Roblox
- API Key tersimpan aman di database

</td>
</tr>
<tr>
<td width="50%">

### 🛠️ Admin Panel
- Manajemen user (aktif/nonaktif/hapus)
- Generate kode invite (custom/auto)
- Atur tier, expiry, max uses
- Statistik upload & history
- Admin settings persisten (SQLite)

</td>
<td width="50%">

### 🎛️ Audio Editor
- Trim audio (start & end)
- Fade in / Fade out
- Download dari YouTube & SoundCloud
- Export hasil sebagai MP3
- Preview langsung di browser

</td>
</tr>
</table>

---

## 🖥️ Preview

```
┌─────────────────────────────────────────────────────────────┐
│  ◈ AUDIO PROCESSOR                                          │
│                                                             │
│  🎚️ Ubah Speed & Pitch              [ ● ON ]               │
│                                                             │
│  UPLOAD SPEED          4.0×   │   PITCH            +12ST   │
│  ████████████░░░  4.0×        │   ░░░░░░█████░  +12st     │
│  1× ─────── 8× ─────── 16×   │   -24st ── 0st ── +24st   │
│                                                             │
│  🎮 Panduan PlaybackSpeed Roblox                            │
│  Audio diupload 4.0× lebih cepat   [ PlaybackSpeed = 0.25 ]│
│  Sound.PlaybackSpeed = 0.25  -- set di script Roblox       │
│  💡 Rumus: PlaybackSpeed = 1 ÷ Upload Speed                │
│                                                             │
│  📝 DESKRIPSI ASSET                              OPSIONAL  │
│  ┌────────────────────────────────────────────────────────┐ │
│  │ Contoh: BGM lobby club, looping ambient, BPM 128...   │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Deploy ke Railway (Rekomendasi)

```bash
# 1. Clone / upload ke GitHub

# 2. Buka railway.app → New Project → Deploy from GitHub

# 3. Set environment variables:
SESSION_SECRET=string_random_panjang_minimal_32_karakter
ADMIN_USERNAME=admin
ADMIN_PASSWORD=password_admin_kamu
TIER_TRIAL_LIMIT=3
TIER_BEGINNER_LIMIT=50
```

> Railway otomatis mendeteksi `npm start` dan menjalankan app. Done! 🎉

---

### Self-Host / VPS

```bash
# Install dependencies
npm install

# Copy & edit konfigurasi
cp .env.example .env
nano .env

# Jalankan
node server.js
```

### Docker

```bash
docker build -t xello-studio .
docker run -d \
  -p 8080:8080 \
  -v $(pwd)/data:/app/data \
  -e SESSION_SECRET=xxx \
  -e ADMIN_USERNAME=admin \
  -e ADMIN_PASSWORD=xxx \
  xello-studio
```

---

## ⚙️ Konfigurasi `.env`

```env
# ─── Server ──────────────────────────────────
PORT=8080
SESSION_SECRET=ganti_dengan_string_acak_panjang_ini

# ─── Admin ───────────────────────────────────
ADMIN_USERNAME=admin
ADMIN_PASSWORD=password_kamu

# ─── Tier Limits (upload/bulan) ──────────────
TIER_TRIAL_LIMIT=3
TIER_BEGINNER_LIMIT=50
TIER_PRO_LIMIT=999999
```

---

## 📱 Halaman & Routes

| Route | Deskripsi | Akses |
|-------|-----------|-------|
| `/` | Landing page | Public |
| `/dashboard` | Dashboard upload & settings | User login |
| `/admin` | Panel admin | Admin only |
| `/api/me` | Info user session | Auth |
| `/api/upload` | Upload audio (SSE stream) | Auth |
| `/api/settings/roblox` | Simpan Roblox account | Auth |
| `/api/editor/process` | Proses audio (trim/fade) | Auth |
| `/api/fetch-audio` | Download dari YouTube/SC | Auth |

---

## 🎫 Sistem Tier & Invite

```
TRIAL      →   3 upload / bulan   (default semua user baru)
BEGINNER   →  50 upload / bulan   (redeem kode invite)
PRO        →   ∞ unlimited         (redeem kode invite)
```

**Cara buat kode invite:**
1. Login ke `/admin`
2. Menu **Invite Codes** → **BUAT KODE**
3. Pilih tier, max uses, expiry date
4. Share kode ke user

**User redeem:**
- Saat register → langsung dapat tier
- Di dashboard → Settings → Invite Code

---

## 🎮 Cara Pakai di Roblox

Setelah upload dengan speed **X×**, set di script Roblox:

```lua
-- Rumus: PlaybackSpeed = 1 ÷ Upload Speed
-- Contoh upload 4× → PlaybackSpeed = 0.25

local Sound = workspace.MySound
Sound.SoundId = "rbxassetid://ASSET_ID_DISINI"
Sound.PlaybackSpeed = 0.25   -- sesuaikan dengan speed yang dipakai
Sound.Looped = true
Sound:Play()
```

| Upload Speed | PlaybackSpeed | Cocok untuk |
|---|---|---|
| 2× | `0.5` | Lagu ≤ 14 menit |
| 4× | `0.25` | Lagu ≤ 28 menit |
| 8× | `0.125` | Lagu ≤ 56 menit |
| 10× | `0.1` | Lagu ~1 jam |

---

## 🔧 Tech Stack

| Layer | Teknologi |
|-------|-----------|
| Runtime | Node.js 18+ |
| Framework | Express.js 4 |
| Database | SQLite (better-sqlite3) |
| Auth | express-session + bcryptjs |
| Audio Processing | FFmpeg (@ffmpeg-installer) |
| YouTube Download | youtube-dl-exec |
| Roblox API | Open Cloud Assets v1 |
| Frontend | Vanilla JS + CSS Custom Properties |
| Deploy | Railway / Docker / VPS |

---

## 📁 Struktur Project

```
xello-studio/
├── server.js           ← Backend utama (Express + SQLite)
├── package.json
├── .env                ← Konfigurasi (jangan di-commit!)
├── Dockerfile
├── vercel.json
├── public/
│   ├── index.html      ← Landing page
│   ├── dashboard.html  ← Dashboard user
│   ├── admin.html      ← Admin panel
│   └── css/
│       ├── base.css
│       ├── index.css
│       ├── dashboard.css
│       └── admin.css
└── data/
    └── xello.sqlite    ← Database (auto-created)
```

---

## ⚠️ Catatan Penting

> **FFmpeg** — Fitur speed & pitch butuh FFmpeg. Di Railway/VPS otomatis tersedia via `@ffmpeg-installer/ffmpeg`. Di Vercel tidak tersedia.

> **Database** — Data di `data/xello.sqlite`. Jangan hapus folder ini! Backup berkala disarankan.

> **File Size** — Max upload 150MB per file. Cukup untuk audio panjang.

> **Vercel** — Bisa deploy tapi fitur YouTube download & SSE streaming terbatas. Disarankan Railway untuk produksi.

---

<div align="center">

**Made with 💙 by XELLO Studio**

*Build for Roblox developers, by a Roblox developer.*

</div>