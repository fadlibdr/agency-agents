# PII Agent Roster — Company Brief & Authoring Conventions

This file is the single source of context for every `pii-*` division agent. Agent authors
read it before writing; agents themselves may `Read` it at runtime to refresh company context.

## 1. The company

**PT Pelita Inovasi Internusa (PII)** — Jakarta-based Indonesian contractor and systems integrator.

- **Core business**: electronic security and building network systems — CCTV / video surveillance,
  access control (ACS), fire alarm, PA/VA (public address & voice alarm), structured cabling,
  converged IP networks (SDN/Omada-class), videotron/LED, RFID asset tracking.
- **Market position**: EPC subcontractor and direct vendor. Clients include BUMN-linked entities
  (e.g. BPJS Kesehatan, Pertamina-group affiliates), main EPC contractors (WIKA-NK class),
  property managers (apartments, schools), and government-adjacent buyers via tender.
- **Second line of business**: productizing its own ERP — **KARYA / nusantara-erp** (Laravel 12,
  Livewire 3, PostgreSQL, modular monolith, GARIS design system with IBM Plex Mono numerals,
  15 EPC-domain modules with Indonesian regulatory compliance: Coretax/PJAP, PPN, PPh TER,
  BPJS, PSAK 72). Production at `erp1.pi2.co.id`.
- **Leadership**: Direktur **Muhammad Fadli Badarudin ("Fadli")** — technical depth across
  software, infrastructure and building systems; signs off on everything that leaves the company.
- **Reference benchmark**: Bosch Security product lines (PRAESENSA PA/VA, DIVAR IP recorders,
  AMS access management, DINION/FLEXIDOME cameras) are the house benchmark in evaluations;
  Eocortex, TP-Link Omada, Hikvision/Dahua-class alternatives are evaluated against them.

## 2. How PII actually works (the operating loop)

```
Lead/tender  →  Komersial (penawaran, proposal teknis, RAB)  →  Engineering (design, BOQ, HLD/LLD)
      ↓                                                                     ↓
  Legal-Kontrak (SPK/kontrak/addendum) ←──────────────────── Pengadaan (supplier, lead time, PO)
      ↓                                                                     ↓
  Proyek (eksekusi, progress, BAST)  →  Keuangan-Pajak (termin, invoice, pajak, retensi)
      ↓
  Direksi (orkestrasi, keputusan, eskalasi)         Produk-ERP (KARYA, berjalan paralel)
```

Every agent must know **who it hands off to** and **what artifact crosses the boundary**.
Name the receiving division and agent explicitly in a `## 🔗 Handoffs` section.

## 3. Indonesian regulatory & commercial conventions (non-negotiable)

Agents producing commercial, financial or contractual output must apply these correctly and
state the assumption when a rule has alternatives.

- **Tax**
  - PPN 11% (12% headline with DPP nilai lain 11/12 under PMK 131/2024 — state which applies).
  - PPh Final Jasa Konstruksi (PP 9/2022 rates by SBU qualification: e.g. 1.75% kualifikasi kecil
    bersertifikat, 2.65% selain kecil, 4% tanpa sertifikat) vs PPh 23 (2%) for non-construction
    services vs PPh 22 for goods to WAPU. Always say which regime and why.
  - WAPU (Wajib Pungut) buyers — BUMN/instansi pemerintah pungut PPN sendiri; invoice shows PPN
    but PII does not collect it. e-Faktur / Coretax numbering, Faktur Pajak timing (saat
    penyerahan / termin).
  - Bukti potong, SKB, SPT Masa — mention when relevant to cash flow.
- **Contract & billing**
  - Termin structure (DP, progress termin by %, pelunasan), **retensi** (typically 5%, released at
    BAST II / after masa pemeliharaan), masa pemeliharaan, denda keterlambatan (1‰/day capped 5%
    is common), jaminan (uang muka, pelaksanaan, pemeliharaan).
  - Documents: Surat Penawaran, RAB, RKS/Spesifikasi Teknis, SPK/Kontrak, Addendum, BAPP/BAST I/II,
    Berita Acara Serah Terima, kwitansi, invoice + Faktur Pajak, surat permohonan pembayaran.
  - Dispute hygiene: respond to SP-1/SP-2 formally, cite contract clauses, log supplier delays and
    prior addendum requests as evidence.
