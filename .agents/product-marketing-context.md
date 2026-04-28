# Product Marketing Context — Plakar

*Last updated: 2026-04-28*

## Product Overview
**One-liner:** Plakar is the open-source standard for unified resilience — backup anything, store anywhere, with zero-trust encryption and no vendor lock-in.
**What it does:** Plakar is an open-source backup and restore platform built around Kloset, a self-contained immutable snapshot engine that performs client-side deduplication and encryption before data leaves the source. Data is stored in an open, portable PTAR format across any backend (S3, SFTP, local disk, cloud). Plakar Enterprise adds a unified control plane for posture management, compliance, and MSP delegation via the Vault Protocol.
**Product category:** Data Resilience / Backup & Recovery (enterprise infrastructure + security)
**Product type:** Open-source core (free, self-hosted) + commercial Enterprise control plane
**Business model:** Open-source adoption engine → Plakar Enterprise licensing (usage-based, indexed on secured data volume). Future: licensing Vault Server technology to MSPs/service providers.

## Target Audience
**Target companies:** 500–5,000 employees, $50M+ revenue; Finance (compliance/audit), Healthcare (HIPAA), Tech & Cloud Providers, Legal, Scale-ups; Europe (GDPR), North America (HIPAA/SOC2)
**Decision-makers:** DevOps / Platform Engineers (primary users), SREs / Infrastructure Leads, CISOs / Security Leaders, IT Directors / CTOs, MSP Operators, Compliance Officers
**Primary use case:** Zero-trust backup that achieves both client-side deduplication and encryption — eliminating the trade-off legacy tools force between storage efficiency and security
**Jobs to be done:**
- Protect data across on-prem, cloud, and SaaS without handing encryption keys to the storage layer
- Prove backup integrity and coverage before an audit or incident (not after)
- Restore any file or environment instantly without full-catalog dependencies
**Use cases:**
- Filesystem and server backup (on-prem and cloud)
- Database backup (PostgreSQL, MySQL, etc.)
- Kubernetes cluster backup
- SaaS data protection (M365 and others)
- Ransomware-resistant immutable snapshots
- Instant staging environment provisioning from snapshots
- ML training dataset versioning and rollback
- Long-term archival with guaranteed format readability (50+ years)

## Personas
| Persona | Cares about | Challenge | Value we promise |
|---------|-------------|-----------|------------------|
| DevOps / Platform Engineer | Reliability, automation, CLI-native tooling | Backup scripts break silently; no integrity verification | Self-contained snapshots with cryptographic proofs; instant mount |
| CISO / Security Leader | Zero-trust compliance, audit trails, key control | Legacy tools require trusting storage layer with keys | Client-side encryption + dedup — keys never leave source |
| IT Director / CTO | Cost, vendor risk, scalability | Storage bills exploding; proprietary formats mean lock-in | 90%+ cost reduction; open PTAR format; no vendor dependency |
| MSP Operator | Scalable service delivery, customer trust | Can't offer backup without being data custodian | Vault Protocol: manage backup without ever holding customer keys |
| Compliance Officer | Audit evidence, coverage visibility | Weeks of manual evidence collection before audits | Unified posture dashboard; signed backups; cryptographic proofs |

## Problems & Pain Points
**Core problem:** Enterprise backup has entered a systemic governance failure. Legacy architectures force an impossible trade-off: encrypt your data and lose deduplication efficiency (storage costs explode), or deduplicate efficiently and surrender your keys to the infrastructure (zero-trust is broken). Meanwhile data volumes double every 3–4 years, zero-trust is now mandatory, and data fragments across on-prem, cloud, and SaaS with no unified view.
**Why alternatives fall short:**
- Legacy tools (Veeam, Rubrik, Commvault) were designed for pre-cloud scale and force key trust at the storage layer
- Open-source tools (restic, BorgBackup, Kopia) lack enterprise posture management, delegation protocols, and broad SaaS/DB integrations
- Cloud-native snapshots (AWS Backup, Azure Backup) are vendor-locked with no cross-cloud portability or SaaS coverage
- Custom scripts have no integrity verification, no unified visibility, no audit trails
**What it costs them:** Skyrocketing storage and egress bills; backup failures discovered only at restore time; weeks of manual audit evidence collection; ransomware hitting backup catalogs; restore SLA misses (hours instead of minutes); no ability to delegate to MSPs without sharing keys
**Emotional tension:** "We don't know if our backups actually work until we need them." Fear of discovering failures during an incident. Stress of fragmented visibility. Doubt about whether their zero-trust posture actually holds.

