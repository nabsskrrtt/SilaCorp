# Dokumen 3a — Spesifikasi Fitur Konkret (Feature Breakdown): SilaCorp

**Nama Produk:** SilaCorp (The Autonomous Virtual Office Hackathon Agency)  
**Parent Entity:** SilaLabs  
**Versi Dokumen:** 1.0.0  
**Tanggal:** 12 Oktober 2026  
**Status Gate:** Siap Direview Tim & Developer (Frontend & Backend)  

---

## 1. Breakdown Detail Fitur P0 (Frontend vs. Backend / Logic)

### F01 — Innovation Intake & Rubric Configurator
* **Sudut Pandang Frontend:**
  * **Komponen UI:** `IntakeModal`, `RubricWeightSliderGroup`, `ThemeInputBox`, `SprintDurationSelector`.
  * **Tata Letak:** Modal dialog terpusat dengan layout 2 kolom (Kolom kiri: Judul, tema, problem mentah; Kolom kanan: Slider bobot rubric berbobot total 100%, estimasi durasi).
  * **Event / Interaksi Pengguna:** 
    * Perubahan nilai slider otomatis menyeimbangkan persentase komponen lain agar total selalu 100%.
    * Klik tombol *"Launch Office"*, memvalidasi form dan memicu transisi ke tampilan kantor.
  * **Perubahan State Visual:** Transisi *fade-out* pada modal inisiasi, lampu ruangan kantor virtual menyala (*lights turning on animation*).
* **Sudut Pandang Backend / Logic:**
  * **Data Input:** `{ projectName: string, theme: string, rawProblem: string, rubricWeights: { innovation: number, technical: number, impact: number, presentation: number }, durationHours: number }`.
  * **Data Output:** `{ projectId: UUID, status: "INITIALIZED", currentPhase: "RESEARCH", activeDesk: "DIRECTOR" }`.
  * **Logika Bisnis & AI:** Inisialisasi root state di state manager; menyusun `SystemContextPrompt` yang akan diwariskan ke semua sub-agen.
  * **Aturan Validasi:** `projectName` min 3 karakter; `theme` tidak boleh kosong; total `rubricWeights` wajib tepat 100%.

---

### F02 — Virtual Office 2D Canvas & Agent Mobilization
* **Sudut Pandang Frontend:**
  * **Komponen UI:** `OfficeCanvas` (HTML5 Canvas / SVG Container), `AgentSprite` (elemen karakter dengan label status), `DeskStation` (area interaktif meja departemen), `PathTracker` (garis jalur pergerakan halus antar meja).
  * **Tata Letak:** Denah ruangan kantor 2D/isometrik:
    * Bagian Tengah Atas: *Executive Board Room* (Meja Human Supervisor)
    * Tengah: *Managing Director Desk*
    * Sisi Kiri: *Research Desk* & *Product Desk*
    * Sisi Kanan: *Architecture & Builder Desk* & *Pitch Desk*
    * Sudut Kiri Bawah: *The Judge Booth / Opposition Desk* (dengan palu sidang / visual khas juri)
  * **Event / Interaksi Pengguna:**
    * Hover pada meja: memunculkan tooltip status dan agen yang sedang bertugas.
    * Klik pada meja: membuka log percakapan internal atau draf aktif di meja tersebut.
  * **Perubahan State Visual:**
    * Agen berpindah dari Titik A ke Titik B menggunakan interpolasi linier halus (*easing in-out* berdurasi 1.2 detik).
    * Indikator status agen: Balon pikiran (*Thinking*), Mengetik di meja (*Working*), Berjalan (*Moving*), Tanda seru (*Escalating*).
* **Sudut Pandang Backend / Logic:**
  * **Data Input:** Event stream `{ agentId: string, fromDesk: DeskType, toDesk: DeskType, action: string, timestamp: number }`.
  * **Data Output:** Posisi koordinat grid visual dan pembaruan state koordinasi.
  * **Logika Bisnis & AI:** Koordinasi perpindahan agen dipicu secara deterministik ketika sebuah agen menyelesaikan sub-tugas dan memanggil agen berikutnya.
  * **Aturan Validasi:** Agen tidak boleh berpindah jika target meja sedang mengalami *lockdown* atau dokumen belum selesai di-generate.

---

### F03 — Autonomous PDCA Multi-Agent Pipeline
* **Sudut Pandang Frontend:**
  * **Komponen UI:** `PDCAStepper`, `PhaseStatusBadge`, `LiveThoughtFeed` (stream terminal miniatur di footer).
  * **Tata Letak:** Bar progres horizontal di bagian atas layar menampilkan tahapan: `PLAN (Doc 1–5)` -> `DO (Code & Scaffolding)` -> `CHECK (Rubric Audit)` -> `ACT (Final Package)`.
  * **Event / Interaksi Pengguna:** Pengguna dapat menekan tahapan yang sudah selesai untuk me-review kembali artefak terkait.
  * **Perubahan State Visual:** Step aktif berkedip lembut (*subtle pulsing accent*), step selesai berubah menjadi centang hijau.
