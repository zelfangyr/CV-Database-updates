# CV-Database-updates

Repo publik ini **bukan source code aplikasi** — isinya cuma `version.json`, dipakai sebagai feed pengecekan update otomatis oleh aplikasi [CV-Database](https://github.com/zelfangyr/CV-Database).

Setiap kali aplikasi CV Database dibuka, ia membaca `version.json` di repo ini (tanpa perlu token/API GitHub) untuk tahu apakah ada versi lebih baru yang tersedia. Kalau ada, muncul banner notifikasi di aplikasi dengan link download.

## Cara kerja

1. `version.json` berisi nomor versi terbaru, link halaman rilis, link download langsung, dan catatan singkat perubahan.
2. File `.zip` hasil build aplikasi (PyInstaller) diupload sebagai asset di **GitHub Release** repo ini, dengan tag mengikuti pola `Vx.y.z` (mis. `V1.4.0`).
3. `download_url` di `version.json` menunjuk langsung ke asset zip tersebut.

## Rilis update baru (checklist)

1. Build aplikasi: `pyinstaller CV_Database.spec --clean`, lalu zip folder `dist/CV_Database` jadi `CV_Database.zip`.
2. Buat GitHub Release baru di repo ini dengan tag `Vx.y.z`, upload `CV_Database.zip` sebagai asset.
3. Update `version.json`:
   - `latest_version`: nomor versi baru (mis. `"1.4.0"`)
   - `release_url`: link halaman release di atas
   - `download_url`: link download langsung asset zip
   - `notes`: ringkasan singkat perubahan
4. Commit & push.

## Versi saat ini

**v1.4.1** — Bug fix: pastikan dependency (pdfplumber, dkk) ter-bundle dengan benar saat build PyInstaller, sehingga fitur baca PDF tidak error di aplikasi hasil release.

### Riwayat versi
- **1.4.1** — Bug fix: dependency PDF (pdfplumber, dkk) ter-bundle dengan benar saat build, fitur baca PDF tidak error lagi di exe.
- **1.4.0** — Redesign Dashboard CV (KPI cards, donut chart, filter tahun); tombol Import dari Excel (sync ke database, data lama tidak terhapus).
- **1.3.0** — Preview CV di halaman, tab Dashboard CV, kolom Tanggal & Jam Simpan, validasi field wajib.
- **1.2.0** — Cek update otomatis, lokasi data persisten di `%APPDATA%`, dropdown Tim & Tahun, pagination.
- **1.1.0** — Fallback OCR, sorting & filter tabel, export ke Excel.
- **1.0.0** — Rilis awal.