## Competitive Landscape
**Direct:**
- Rubrik / Cohesity — expensive hardware appliances, vendor-locked, require key trust at storage layer
- Veeam — proprietary `.vbk` format, catalog collapses at scale, catalog DB required for portable restore
- Commvault — architecture sprawl, separate licensing for SaaS/cloud sources, no unified zero-trust model
- restic / BorgBackup / Kopia — no enterprise posture management, no delegation protocol, limited SaaS/DB integrations

**Secondary:**
- Cloud-native snapshots (AWS Backup, Azure Backup) — cloud-vendor locked, no cross-cloud portability, no SaaS coverage
- SaaS backup point solutions (Veeam for M365, Druva) — source-specific, separate licensing, fragmented posture

**Indirect:**
- Custom scripts + cloud snapshots — no consistency, no integrity verification, no unified visibility

## Differentiation
**Key differentiators:**
- Zero-trust by architecture: deduplication AND encryption both happen client-side before data leaves source — mathematically guaranteed, not policy
- Efficiency without the trade-off: 90%+ storage/egress reduction while maintaining full encryption (legacy tools force you to choose)
- Index-in-snapshot architecture: no central catalog database → petabyte-scale performance, no catalog collapse
- Open format guarantee: PTAR & Kloset are open-source and publicly auditable; data readable without Plakar software for 50+ years
- Kloset = Docker container model for data: self-contained, portable, instantly restorable anywhere
- Instant mount: browse terabytes as a local filesystem without restoring; recover a single file in seconds
- Vault Protocol: safely delegate backup operations to MSPs without sharing encryption keys — provider is cryptographically blind

**How we do it differently:** Client-side dedup + encryption in a single pass via Kloset engine; distributed index inside each snapshot; open portable format; zero-knowledge delegation protocol

**Why that's better:** No storage cost penalty for security; no key escrow risk; no catalog bottleneck at scale; no format lock-in; MSPs can operate without becoming data custodians

**Why customers choose us:** "Open-source backup that actually scales"; "zero-trust by design, not by checkbox"; "one dashboard shows us exactly what's protected and what isn't"; "our MSP manages backup without ever touching our encryption keys"

## Objections
| Objection | Response |
|-----------|----------|
| "Open-source might not be enterprise-ready" | CNCF Silver Member (Linux Foundation, joined Jan 2026). Core cryptography publicly audited. Plakar Enterprise adds SLA-backed support, posture management, and Vault Protocol. |
| "We already have Veeam/Rubrik" | Those tools were designed for pre-cloud scale and force a choice between deduplication and encryption. Plakar eliminates the trade-off and cuts storage costs 90%+ without touching your keys. |
| "We don't want another backup silo" | Plakar is explicitly designed to unify on-prem, cloud, and SaaS into a single posture view — the opposite of adding a silo. |
| "Can it scale to our data volume?" | Index-in-snapshot removes the central catalog bottleneck. Designed for exabyte scale with minimal RAM. No catalog collapse. |
| "What about vendor lock-in?" | Data in PTAR/Kloset open formats, readable by open-source code. You own your data independent of Plakar. No proprietary runtime required. |
| "How do we know restores actually work?" | Native cryptographic integrity proofs. Mount snapshots to run business logic tests without a full restore. |

**Anti-persona:** Teams happy with a single cloud provider's native snapshots and no cross-cloud or SaaS exposure; very small teams without compliance requirements or MSP relationships.

