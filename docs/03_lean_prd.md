# Dokumen 3 — Lean PRD: SilaCorp

**Nama Produk:** SilaCorp (The Autonomous Virtual Office Hackathon Agency)  
**Parent Entity:** SilaLabs  
**Versi Dokumen:** 1.0.0  
**Tanggal:** 12 Oktober 2026  
**Status Gate:** Siap Direview Tim & Human Supervisor  

---

## 1. Tujuan Produk & Non-Goals

### Tujuan (Goals)
1. Menyediakan platform web terpadu yang mampu mengorkestrasi siklus PDCA inovasi hackathon secara terstruktur dari ide mentah hingga deliverable siap juri.
2. Memvisualisasikan kolaborasi multi-agen secara spatial dalam bentuk antarmuka *Virtual Office 2D* yang dinamis dan informatif.
3. Mengintegrasikan mekanisme debat kritis melalui *Judge Agent* dan menjaga kendali strategis melalui sistem persetujuan bertingkat (*Human Board Checkpoint Gate*).
4. Menghasilkan artefak standar industri yang konsisten: Dokumen 1–5 ([needed.md](file:///c:/Users/ASUS/Documents/GROW/Agency/needed.md)), blueprint arsitektur, dan paket persiapan pitch.

### Batasan Luar (Non-Goals untuk MVP)
1. **Bukan 3D Heavy Game Engine:** MVP tidak menggunakan WebGL/3D berat yang membebani browser; tampilan kantor dibuat menggunakan kanvas 2D/isometric sprite modern yang ringan, cepat dimuat, dan responsif.
2. **Tidak Melakukan Auto-Payment / Deployment Berbayar Tanpa Izin:** MVP tidak langsung men-deploy ke server cloud komersial tanpa persetujuan eksplisit; MVP berfokus menghasilkan kode runnable lokal dan artefak terverifikasi.
3. **Bukan Chatbot Percakapan Bebas (Unbounded Free Chat):** Sistem tidak dirancang untuk obrolan santai tanpa tujuan; setiap pertukaran pesan antar agen terikat pada tugas menghasilkan artefak dan meloloskan gate.

---

## 2. Prioritisasi Fitur (P0, P1, P2)

### Fitur P0 (Wajib Ada di MVP)
* **F01 — Innovation Intake & Rubric Configurator:** Form inisiasi proyek untuk memasukkan nama proyek, tema hackathon, problem statement awal, dan kriteria penilaian juri (rubric weight).
* **F02 — Virtual Office 2D Canvas & Agent Mobilization:** Kanvas visual denah kantor dengan meja-meja departemen (Director, Research, Product, Architecture, Judge, Board Room). Agen divisualisasikan bergerak antar meja saat terjadi handoff tugas.
* **F03 — Autonomous PDCA Multi-Agent Pipeline:** State engine yang mengatur alur kerja sekuensial dan paralel antar agen untuk menyusun Dokumen 1 hingga Dokumen 5.
* **F04 — The Opposition Engine (Judge Agent):** Modul penilaian independen yang menguji setiap dokumen terhadap kriteria rubric hackathon dan memberikan catatan tajam sebelum dokumen diajukan ke manusia.
* **F05 — Human Board Gatekeeper Modal:** Antarmuka verifikasi checkpoint di setiap akhir fase dokumen (Gate 1 sampai 5) dengan aksi: *Approve & Continue*, *Request Revision*, atau *Direct Directive (Veto)*.
* **F06 — Real-time Artifact Viewer & Workspace Export:** Panel pembaca markdown langsung dengan tab dokumen (1–5) serta tombol ekspor bundel proyek ke file ZIP/Markdown.

### Fitur P1 (Jika Sempat / Sprint Lanjutan)
* **F07 — Pitch Deck & Script Generator:** Generator otomatis outline slide presentasi dan naskah pitch 3 menit berdasarkan dokumen yang telah disetujui.
* **F08 — Office Soundscapes & Haptic Feedback:** Efek suara retro ketikan, lonceng notifikasi eskalasi, dan suara langkah kaki agen saat berpindah meja.
* **F09 — Direct GitHub Sync:** Otomasi commit dan push seluruh artefak ke repositori GitHub pribadi pengguna.

### Fitur P2 (Diabaikan untuk MVP Awal)
* **F10 — Virtual Office Customizer:** Kustomisasi layout ruangan, wallpaper, dan skin karakter agen.
* **F11 — Multi-Human Multiplayer Room:** Kolaborasi real-time banyak pengguna manusia dalam satu kantor virtual.
* **F12 — Auto-Submission Bot:** Integrasi bot pengiriman otomatis ke portal Devpost atau platform hackathon eksternal.

---

## 3. User Stories

| ID | As a... | I want to... | So that... |
| :--- | :--- | :--- | :--- |
| **US-01** | Hackathon Lead | Memasukkan tema, panduan lomba, dan bobot rubric juri di awal sesi | Agen memiliki referensi baku dalam memvalidasi relevansi produk. |
| **US-02** | User | Melihat agen-agen bekerja dan berpindah meja di kanvas kantor secara real-time | Saya memahami siapa yang sedang mengerjakan apa tanpa kebingungan membaca log teks mentah. |
| **US-03** | User | Mendapatkan hasil review kritis dari Judge Agent sebelum menandatangani gate | Saya terhindar dari bias ide yang tidak realistis dan tahu kelemahan produk sebelum juri asli melihatnya. |
| **US-04** | User / Board | Menerima notifikasi eskalasi ketika agen menemui kebuntuan atau butuh persetujuan arah produk | Saya memegang kendali penuh atas keputusan bisnis dan visi produk. |
| **US-05** | Developer | Mengunduh paket dokumen dan blueprint arsitektur yang sudah terstruktur | Tim saya bisa langsung mengeksekusi implementasi dengan kontrak data yang jelas. |

---

## 4. Acceptance Criteria (Bisa Dites Secara Objektif)

### Skenario AC-01: Inisiasi Proyek & Mobilisasi Awal
* **Given:** Pengguna berada di halaman utama SilaCorp dan mengisi form proyek (Tema: "AI Accessibility", Rubric: "Impact 40%, Tech 30%, UX 30%").
* **When:** Pengguna menekan tombol "Start Innovation Sprint".
* **Then:** State proyek berubah menjadi `PLANNING_RESEARCH`, avatar Managing Director memanggil avatar Researcher, dan avatar Researcher bergerak menuju *Research Desk* disertai status visual *"Investigating Problem Space..."*.

### Skenario AC-02: Evaluasi Oposisi oleh Judge Agent
* **Given:** PM Agent selesai menyusun draf Dokumen 2 (Concept Brief).
* **When:** Draf diserahkan ke pipeline verifikasi internal.
* **Then:** Avatar Judge Agent bergerak ke meja PM, status berubah menjadi *"Auditing Against Hackathon Rubric"*, dan sistem menghasilkan dokumen evaluasi berisi skor rubric serta minimal 2 kritik/tantangan terhadap asumsi produk.

### Skenario AC-03: Human Board Gate Approval & Rejection
* **Given:** Dokumen dan laporan Judge siap untuk diperiksa pada Gate Checkpoint.
* **When:** Modal persetujuan muncul di layar pengguna:
  * Jika pengguna klik **"Approve"**: State gate tersimpan sebagai `APPROVED`, kanvas membuka kunci fase berikutnya, dan agen fase berikutnya mulai bergerak.
  * Jika pengguna klik **"Request Revision"** dengan catatan tambahan: Status kembali ke agen pembuat dengan instruksi revisi yang terlampir.

### Skenario AC-04: Ekspor Artefak
* **Given:** Pengguna telah meloloskan minimal Gate 1 hingga 5.
* **When:** Pengguna menekan tombol "Export All Deliverables".
* **Then:** Sistem mengunduh arsip file yang berisi seluruh dokumen markdown (01–05) dengan struktur folder yang rapi dan metadata yang lengkap.

---

## 5. User Flow & Penanganan Error States

### Diagram User Flow Utama:
```
[User Input Tema & Rubric]
          │
          ▼
[Managing Director Delegasi Tugas]
          │
          ▼
[Spesialis Menyusun Draf Dokumen] ◄──────┐ (Revisi)
          │                             │
          ▼                             │
[Judge Agent Menilai & Mengkritik]      │
          │                             │
          ▼                             │
[Human Checkpoint Gate Modal] ──────────┘
          │ (Approved)
          ▼
[Buka Gate Berikutnya / Lanjut ke Fase Eksekusi]
```

### Penanganan Error States (Resilience):
1. **LLM API Timeout / Rate Limit:**
   * Agen menampilkan status visual *"Reconnecting to HQ..."* (ikon sinyal berkedip kuning).
   * Sistem otomatis mencoba ulang dengan mekanisme exponential backoff (hingga 3 kali) dan fallback ke model alternatif yang setara tanpa merusak sesi pengguna.
2. **Infinite Debate Loop:**
   * Jika agen spesialis dan Judge Agent berdebat lebih dari 2 putaran tanpa konsensus, Managing Director otomatis menghentikan perdebatan dan mengeskalasikan kedua opsi solusi ke Human Supervisor untuk divoting.
3. **Mati Lampu / Browser Refresh:**
   * Seluruh state agen, riwayat percakapan, dan dokumen tersimpan secara reaktif di *LocalStorage / Persistent Database Store*, sehingga pengguna dapat melanjutkan sesi tepat di checkpoint terakhir.

---

## 6. Constraint Hackathon & Batasan MVP

* **Batas Waktu Eksekusi Agen:** Tiap tahapan pembuatan dokumen dibatasi maksimal 120 detik agar pengguna tidak menunggu terlalu lama.
* **Kebutuhan Resource Minimal:** Aplikasi harus berjalan lancar di browser modern standar (Chrome, Firefox, Edge) tanpa memerlukan GPU khusus di sisi client.
* **Format Output Baku:** Seluruh dokumen yang dihasilkan wajib mengikuti format baku struktur [needed.md](file:///c:/Users/ASUS/Documents/GROW/Agency/needed.md).

---

## 7. Gate Status: Dokumen 3 — Lean PRD

> **Gate Criteria:** Setiap fitur P0 punya perilaku yang jelas dan bisa diverifikasi.  
>  
> **Verifikasi Fitur P0:**  
> [x] F01 Intake Configurator: Input jelas, trigger valid.  
> [x] F02 Virtual Office Canvas: State visual spatial dan animasi mobilisasi terdefinisi.  
> [x] F03 Multi-Agent Pipeline: Alur transisi antar-tahap jelas.  
> [x] F04 Opposition Engine: Kriteria review dan scoring rubric terukur.  
> [x] F05 Human Board Modal: Pilihan aksi Approve/Revise/Veto jelas.  
> [x] F06 Artifact Viewer: Format markdown terstandarisasi.  
>  
> **Status Gate: PASSED / SIAP LANJUT KE DOKUMEN 3a (Feature Breakdown).**
