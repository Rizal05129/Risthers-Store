# Cara Deploy Risthers Store ke GitHub Pages

Website ini sudah diubah supaya bisa jalan sebagai situs statis (tanpa server/database), jadi bisa langsung di-host gratis di GitHub Pages dan langsung dapat link publik.

## Langkah-langkah

1. **Buat repository baru di GitHub**
   - Buka https://github.com/new
   - Beri nama repo, misalnya `risthers-store`
   - Pilih **Public**, lalu klik **Create repository**

2. **Upload semua file project ini ke repo tersebut**
   - Bisa lewat GitHub Desktop, atau lewat terminal:
     ```bash
     git init
     git add .
     git commit -m "Initial commit"
     git branch -M main
     git remote add origin https://github.com/USERNAME/risthers-store.git
     git push -u origin main
     ```
     (ganti `USERNAME` dan nama repo sesuai punya kamu)

3. **Aktifkan GitHub Pages**
   - Di repo, buka tab **Settings** → **Pages**
   - Pada bagian **Build and deployment** → **Source**, pilih **GitHub Actions**
   - Selesai — tidak perlu setting lain

4. **Tunggu proses deploy**
   - Buka tab **Actions** di repo, akan ada workflow "Deploy to GitHub Pages" berjalan otomatis
   - Setelah selesai (tanda centang hijau), buka lagi **Settings → Pages** — link situsnya akan muncul di bagian atas, formatnya:
     ```
     https://USERNAME.github.io/risthers-store/
     ```

5. **Update otomatis**
   - Setiap kali kamu push perubahan baru ke branch `main`, situs akan otomatis ter-build ulang dan ter-deploy oleh GitHub Actions (file workflow-nya ada di `.github/workflows/deploy.yml`).

## Yang berubah agar bisa jadi situs statis

- Data produk sekarang disimpan langsung di `client/src/data/products.ts` (tidak perlu database/server lagi). Kalau mau tambah/ubah produk, edit file ini.
- Routing halaman (`/products`, `/product/1`, dll) diubah pakai hash routing (`#/products`) supaya tetap berfungsi di GitHub Pages, karena GitHub Pages tidak mendukung server-side routing.
- Build hanya untuk bagian client (`npm run build:pages`), folder `server/` tidak dipakai untuk deploy ini.

## Catatan

- Folder `server/` dan `drizzle.config.ts` masih ada di project ini kalau nanti kamu mau deploy versi full dengan database di platform lain (Railway, Render, VPS, dll) — tidak mengganggu proses build statis di atas.
- Kalau ingin custom domain, tambahkan file `client/public/CNAME` berisi domain kamu, lalu atur DNS domain ke GitHub Pages.