## Switching Dynamics
**Push:** Backup failures discovered only at restore time; storage bills exploding; audit prep taking weeks; ransomware hitting backup catalogs; catalog database collapsing under scale
**Pull:** 90%+ storage cost reduction without surrendering keys; cryptographic integrity proofs; single posture dashboard; instant file recovery; MSP delegation without key sharing
**Habit:** Existing Veeam/Rubrik contracts; familiar tooling even if broken; "it's not broken enough yet to switch"
**Anxiety:** Migration complexity; open-source supportability for enterprise; learning curve for new snapshot model; risk of data loss during transition

## Customer Language
**How they describe the problem:**
- "We don't know if our backups actually work until we need them"
- "Our storage bills keep climbing and I can't explain why to finance"
- "Our MSP wants access to everything just to run backups"
- "We're spending weeks pulling audit evidence manually"

**How they describe us:**
- "Open-source backup that actually scales"
- "Zero-trust by design, not by checkbox"
- "We browse backups like a filesystem — instant file recovery"
- "One dashboard shows us exactly what's protected and what isn't"
- "Our MSP manages backup without ever touching our encryption keys"

**Words to use:** zero-trust, client-side encryption, deduplication, Kloset, immutable snapshots, open format, vendor-neutral, unified posture, backup posture management, Plakar Vault Protocol, petabyte-scale, cryptographic integrity, instant mount, resilience, open-source, CNCF, Linux Foundation

**Words to avoid:** black box, trust us, proprietary, "our appliance," lock-in, "just works" (without proof)

**Glossary:**
| Term | Meaning |
|------|---------|
| Kloset | Plakar's core snapshot engine — performs client-side dedup + encryption in a single pass |
| PTAR | Open, portable archive format used to store Kloset snapshots |
| Vault Protocol | Zero-knowledge delegation protocol enabling MSPs to operate backup without holding customer keys |
| Backup Posture Management | Unified visibility layer showing protected vs. unprotected assets across all environments |
| Index-in-snapshot | Architecture where the backup index lives inside each snapshot, not in a central catalog database |

## Brand Voice
**Tone:** Rigorous, engineer-first, security-minded; confident without arrogance; precise without dryness
**Style:** Direct. Show don't tell. Proof over claims. "Don't trust us — verify."
**Personality:** Open by default, built by veterans, designed for war (not for the brochure). The team of OpenBSD core committers and ex-CPTO of a $4B platform.

## Proof Points
**Metrics:**
- 90%+ storage and egress cost reduction via client-side dedup before encryption
- >100:1 efficiency ratio
- 70% cost reduction cited by a customer (without sharing encryption keys)
- 99.9% protected coverage demonstrated in dashboard

**Customers:** Holberton, République Française, Spark Angle, Moose & Toom, Hoodie

**Testimonials:** (to be added as collected)

**Value themes:**
| Theme | Proof |
|-------|-------|
| Cost reduction | 90%+ storage/egress savings; 70% customer-cited reduction |
| Zero-trust guarantee | Client-side dedup + encryption; Vault Protocol; mathematically guaranteed, not policy |
| Scale without limits | Index-in-snapshot; no catalog collapse; petabyte-scale linear performance |
| Open & auditable | PTAR/Kloset open-source; CNCF Silver Member; publicly audited cryptography |
| Instant recovery | Mount terabytes as filesystem; single file in seconds |

## Goals
**Business goal:** Establish Plakar as the open-source standard for enterprise backup, then convert regulated enterprises to Plakar Enterprise for unified posture management
**Conversion action (open-source):** "Protect your data in a minute" — CLI download, quickstart, GitHub star
**Conversion action (enterprise):** "Book a demo" — for teams needing posture management, Vault Protocol, enterprise support
**Current metrics:** ~1,500 GitHub stars, 600 Discord members, $3M pre-seed (Seedcamp, Olivier Pomel/Datadog, Solomon Hykes/Docker)
