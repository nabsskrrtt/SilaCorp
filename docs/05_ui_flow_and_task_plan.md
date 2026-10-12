# Dokumen 5 — UI Flow + Task Plan: SilaCorp

**Nama Produk:** SilaCorp (The Autonomous Virtual Office Hackathon Agency)  
**Parent Entity:** SilaLabs  
**Versi Dokumen:** 1.0.0  
**Tanggal:** 12 Oktober 2026  
**Status Gate:** Siap Direview Tim & Siap Masuk Eksekusi Teknis  

---

## 1. Screen Map & Urutan Interaksi Pengguna

```
┌────────────────────────────────────────────────────────┐
│  SCREEN 1: SPRINT LAUNCHPAD & REPO SEEDER (/)          │
│  • Daftar sprint aktif & tombol "+ Start New Sprint"   │
└───────────────────────────┬────────────────────────────┘
                            │ Klik Start
┌───────────────────────────▼────────────────────────────┐
│  MODAL 1: INTAKE & RUBRIC CONFIGURATOR                 │
│  • Form tema, problem awal, & bobot rubric (F01)       │
└───────────────────────────┬────────────────────────────┘
                            │ Validasi Submit
┌───────────────────────────▼────────────────────────────┐
│  SCREEN 2: VIRTUAL OFFICE WORKSPACE (/sprint/:id)      │
│  ┌──────────────────────────────────────────────────┐  │
│  │ TOP BAR: Status PDCA, Phase Badge, Veto Button   │  │
│  ├──────────────────────────────────────────────────┤  │
│  │ CENTER: 2D Office Canvas (Meja & Mobilisasi Agen)│  │
│  ├──────────────────────────────────────────────────┤  │
│  │ BOTTOM: Real-time Live Thought Stream            │  │
│  ├──────────────────────────────────────────────────┤  │
│  │ RIGHT: Collapsible Markdown Artifact Viewer      │  │
│  └────────────────────────┬─────────────────────────┘  │
└───────────────────────────┼────────────────────────────┘
                            │ Memicu Checkpoint Gate
┌───────────────────────────▼────────────────────────────┐
│  MODAL 2: HUMAN BOARD GATEKEEPER MODAL                 │
│  • Side-by-Side: Draf Dokumen vs Catatan Juri (F05)    │
│  • Aksi: Approve / Request Revision / Direct Veto      │
└───────────────────────────┬────────────────────────────┘
                            │ Semua Gate 1-5 Lolos
┌───────────────────────────▼────────────────────────────┐
│  SCREEN 3: SUBMISSION PORTAL (/sprint/:id/export)      │
│  • Unduh ZIP Submission Kit, Slide Pitch, & Kode Repo  │
└────────────────────────────────────────────────────────┘
```

---

## 2. Penanganan Visual States (Loading, Empty, Success, Error)

| Kondisi State | Indikator Visual Antarmuka | Aksi Sistem & Umpan Balik |
| :--- | :--- | :--- |
| **Empty State** | Denah kantor dalam mode temaram (*night ambient*), lampu meja mati, ada teks panduan: *"Lantai kantor siap. Masukkan tema untuk memanggil tim agen SilaCorp."* | Menyorot tombol utama "+ Start Innovation Sprint" dengan animasi pulsing lembut. |
| **Working / Thinking** | Lampu di atas meja bersangkutan menyala terang; avatar agen menampilkan balon animasi berpikir (*typing dots bubble*). | Token pikiran dialirkan secara langsung (*streaming*) ke panel *Live Thought Stream*. |
| **Gate Awaiting Approval** | Meja Board Room di tengah atas berkedip dengan lampu aksen emas (*golden spotlight*); muncul lencana lonceng di header. | Membuka *Gate Decision Modal* secara elegan tanpa menutup latar kanvas kantor. |
| **Success State** | Efek stempel digital timbul bersuara *"APPROVED"*; confetti halus di sekitar meja terkait; avatar agen melakukan gestur tos (*high-five*). | Status bar beralih ke warna hijau, membuka kunci akses dokumen di panel samping. |
| **Error / Network Drop** | Avatar agen menampilkan tanda seru kuning di atas kepala; status badge bertuliskan *"Reconnecting to SilaCorp HQ..."*. | Sistem mencoba menyambung ulang otomatis di latar belakang; menyediakan tombol cadangan *"Retry Agent Task"*. |

---

## 3. Pembagian Task yang Bisa Dikerjakan Paralel