* **Sudut Pandang Backend / Logic:**
  * **Data Input:** State proyek saat ini dan payload artefak fase sebelumnya.
  * **Data Output:** Dokumen terstruktur dalam format markdown standar [needed.md](file:///c:/Users/ASUS/Documents/GROW/Agency/needed.md).
  * **Logika Bisnis & AI:** Agen mengeksekusi *prompt template* spesialis berurutan:
    1. Researcher membuat Draf Dokumen 1.
    2. Product Lead menyusun Draf Dokumen 2, 3, 3a, 3b.
    3. Architect merumuskan Dokumen 4 & 5.
  * **Aturan Validasi:** Input token dibatasi per giliran agen; output divalidasi dengan regex header markdown untuk memastikan seluruh struktur terpenuhi.

---

### F04 — The Opposition Engine (Judge Agent)
* **Sudut Pandang Frontend:**
  * **Komponen UI:** `JudgeVerdictPanel`, `RubricScoreCard`, `CriticalIssueList`.
  * **Tata Letak:** Panel samping berwarna aksen tegas (amber/merah tua) dengan badge resmi *"OPPOSITION AUDIT REPORT"*.
  * **Event / Interaksi Pengguna:** Klik item kritik untuk melihat potongan teks dokumen yang disorot (*highlighting*).
  * **Perubahan State Visual:** Avatar Judge Agent membanting palu sidang (*gavel animation*) ketika kritik selesai dirumuskan.
* **Sudut Pandang Backend / Logic:**
  * **Data Input:** `{ documentType: string, contentMarkdown: string, rubricConfig: RubricWeights }`.
  * **Data Output:** `{ auditScore: number, isPassing: boolean, criticalCritiques: string[], groundedRecommendations: string[] }`.
  * **Logika Bisnis & AI:** Prompt Judge Agent diprogram dengan persona juri kompetisi yang skeptis dan ketat, menguji: kejelasan masalah, feasibilitas teknis dalam waktu terbatas, dan originalitas.
  * **Aturan Validasi:** Wajib mengeluarkan minimal 2 kritik konstruktif dan rekomendasi perampingan fitur jika beban fitur dinilai melebihi durasi hackathon.

---

### F05 — Human Board Gatekeeper Modal
* **Sudut Pandang Frontend:**
  * **Komponen UI:** `GateDecisionModal`, `SplitComparisonView` (Draf Dokumen vs Catatan Juri), `RevisionInputBox`, `ActionButtonGroup` (Approve / Revise / Veto).
  * **Tata Letak:** Modal layar penuh dengan mode fokus. Sisi kiri menampilkan dokumen yang diajukan; sisi kanan menampilkan telaah Judge Agent dan form instruksi manusia.
  * **Event / Interaksi Pengguna:**
    * Tombol **"Approve Gate"**: Mengunci dokumen dan memicu fase berikutnya.
    * Tombol **"Request Revision"**: Membuka input teks alasan revisi untuk dikirimkan kembali ke agen.
    * Tombol **"Veto / Direct Decision"**: Memungkinkan pengguna langsung mengedit draf teks sebelum disahkan.
  * **Perubahan State Visual:** Suara cap stempel digital (*stamp effect*), status gate berubah menjadi `LOCKED & APPROVED`.
* **Sudut Pandang Backend / Logic:**
  * **Data Input:** `{ gateId: string, decision: "APPROVE" | "REVISE" | "VETO", humanNotes?: string, editedContent?: string }`.
  * **Data Output:** `{ gateStatus: "PASSED", unlockedPhase: string, updatedArtifactPath: string }`.
  * **Logika Bisnis & AI:** Menyimpan versi final dokumen ke storage permanen; menginjeksi `humanNotes` ke memori jangka pendek agen jika revisi diminta.
  * **Aturan Validasi:** Gate tidak bisa dilewati tanpa klik aksi eksplisit dari pengguna.

---

### F06 — Real-Time Artifact Viewer & Workspace Export
* **Sudut Pandang Frontend:**
  * **Komponen UI:** `ArtifactTabs`, `MarkdownPreviewRenderer`, `ExportDropdown` (Zip, Individual Markdown, JSON Bundle).
  * **Tata Letak:** Panel samping kanan yang dapat ditarik (*collapsible drawer*), mendukung *syntax highlighting* untuk kode dan rendering tabel.
  * **Event / Interaksi Pengguna:** Klik tombol *"Export Submission Pack"*, memicu pengunduhan file zip.
  * **Perubahan State Visual:** Indikator unduhan selesai dengan status *success toast*.
* **Sudut Pandang Backend / Logic:**
  * **Data Input:** Request ekspor dari client berisi `projectId`.
  * **Data Output:** Stream data `application/zip` berisi seluruh file dokumen di direktori `docs/` serta metadata proyek.
  * **Logika Bisnis & AI:** Packaging seluruh artefak yang telah berstatus `APPROVED` tanpa menyertakan draf yang ditolak.
  * **Aturan Validasi:** File yang belum disetujui gate-nya diberi watermark *"DRAFT - UNAPPROVED"*.

---

## 2. Edge Cases & Penanganan Kegagalan Spesifik per Fitur

| Fitur | Skenario Edge Case | Mekanisme Penanganan Kegagalan (Fallback) |
| :--- | :--- | :--- |
| **F01** | Pengguna memasukkan tema yang terlalu pendek atau ambigu (misal hanya: *"bikin web"*). | Sistem menampilkan saran otomatis (*AI Prompt Expander*) untuk meminta penjelasan target sektor atau pengguna dalam 1 klik. |
| **F02** | Layar browser pengguna terlalu kecil (mobile atau layar kecil). | Canvas secara otomatis beralih ke *Responsive Pan/Zoom Canvas* atau fallback ke mode *Department Card View*. |
| **F03** | Agen menghasilkan dokumen yang strukturnya terpotong karena batas token (Max Token Truncation). | Orchestrator mendeteksi markdown yang tidak lengkap, otomatis memicu sub-task *"Continue Generation"* menyambung sub-bagian yang hilang. |
| **F04** | Judge Agent memberikan skor 0 atau memberikan kritik destruktif tanpa solusi. | Sanitizer logic memfilter hasil audit dan memaksa format output menyertakan *"Actionable Grounding Suggestions"*. |
| **F05** | Pengguna menutup browser saat modal Gate sedang terbuka. | State gate tetap tersimpan di `AWAITING_HUMAN_APPROVAL`; saat dibuka kembali, sistem langsung menampilkan modal yang sama. |
| **F06** | Browser memblokir download otomatis file ZIP. | Sistem menyediakan tautan unduh manual alternatif dan tombol copy-to-clipboard untuk masing-masing dokumen. |

---

## 3. Matriks Keterlacakan (Traceability Matrix)

| Kode Fitur | Nama Fitur | Komponen UI Frontend Terkait | Service & Modul Backend Terkait | Artefak / Dokumen Acuan |
| :--- | :--- | :--- | :--- | :--- |
| **F01** | Innovation Intake | `IntakeModal`, `RubricWeightSliderGroup` | `ProjectService.initializeProject()` | Dokumen 1 — Research Brief |
| **F02** | Virtual Office Canvas | `OfficeCanvas`, `AgentSprite`, `DeskStation` | `OfficeStateManager`, `CanvasEventBus` | Dokumen 2, Dokumen 5 |
| **F03** | PDCA Agent Pipeline | `PDCAStepper`, `LiveThoughtFeed` | `AgentOrchestrationEngine`, `LLMRouter` | Dokumen 1, 2, 3, 4, 5 |
| **F04** | The Opposition Engine | `JudgeVerdictPanel`, `RubricScoreCard` | `OppositionAuditService`, `RubricEvaluator` | Dokumen 1, 2, 3 |
| **F05** | Human Board Gatekeeper | `GateDecisionModal`, `SplitComparisonView` | `GatekeeperService.recordDecision()` | Seluruh Gate Dokumen 1–5 |
| **F06** | Artifact Viewer & Export | `ArtifactTabs`, `MarkdownPreviewRenderer` | `ArtifactBundleService.createZip()` | File output di `docs/*.md` |

---

## 4. Gate Status: Dokumen 3a — Spesifikasi Fitur Konkret

> **Gate Criteria:** Developer Frontend dan Backend tahu persis apa yang harus dibangun per fitur tanpa multitafsir.  
>  
> **Verifikasi Spesifikasi:**  
> [x] Komponen Frontend, tata letak, event, dan visual state terinci untuk semua fitur P0.  
> [x] Data I/O, aturan validasi, dan service layer backend terdefinisi dengan format tipe data.  
> [x] Skenario edge cases dan mitigasi fallback siap diimplementasikan.  
> [x] Matriks keterlacakan menghubungkan kode fitur dengan komponen teknis secara 1-to-1.  
>  
> **Status Gate: PASSED / SIAP LANJUT KE DOKUMEN 3b (End-to-End Workflows & Tracks).**
