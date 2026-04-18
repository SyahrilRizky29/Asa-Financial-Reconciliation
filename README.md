# Asa Financial Reconciliation (Tugas 4 - NF Academy)

Sistem otomasi rekonsiliasi keuangan menggunakan **n8n** untuk mencocokkan data transaksi internal dengan laporan mutasi bank secara otomatis. Project ini dirancang untuk memastikan integritas data finansial dengan mendeteksi selisih secara real-time.

## 🚀 Fitur Utama
- **Paralel Data Fetching:** Mengambil data dari Google Sheets (Internal) dan Google Drive (Bank CSV) secara bersamaan.
- **Auto Data Cleaning:** Standarisasi format tanggal (`YYYY-MM-DD`) dan pembersihan karakter non-numerik pada nominal menggunakan JavaScript di node `Clean Internal Data` & `Clean Bank Data`.
- **Smart Matching Logic:** Pencocokan transaksi menggunakan variabel unik `match_key` (Gabungan Tanggal + Nominal) pada node `Merge`.
- **Automated Categorization:** Mengelompokkan transaksi menjadi *Matched*, *Unrecorded Internal*, atau *Missing in Bank*.
- **Real-time Alerting:** Notifikasi otomatis via Telegram khusus untuk transaksi yang selisih/tidak cocok melalui node `Kirim Laporan Data Tidak Cocok`.

## 🛠️ Tech Stack
- **n8n** (Workflow Automation)
- **Google Sheets** (Internal Database)
- **Google Drive** (Bank Statement Storage)
- **Telegram Bot API** (Alerting System)
- **JavaScript** (Data Transformation/Cleaning)

## 📝 Deskripsi Workflow
Workflow ini membandingkan data dari Google Sheets sebagai sumber internal dan file CSV dari Google Drive sebagai sumber eksternal (Bank). 

Proses dimulai dengan:
1. **Trigger:** Menjalankan workflow secara terjadwal.
2. **Cleaning:** Node `Clean Internal Data` dan `Clean Bank Data` memastikan data sinkron sebelum dibandingkan.
3. **Reconciliation:** Node `Merge` membandingkan `match_key`.
4. **Analysis:** Node `Get Status Match` menyaring transaksi yang tidak memiliki pasangan.
5. **Reporting:** Bot Telegram mengirimkan detail transaksi yang bermasalah agar bisa segera diinvestigasi.
---
