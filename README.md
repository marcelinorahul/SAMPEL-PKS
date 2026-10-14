# SIGAP Lab

**Analisa Sampel Cair dan Padat PKS: hitung otomatis, laporan otomatis, siap kirim.**

Aplikasi web satu file untuk analis lab pabrik kelapa sawit (PKS). Input berat hasil timbangan, hasil dan status langsung muncul, laporan format WhatsApp tersusun otomatis, dan data direkap harian lengkap dengan grafik.

Tanpa instal, tanpa server. Buka di browser HP atau laptop.

---

## Fitur

| Menu | Fungsi |
|---|---|
| **Padatan** | Ripple Mill, Inti Basah, S-Claybath, LTDS I & II, F.Cyclone, Kernel Silo, Press Cake |
| **Laporan 2 Jam** | Susun laporan format WhatsApp, salin atau kirim langsung ke WA, Laporan Pintar (tempel teks, otomatis terbaca) |
| **Rekap Harian** | Grafik tren (garis/batang/area), temuan abnormal, ekspor Excel dan PDF |
| **Cairan** | Kadar Sulfit, FFA, Alkalinity M/P/H |
| **Oil Losses** | Baca laporan shift (Moist, OWM, ODM), rekap mingguan dan bulanan ke Excel |
| **USB / FLEB** | Hitung USB dan FLEB sebelum dan sesudah bunch crusher |
| **Rumus** | Uji otomatis 12 rumus dengan angka acuan |
| **Acak** (dari tab Rumus) | Alat latihan: data acak dalam rentang aman, tidak masuk rekap |

Tambahan: autosave draft di browser, riwayat koreksi (audit trail), tampilan mobile-first.

## Cara Pakai

1. Buka `index.html` di browser (atau host di mana saja, cukup file statis).
2. Tab **Padatan**: pilih titik sampling, isi berat (gram), lihat hasil dan status.
3. Tekan **Tambah ke Sesi Laporan**.
4. Tab **Laporan**: lengkapi tanggal, jam, dan data cairan/suhu, lalu **Buat Laporan 2 Jam**.
5. **Salin** atau **Kirim ke WA**, lalu **Simpan Sesi ke Rekap Harian**.
6. Lihat grafik dan ekspor di bagian **Rekap Rata-Rata Harian**.

> Alternatif cepat: tempel teks laporan WA ke **Laporan Pintar**, lalu tekan **Deteksi & Simpan ke Rekap**.

## Rumus dan Target

| Titik | Rumus | Target |
|---|---|---|
| Ripple Mill | Efisiensi = 100 − (%Nu + %Np); %BK = BK ÷ sampel × 100 | Efisiensi ≥ 98%; BK 11–12,5% |
| Inti Basah | (Nu + Np + C) ÷ sampel × 100 | ≤ 7,00% |
| S-Claybath | (Nu×0,45 + Np×0,55 + Ku + Kp) ÷ sampel × 100 | Normal 0,50–0,80%; wajib foto & lapor ≥ 0,90% |
| LTDS I / II | IP ÷ sampel × 100 | ≤ 0,10% / ≤ 0,45% |
| F.Cyclone | IP ÷ sampel × 100 per line | ≤ 0,86% |
| Kernel Silo | (Nu + Np + C) ÷ sampel × 100 | Dirt ≤ 7%; Moisture ≤ 7% |
| Sulfit | Titrasi × 0,0125 × faktor × 1000 ÷ vol. sampel | Default faktor 50, vol. 20 |
| FFA | Titrasi × 25,6 × normalitas ÷ berat sampel | Normalitas default 0,1035 |
| Alkalinity | Titrasi × 0,02 × faktor × 1000 ÷ vol. sampel | Default faktor 50, vol. 20 |
| USB / FLEB | USB = USB ÷ janjang × 100; FLEB = (brondolan × USB) ÷ (berat janjang × janjang) × 100 | - |

## Teknis

- Satu file HTML + CSS + JavaScript, tanpa build step.
- Data disimpan di `localStorage` (key `labQcPksDraftV1`).
- Library dimuat saat dibutuhkan lewat CDN: SheetJS 0.18.5 (ekspor Excel rekap), ExcelJS 4.4.0 (ekspor Oil Losses). Font dari Google Fonts.
- Integrasi WhatsApp lewat `https://wa.me/?text=`.
- Kalkulator dan laporan jalan offline; ekspor Excel dan font butuh internet.

## Keterbatasan

- Data hanya di browser perangkat. Hapus data browser berarti data hilang.
- Modul cairan lengkap (COT, CST, Sludge, Vacuum Dryer) belum selesai.
- Ambang target masih tetap di dalam kode.
- Data cairan manual belum ikut masuk ke grafik rekap bila sesi disimpan lewat jalur manual (hanya lewat Laporan Pintar).
- Ekspor Excel Oil Losses: alamat sel `C4:D4` dan `G4:H4` di header ringkasan perlu diperbaiki.

## Roadmap

1. Perbaiki bug rekap dan ekspor Oil Losses.
2. Backup dan restore data (JSON), self-host library.
3. Modul cairan lengkap, otomatis masuk Laporan 2 Jam.
4. Pengaturan target, PWA (offline penuh).
5. Opsional: sinkronisasi cloud dan multi-user.