Pengembangan MVP SilaCorp dibagi ke dalam 3 Jalur Paralel (*Tracks*) yang saling terhubung melalui kontrak teknis di [Dokumen 4](file:///c:/Users/ASUS/Documents/GROW/Agency/docs/04_technical_design.md):

```
                       ┌─────────────────────────┐
                       │   T00: Project Setup    │
                       │   & Type Definitions    │
                       └────────────┬────────────┘
            ┌───────────────────────┼───────────────────────┐
            ▼                       ▼                       ▼
┌───────────────────────┐┌───────────────────────┐┌───────────────────────┐
│ TRACK A: FRONTEND &   ││ TRACK B: STATE ENGINE ││ TRACK C: PROMPT &     │
│ VIRTUAL CANVAS        ││ & BACKEND API         ││ OPPOSITION LOGIC      │
│ • T01: Office Grid &  ││ • T04: State Machine  ││ • T07: Prompt Engine  │
│   Desk Stations       ││   & PDCA Transitions  ││   (Docs 1–5 Prompts)  │
│ • T02: Sprite Movement││ • T05: REST API & SSE ││ • T08: The Opposition│
│   & Path Easing       ││   Event Streaming Hub ││   Judge Logic & Score │
│ • T03: Gatekeeper     ││ • T06: Persistence &  ││ • T09: Context Window │
│   Modal & Viewer      ││   ZIP Packaging Engine││   Digest Compressor   │
└───────────┬───────────┘└───────────┬───────────┘└───────────┬───────────┘
            └───────────────────────┼───────────────────────┘
                                    ▼
                       ┌─────────────────────────┐
                       │ T10: System Integration │
                       │ & End-to-End Validation │
                       └─────────────────────────┘
```

---

## 4. Matriks Dependensi Antartask & Estimasi

| Kode Task | Deskripsi Pekerjaan | Dependensi | Estimasi | PIC |
| :--- | :--- | :--- | :--- | :--- |
| **T00** | Setup repositori, Tailwind/Vanilla CSS tokens, & kontrak TypeScript (Doc 4). | Tidak ada | 1 Jam | Fullstack Lead |
| **T01** | Bangun komponen `OfficeCanvas`, denah meja 2D, dan visual ambient lighting. | T00 | 2.5 Jam | Frontend Dev |
| **T02** | Implementasi sistem pergerakan sprite avatar agen antar meja dengan interpolasi. | T01 | 2 Jam | Frontend Dev |
| **T03** | Bangun `GateDecisionModal` (side-by-side) dan `ArtifactViewer` markdown renderer. | T00 | 2 Jam | Frontend Dev |
| **T04** | Bangun mesin keadaan deterministik (*State Machine*) untuk siklus PDCA. | T00 | 2 Jam | Backend Dev |
| **T05** | Bangun endpoint REST inisiasi proyek dan SSE event hub untuk streaming data. | T04 | 2 Jam | Backend Dev |
| **T06** | Bangun layanan penyimpanan persistent (SQLite/Store) dan bundler arsip ZIP. | T04 | 1.5 Jam | Backend Dev |
| **T07** | Susun prompt sistem spesialis (Researcher, PM, Architect) sesuai standar Dokumen 1–5. | T00 | 2.5 Jam | AI Engineer |
| **T08** | Implementasi prompt *Judge Agent (The Opposition)* dengan rubric benchmarking. | T07 | 2 Jam | AI Engineer |
| **T09** | Bangun pembuat ringkasan sari keputusan (*Executive Digest Compressor*). | T07 | 1.5 Jam | AI Engineer |
| **T10** | Integrasi utuh: Sinkronisasi Canvas + SSE Stream + Gatekeeper + Export E2E. | T02, T03, T05, T08 | 3 Jam | Seluruh Tim |

---

## 5. Definition of Done (DoD)

Sebuah modul atau fitur dinyatakan **SELESAI (DONE)** jika memenuhi kriteria absolut berikut:
1. **Zero Guesswork Integration:** Menggunakan kontrak tipe data TypeScript yang didefinisikan di Dokumen 4 tanpa `any` type sembarangan.
2. **Visual Smoothness:** Kanvas kantor 2D berjalan mulus pada 60 FPS tanpa jeda patah-patah saat animasi sprite berpindah meja.
3. **Deterministic Gate Enforcement:** Fase selanjutnya mustahil terbuka jika state persetujuan gate belum bernilai `APPROVED`.
4. **Resilient Failure Recovery:** Ketika koneksi terputus atau API LLM mengalami timeout, sistem tidak crash dan mampu memulihkan state dari penyimpanan lokal.
5. **Traceable Artifacts:** Seluruh dokumen 1–5 yang diekspor berformat markdown rapi dan memenuhi seluruh kriteria isi di [needed.md](file:///c:/Users/ASUS/Documents/GROW/Agency/needed.md).

---

## 6. Pembagian Peran & Tanggung Jawab (PIC)

* **Lead Architect & AI Orchestrator (PIC: AI & Backend Lead):**
  * Bertanggung jawab atas mesin PDCA, stabilitas prompt LLM, integrasi Judge Agent, dan keamanan context window.
* **UI/UX & Interactive Canvas Specialist (PIC: Frontend Lead):**
  * Bertanggung jawab atas estetika visual kantor virtual SilaCorp, responsivitas denah, kehalusan animasi sprite, dan kenyamanan modal persetujuan.
* **Product Quality & Rubric Compliance Officer (PIC: QA & Product Lead):**
  * Bertanggung jawab memvalidasi bahwa sistem benar-benar mampu mengonversi input tema apa pun menjadi paket inovasi yang bernilai tinggi di hadapan juri hackathon.

---

## 7. Gate Status: Dokumen 5 — UI Flow + Task Plan

> **Gate Criteria:** Tim tahu persis apa yang dikerjakan, siapa yang mengerjakan, dan bagaimana hasilnya diperiksa.  
>  
> **Verifikasi Kesiapan Eksekusi:**  
> [x] Screen map dan alur antar-layar telah dipetakan lengkap.  
> [x] Penanganan 5 visual state (Empty, Thinking, Awaiting, Success, Error) terdefinisi.  
> [x] Rencana task paralel dan urutan dependensi jelas.  
> [x] Definition of Done (DoD) terukur secara objektif.  
> [x] PIC dan penanggung jawab per modul telah dialokasikan.  
>  
> **Status Gate: PASSED / SELURUH RANGKAIAN DOKUMEN 1–5 RESMI LENGKAP & SIAP IMPLEMENTASI!**
