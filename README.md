# SBT-DF204 Case Study 1: Investigating Harassment Email Traffic With Wireshark

**Student:** Mary-Joy Adewole  
**Registration number:** 2025/FWSD/11468  
**Institution:** International Cybersecurity and Digital Forensics Academy (ICDFA)  
**Course:** SBT-DF204 Computer Forensics Case Studies  
**Evidence analysed:** `nitroba.pcap` (2008 Nitroba University Harassment Scenario, Digital Corpora)  
**Analysis date:** 3 October 2026

## What is in this package

| Path | Contents |
|---|---|
| `report/SBTDF204_CaseStudy1_2025-FWSD-11468.pdf` | Full forensic report as PDF |
| `screenshots/` | labelled, redacted screenshots, as in the report |
| `evidence_records/` | Hash records, packet exports, timeline, evidence log and command log as plain text/CSV |


The original `nitroba.pcap` is **not** included, as the brief says not to upload it unless requested.

## Evidence records

| File | What it holds |
|---|---|
| `hash_records.txt` | File name, source, size, download time (UTC), SHA-256/MD5/SHA-1, published values and verification result |
| `capinfos_summary_utc.txt` | Capture properties and UTC time span |
| `willselfdestruct_packets_utc.csv` | The nine GETs, the POST (83601) and the 302 reply (83604) with UTC times |
| `post_packet_83601.txt` | Form fields, stream 1707, server reply and the single-POST check |
| `mac_and_ip_checks.txt` | MAC to IP mapping, ARP frames, gateway MAC |
| `cookie_identity_fragments.txt` | Identity-bearing cookie fragments, gmailchat packet times, User-Agent counts |
| `timeline_utc.csv` | UTC timeline |
| `evidence_log.csv` | Evidence log E01 to E16 (same as Appendix A of the report) |
| `command_log.txt` | Commands and display filters used |
| `redaction_and_transcription_note.txt` | What was redacted and how the text records were made |

## Important notes

- **Time basis:** all packet times are UTC as shown by Wireshark. The analysis VM clock was UTC-4 (EDT). The Yahoo mailbox times in the scenario slides appear to be UTC-7; this is an assumption and is stated as such in the report.
- **Transcribed records:** the text and CSV files in `evidence_records/` were typed from the screenshots named inside each file. They are not copies of files on the analysis VM.
- **Redaction:** screenshots are cropped copies. Unrelated session and tracking values were covered or cropped out (see `redaction_and_transcription_note.txt` and Appendix C of the report). The raw cookie listing is not included.
- **Scenario slides:** emails, headers and the Chem 109 roster were taken from the scenario slide deck (`slides.pdf`) on the Digital Corpora scenario page and are cited by PDF page number.
- **Handling:** the capture was used only for this authorised academic case study. No host or account in the evidence was contacted.