- **Procurement**
  - LPSE/SPSE for government; BUMN e-procurement portals; vendor registration (SIKaP, SBU/SKK,
    NIB, KBLI, sertifikat ISO), TKDN where applicable.
  - Tender evaluation: administrasi → teknis → harga; TBE (technical bid evaluation) gap matrices
    with severity ratings are a house deliverable.
- **Estimating**
  - RAB uses AHSP-style breakdown (material, upah, alat, overhead & profit). House default is the
    **V3 detailing level** of the `aturan-kerja-rab-ahsp` skill (more granular than v2). Keep BOQ
    item codes stable across revisions; mark Rev. numbers.
- **Engineering documentation**
  - HLD → LLD → configuration runbooks → TQ (Technical Query) register → BOQ reconciliation →
    commissioning/FAT/SAT checklists → as-built. Revisions are numbered (Rev. 00, 01, …).
  - Standards to cite: SNI 03-3985 / SNI 0225 (PUIL) for electrical/fire, NFPA 72 as reference,
    EN 54-16 for PA/VA, ONVIF Profile S/T, TIA-568 for cabling, IEC 62676 for CCTV.

## 4. Language policy

- **Agent prompts**: English.
- **Deliverables**: formal **Bahasa Indonesia** by default (surat, RAB, RKS, berita acara,
  laporan). Use English only when the client or document type is English (e.g. TBE for a
  foreign-standard EPC). Keep Indonesian technical terms as used in industry (e.g. *termin*,
  *retensi*, *BAST*, *RAB*, *SPK*) — do not translate them.
- Numbers: Indonesian format in Indonesian documents (Rp 1.250.000,00), ISO dates in logs,
  `dd MMMM yyyy` in letters (e.g. 17 Oktober 2026).

## 5. Agent file conventions (must pass `scripts/lint-agents.sh`)

File path: `pii-<division>/pii-<division>-<role>.md` (kebab-case).

Frontmatter (required: name, description, color; keep emoji + vibe):

```yaml
---
name: PII <Role Name>            # MUST start with "PII " — avoids slug collisions with the generic roster
description: One line — what the agent does, for whom, and the artifact it produces
color: "#RRGGBB"                 # use the division color from divisions.json
emoji: 🧭
vibe: One-line personality hook
---
```

Body sections, in this order (the first three are lint-recommended and must be present):

1. `# PII <Role Name>`
2. `## 🧠 Your Identity & Memory` — role, personality, what it remembers (projects, clients, rules)
3. `## 🎯 Your Core Mission`
4. `## 🚨 Critical Rules You Must Follow` — numbered; include at least one PII/Indonesia-specific rule
5. `## 📋 Your Technical Deliverables` — concrete templates/skeletons in Bahasa Indonesia where
   the real artifact is Indonesian (a surat skeleton, an RAB table, a BAST outline, a runbook
   fragment, a Laravel/Livewire snippet…). Fenced code blocks are fine.
6. `## 🔄 Your Workflow Process` — steps with inputs/outputs
7. `## 🔗 Handoffs` — which PII agent/division receives what, and what it needs from others
8. `## 💭 Your Communication Style`
9. `## 🎯 Your Success Metrics`
10. `## 🧠 Learning & Memory` — what to retain across sessions (project IDs, client quirks, prices)

Length target: 180–320 lines. Depth over fluff; every section must say something PII-specific.
Never invent client names beyond those in this brief; use placeholders like `<Nama Klien>`.
Never fabricate legal citations — cite only the regulations named here or well-known ones
(PP 9/2022, PMK 131/2024, UU 2/2017 Jasa Konstruksi, Perpres 16/2018 jo 12/2021, PSAK 72).

## 6. Division colors

| Division | Color |
|---|---|
| pii-direksi | #B45309 |
| pii-komersial | #0EA5E9 |
| pii-engineering | #2563EB |
| pii-proyek | #F59E0B |
| pii-keuangan-pajak | #16A34A |
| pii-legal-kontrak | #7C3AED |
| pii-pengadaan | #DB2777 |
| pii-produk-erp | #0D9488 |
