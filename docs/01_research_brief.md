# Dokumen 1 — Research Brief: SilaCorp

**Nama Proyek:** SilaCorp (The Autonomous Virtual Office Hackathon Agency)  
**Parent Entity:** SilaLabs  
**Versi Dokumen:** 1.0.0  
**Tanggal:** 12 Oktober 2026  
**Status Gate:** Siap Direview Tim & Human Supervisor  

---

## 1. Problem Statement & Target User

### Problem Utama
Mengikuti kompetisi inovasi atau hackathon (24–72 jam) adalah arena bertekanan tinggi dengan tingkat kegagalan proyek (incomplete submission) mencapai lebih dari 60%. Masalah mendasar yang dialami tim hackathon modern bukan lagi ketiadaan AI, melainkan:

1. **AI Prompt Fatigue & Disjointed Context:** Pengguna kelelahan memandu AI secara mikromanajemen melalui puluhan tab terpisah (ChatGPT untuk ideasi, Cursor/v0 untuk frontend, Claude untuk PRD, Canva untuk slide). Konteks produk tercecer, tidak sinkron, dan inkonsisten.
2. **Ketiadaan Oposisi & Ilusi Validitas (The Hallucination Trap):** Tim sering terburu-buru coding (*vibe coding*) fitur yang tampak keren namun tidak menjawab rubric penilaian juri, tidak memiliki problem-solution fit yang valid, atau overscoped hingga gagal diselesaikan tepat waktu.
3. **Ketiadaan Orkestrasi PDCA Terstruktur:** Tidak ada jembatan otomatis antara *Plan* (Research, PRD, Tech Design), *Do* (Coding & Generation), *Check* (Rubric Testing & QA), dan *Act* (Eskalasi & Refinement).

### Target User Persona
* **Hackathon Warriors & Solo Builders:** Developer atau kreator independen yang ingin membangun proyek hackathon berkualitas tim penuh dalam waktu singkat.
* **Cross-functional Innovation Teams (Hacker, Hipster, Hustler):** Tim mahasiswa atau profesional yang membutuhkan sinkronisasi cepat antara konsep bisnis, antarmuka, dan backend.
* **Corporate & University Innovation Sprints:** Tim internal yang mengikuti lomba inovasi tahunan dan membutuhkan metodologi terstruktur untuk menghasilkan deliverable lengkap.

---

## 2. Bukti & Validasi Masalah (Evidence of Problem)

* **Hackathon Drop-out Rate:** Data empiris penyelenggara hackathon global (seperti Devpost, ETHGlobal, hackathon korporat) menunjukkan bahwa 40–60% tim yang mendaftar gagal mengumpulkan submission fungsional di hari penutupan. Sebagian besar berhenti karena kehabisan waktu di fase integrasi backend-frontend atau tidak sempat membuat demo video dan pitch deck.
* **Cognitive Overload pada AI Prompting:** Penelitian human-AI interaction menunjukkan bahwa memandu *single-agent LLM* secara manual untuk proyek multi-tahap menimbulkan *context drift*—di mana AI di tahap akhir melupakan batasan non-goals yang telah ditetapkan di tahap awal.
* **Rubric Mismatch:** Mayoritas tim kalah bukan karena kode yang jelek, melainkan karena solusi mereka tidak menjawab kriteria bobot juri (misal: bobot *Market Feasibility* 40%, namun tim menghabiskan 90% waktu mengutak-atik animasi UI tanpa bukti validasi masalah).

---

## 3. Analisis Solusi & Kompetitor yang Tersedia

| Solusi / Platform | Karakteristik Utama | Kelemahan Fatal dalam Konteks Hackathon |
| :--- | :--- | :--- |
| **General AI Chatbots**<br>*(ChatGPT, Claude, Gemini)* | Percakapan reaktif single-turn atau multi-turn berbasis prompt manual. | Tidak memiliki konsep state persisten, tidak ada alur kerja PDCA otomatis, pengguna harus bertindak sebagai operator penuh tanpa henti. |
| **Agent Frameworks**<br>*(CrewAI, AutoGen, MetaGPT)* | Framework multi-agent berbasis Python/kode untuk eksekusi task otonom. | Sangat teknis (CLI-heavy), tidak punya visualisasi human-friendly (seperti kantor virtual), tidak memiliki domain logic khusus kriteria hackathon (Rubric Judge). |
| **Autonomous Coders**<br>*(Devin, OpenHands)* | Agen mandiri fokus pada perbaikan bug & coding repo. | Terlalu terfokus pada level kode (code-centric); mengabaikan tahap riset, bisnis, PRD lean, presentasi pitch deck, dan grounding ideasi. |
| **AI App Builders / Generators**<br>*(v0.dev, Bolt.new, Lovable)* | Prototyping UI instan berbasis browser. | Tidak menghasilkan arsitektur enterprise, tidak memvalidasi masalah bisnis, dan tidak menyediakan alur end-to-end dari ide hingga submission kit. |

