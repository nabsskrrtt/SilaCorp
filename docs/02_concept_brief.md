# Dokumen 2 — Concept Brief: SilaCorp

**Nama Produk:** SilaCorp (The Autonomous Virtual Office Hackathon Agency)  
**Parent Entity:** SilaLabs  
**Versi Dokumen:** 1.0.0  
**Tanggal:** 12 Oktober 2026  
**Status Gate:** Siap Direview Tim & Human Supervisor  

---

## 1. Problem Statement

Tim inovator dan peserta hackathon sering mengalami kegagalan produk (*project derailment*) karena tiga hal:
1. Terjebak dalam kelelahan mikromanajemen AI di banyak platform terpisah tanpa kontinuitas konteks (*AI prompt fatigue*).
2. Tidak adanya mitra debat kritis (*opposition*) yang menguji kelayakan ide terhadap kriteria juri (*the yes-man hallucination trap*).
3. Terputusnya rantai kerja antara perumusan konsep, penulisan kode, pengetesan, dan materi presentasi menjelang batas akhir pengumpulan (*disjointed PDCA cycle*).

---

## 2. Persona Target Pengguna Utama

### Persona Utama: "Rian — The Hackathon Lead & Builder"
* **Demografi:** Usia 20–28 tahun, Software Engineer / Mahasiswa Teknik / Product Builder.
* **Tujuan:** Memenangkan kompetisi inovasi atau hackathon bergengsi dengan menghasilkan produk fungsional, berdampak nyata, dan presentasi yang memikat dewan juri dalam waktu <48 jam.
* **Pain Point:**
  * Waktu habis untuk bolak-balik prompt AI dan memperbaiki integrasi kode yang tidak sinkron di menit-menit akhir.
  * Sering bingung membagi prioritas fitur (mana P0 wajib, mana P2 yang bisa dibuang).
  * Sulit melihat gambaran besar progres ketika rekan tim atau AI bekerja di silo terpisah.

---

## 3. Value Proposition

> **"SilaCorp mengubah ide mentah atau tema hackathon menjadi produk MVP fungsional, spesifikasi teknis presisi, dan submission kit siap juri melalui agensi virtual multi-agen yang saling berkolaborasi, berdebat secara kritis, dan disupervisi langsung oleh pengguna."**

### Tiga Nilai Pembeda Inti:
1. **The Opposition Principle (Judge Agent):** Setiap ide diuji oleh agen oposisi yang bertindak sebagai juri galak, memastikan solusi relevan dengan rubric lomba dan tidak overscoped.
2. **Interactive Virtual Office Canvas:** Interaksi agen divisualisasikan dalam bentuk ruang kantor dinamis—pengguna melihat agen berpindah meja, berdiskusi, dan mengantarkan dokumen secara spatial.
3. **Executive Escalation Hierarchy:** Manusia tidak lagi menjadi kuli prompt; manusia duduk sebagai *Board of Directors / CEO* yang hanya memvalidasi keputusan strategis di tiap *Checkpoint Gate*.

---

## 4. Solusi yang Dipilih vs. Alternatif yang Ditolak

```
                          ┌────────────────────────┐
                          │   HUMAN SUPERVISOR     │
                          │   (Executive Board)    │
                          └───────────┬────────────┘
                                      │ (Gate Approvals & Veto)
                          ┌───────────▼────────────┐
                          │   MANAGING DIRECTOR    │
                          │   (Chief Orchestrator) │
                          └─────┬──────┬─────┬─────┘
           ┌────────────────────┘      │     └────────────────────┐
           ▼                           ▼                          ▼
   ┌──────────────┐             ┌──────────────┐           ┌──────────────┐
   │ RESEARCH DESK│◄───────────►│ PRODUCT DESK │◄─────────►│ ARCHITECT &  │
   │ (Market/Data)│             │ (PM Agent)   │           │ BUILDER DESK │
   └──────┬───────┘             └──────┬───────┘           └──────┬───────┘
          │                            │                          │
          └─────────────────────┐      │      ┌───────────────────┘
                                ▼      ▼      ▼
                          ┌────────────────────────┐
                          │      JUDGE DESK        │
                          │  (The Opposition/QA)   │
                          └────────────────────────┘
```