---

## 4. Kelemahan Solusi Saat Ini (The Gap)

1. **Zero Opposition (Tidak Ada Peran Juri Internal):** Semua AI tool saat ini bersikap "yes-man" (selalu memuji dan menyetujui prompt pengguna), menyebabkan tim terjebak pada ide yang bias dan tidak kompetitif.
2. **Ketiadaan Visualisasi Koordinasi yang Intuitif:** Pengguna tidak bisa melihat proses berpikir dan handoff antar agen secara transparan tanpa harus membaca wall-of-text JSON log di terminal.
3. **Pemisahan Perencanaan vs Eksekusi:** Belum ada sistem yang menggabungkan pembuatan dokumen spesifikasi produk ([needed.md](file:///c:/Users/ASUS/Documents/GROW/Agency/needed.md)) dengan eksekusi kode dan materi presentasi dalam satu *single source of truth*.

---

## 5. Relevansi Tema & Rubric Penilaian Hackathon

SilaCorp menempati irisan strategis kategori **AI Multi-Agent Systems, Autonomous Workflow, & Developer Productivity Tools**.

* **Innovation & Uniqueness (Bobot ~30%):** Memperkenalkan konsep *Virtual Office Visual Simulation* di mana agen AI berwujud pegawai kantor yang bergerak dan berkoordinasi secara visual, dipadukan dengan *Judge Agent* sebagai oposisi independen.
* **Technical Depth & Execution (Bobot ~30%):** Implementasi multi-agent state graph, deterministic gates, event-driven escalation hierarki (Spesialis -> Director -> Human Board), serta automated code & artifact generation.
* **Practical Impact & Market Size (Bobot ~25%):** Jutaan pengembang dan inovator berpartisipasi dalam hackathon dan sprint produk setiap tahunnya. SilaCorp memangkas siklus 48 jam menjadi workflow terarah dengan jaminan submission siap juri.
* **UI/UX & Presentation (Bobot ~15%):** Visualisasi kanvas kantor virtual yang memukau (*wow-factor* seketika) menggantikan dashboard tabular yang membosankan.

---

## 6. Asumsi yang Belum Terbukti & Risiko Terbesar

### Asumsi
1. **Asumsi Kolaborasi Agen:** Agen dengan prompt spesialis berbeda (PM, Architect, Judge) dapat mencapai konsensus yang kohesif dalam maksimal 3 putaran dialog tanpa looping tanpa henti.
2. **Asumsi Kontrol Biaya Token:** Context window caching dan ringkasan state mampu menjaga biaya token LLM tetap efisien untuk satu siklus penuh hackathon.
3. **Asumsi Relevansi Visual Kantor:** Pengguna merasa animasi agen berpindah meja memberikan kejelasan status tugas dan meningkatkan *trust*, bukan dianggap sekadar beban visual.

### Risiko Terbesar & Mitigasi
* **Risiko 1: Token & Latency Explosion.**
  * *Mitigasi:* Gunakan model cepat dan hemat untuk koordinasi awal & judge critique; gunakan model reasoning tinggi hanya untuk arsitektur teknis dan deep code generation.
* **Risiko 2: Agen Berhalusinasi pada Gate Approval.**
  * *Mitigasi:* Deterministic Gate Checks—agen tidak bisa menandai gate lolos hanya dengan asumsi teks; harus ada artefak markdown terverifikasi dan persetujuan eksplisit dari Human Supervisor.
* **Risiko 3: Scope Creep pada MVP SilaCorp Sendiri.**
  * *Mitigasi:* Terapkan aturan ketat P0 pada pengembangan awal (Dokumen 3 & 3a) dan prioritaskan alur golden path.

---

## 7. Gate Status: Dokumen 1 — Research Brief

> **Gate Criteria:** Tim sepakat problem mana yang layak diselesaikan.  
> **Keputusan:**  
> [x] Problem: *Cognitive overload, lack of rubric-aligned opposition, and fragmented AI workflows in hackathon sprints.*  
> [x] Target User: *Hackathon teams and innovation builders under tight deadlines.*  
> [x] Nilai Tambah Inti: *Virtual Office multi-agent agency dengan oposisi Judge Agent dan Human-in-the-Loop Gate Approval.*  
>  
> **Status Gate: PASSED / SIAP LANJUT KE DOKUMEN 2 (Concept Brief).**