| Pendekatan | Status | Alasan Pemilihan / Penolakan |
| :--- | :--- | :--- |
| **Multi-Agent Virtual Office dengan Oposisi & Human Checkpoint** | **DIPILIH** | Menjaga kontrol kualitas tinggi, mencegah halusinasi, memberikan transparansi visual, dan menjaga arah produk tetap sejalan dengan visi pengguna. |
| **Single-Agent Megaprompt (Chatbot Konvensional)** | **DITOLAK** | Konteks cepat hilang (*context degradation*), tidak ada pemisahan domain keahlian, dan pengguna lelah mengetik instruksi berulang. |
| **Full Autonomous Blackbox (Tanpa Pengawasan Manusia)** | **DITOLAK** | Menghasilkan produk yang sering keluar jalur dari intensi awal pengguna; tanpa intervensi manusia, risiko kegagalan di hadapan juri sangat tinggi. |
| **Dashboard Tabel Standar (Plain Kanban Board)** | **DITOLAK** | Kering dan membosankan; tidak memberikan *spatial awareness* atas interaksi antar-agen dan minim *wow-factor* saat dipresentasikan. |

---

## 5. Skenario Penggunaan Utama (The Golden Journey)

1. **Inisiasi Proyek (Hour 0):**
   * Rian membuka Web App SilaCorp, memasukkan input: Tema: *"Sustainable Smart Logistics"* + Rubric Penilaian Juri + Batas Waktu 24 Jam.
2. **Fase Perencanaan & Debat (Plan):**
   * Managing Director memanggil **Researcher Agent**. Agen bergerak ke *Research Desk* mengumpulkan problem space dan kompetitor (Dokumen 1).
   * **Product Lead Agent** menerima riset, berjalan ke mejanya merancang konsep (Dokumen 2) dan Lean PRD (Dokumen 3).
   * **Judge Agent** berjalan ke meja Product Lead, memberikan penolakan: *"Fitur tracking IoT terlalu mahal dan tidak realistis dibangun dalam 24 jam; fokus ke algoritma dynamic rerouting berbasis GPS smartphone."*
   * Product Lead merevisi fitur P0. Sistem memunculkan dialog eskalasi ke Rian (Human Board) untuk meminta persetujuan.
   * Rian menekan tombol **"Approve Gate 2 & 3"**.
3. **Fase Arsitektur & Pembangunan (Do):**
   * **Architect Agent** memetakan Dokumen 4 & 5 (Tech Design & Task Plan).
   * **Code Builders (Frontend & Backend Agents)** mulai mengeksekusi kode modular secara paralel.
4. **Fase Pengujian & Pemolesan (Check & Act):**
   * Judge Agent dan QA Agent memvalidasi fungsionalitas dan kesesuaian rubric.
   * **Pitch Agent** merangkum output menjadi outline slide presentasi dan naskah demo video 3 menit.
5. **Final Submission:**
   * Rian mengunduh repositori kode lengkap yang siap jalan dan dokumen presentasi utuh.

---

## 6. Definisi Sukses & Keunggulan Produk

### Metrik Keberhasilan MVP
* **Time-to-Blueprint:** Siklus Dokumen 1 hingga Dokumen 5 terselesaikan dalam waktu <15 menit interaksi terarah.
* **Zero Disconnected Code:** 100% kode yang di-generate memiliki rujukan langsung ke fitur P0 di Dokumen 3a (Traceability Matrix).
* **Judge Stress-Test Pass:** Setiap solusi telah melalui minimal 1 putaran kritik tajam dari Judge Agent dan disetujui Human Board.

### Keunggulan Kompetitif SilaCorp
1. **Psychological Reality Check:** Menyelamatkan tim dari bias optimisme yang berlebihan melalui Judge Agent.
2. **Visual Engagement:** Visualisasi kantor virtual yang membuat proses kolaborasi AI terasa hidup dan mudah dipantau oleh siapa saja.
3. **Submission-Ready Outputs:** Menghasilkan paket artefak lengkap standar industri, bukan sekadar potongan skrip kode.

---

## 7. Gate Status: Dokumen 2 — Concept Brief

> **Gate Criteria:** Semua anggota tim bisa menjelaskan produk dalam satu kalimat yang sama.  
>  
> **Kalimat Konsensus:**  
> *"SilaCorp adalah agensi virtual multi-agen berwujud kantor simulasi interaktif yang mengotomasi seluruh siklus PDCA hackathon—mulai dari riset, validasi oposisi juri, spesifikasi sistem, kode MVP, hingga materi pitch—di bawah kendali strategis manusia."*  
>  
> **Status Gate: PASSED / SIAP LANJUT KE DOKUMEN 3 (Lean PRD).**
