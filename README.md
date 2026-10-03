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
| `report/SBTDF204_CaseStudy1_2025-FWSD-11468.docx` | Full forensic report (Word) |
| `report/SBTDF204_CaseStudy1_2025-FWSD-11468.pdf` | Same report as PDF |
| `screenshots/` | 27 labelled, redacted screenshots (Fig01 to Fig27), numbered as in the report |
| `evidence_records/` | Hash records, packet exports, timeline, evidence log and command log as plain text/CSV |
| `README.md` | This file |

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

## Important notes for the examiner

- **Time basis:** all packet times are UTC as shown by Wireshark. The analysis VM clock was UTC-4 (EDT). The Yahoo mailbox times in the scenario slides appear to be UTC-7; this is an assumption and is stated as such in the report.
- **Transcribed records:** the text and CSV files in `evidence_records/` were typed from the screenshots named inside each file. They are not copies of files on the analysis VM.
- **Redaction:** screenshots are cropped copies. Unrelated session and tracking values were covered or cropped out (see `redaction_and_transcription_note.txt` and Appendix C of the report). The raw cookie listing is not included.
- **Scenario slides:** emails, headers and the Chem 109 roster were taken from the scenario slide deck (`slides.pdf`) on the Digital Corpora scenario page and are cited by PDF page number.
- **Handling:** the capture was used only for this authorised academic case study. No host or account in the evidence was contacted.

## Screenshot index

| Fig | File | Caption |
|---|---|---|
| 1 | `screenshots/Fig01_download_and_hash_record.png` | Download of nitroba.pcap (wget), download date in UTC, stat output, and SHA-256 and MD5 values of the original file. (E01) |
| 2 | `screenshots/Fig02_working_copy_and_capinfos.png` | Working copy created with cp -p, hash comparison (“HASHES MATCH”) and capinfos summary. Capinfos times here are shown in the VM’s local time (UTC-4); see Figure 5 for the UTC values. (E02) |
| 3 | `screenshots/Fig03_published_hash_values.png` | Published MD5, SHA1 and SHA256 values for nitroba.pcap on the Digital Corpora scenario page. (E01) |
| 4 | `screenshots/Fig04_hash_verification_OK.png` | Published hashes saved to a text file and verified against the original with md5sum, sha1sum and sha256sum (all OK). (E01) |
| 5 | `screenshots/Fig05_write_protect_and_UTC_basis.png` | Original file permissions after chmod a-w (-r--r--r--), and capinfos/tshark output run with TZ=UTC showing the capture span in UTC (packet 1: 2008-07-22T01:51:07.095278Z). (E02) |
| 6 | `screenshots/Fig06_GET_requests_to_willselfdestruct.png` | GET filter for www.willselfdestruct.com showing nine requests from 192.168.15.4 to 69.25.94.22, UTC time column, and HTTP details for packet 82936. (E03) |
| 7 | `screenshots/Fig07_frame_82936_UTC_arrival_time.png` | Frame details for packet 82936 showing local (EDT) and UTC arrival times, epoch 1216706623.825871. (E03) |
| 8 | `screenshots/Fig08_POST_form_fields_packet_83601.png` | Filter isolating the single POST (packet 83601) with HTML Form URL Encoded fields: to, from, subject, message, type, ttl. (E04) |
| 9 | `screenshots/Fig09_follow_tcp_stream_1707.png` | Follow TCP Stream (tcp.stream eq 1707): request with URL-encoded body and the 302 reply to /secure/success. The reply’s Date header (07:24:45 GMT) differs from the capture time by about 1 h 20 min; see Section 7. (E04, E05) |
| 10 | `screenshots/Fig10_tcp_stream_1707_packets.png` | Stream 1707 packet list: handshake, POST (83601, 06:04:24.311700 UTC), 302 reply (83604) and connection close. (E04, E05) |
| 11 | `screenshots/Fig11_single_POST_csv_record.png` | TShark export showing exactly one POST to willselfdestruct.com (header plus one row) with frame number, UTC time, epoch time, MACs, IPs, port, stream and URI. (E06) |
| 12 | `screenshots/Fig12_slide10_second_email_inbox.png` | Scenario slide (PDF page 10): Yahoo inbox showing a message from noreply@willselfdestruct… with subject “you can’t find us”, Mon 7/21/08 11:04 PM. (E14) |
| 13 | `screenshots/Fig13_slide11_notification_email.png` | Scenario slide (PDF page 11): notification email stating the message can be viewed only once for 30 second(s). (E14) |
| 14 | `screenshots/Fig14_slide12_message_as_displayed.png` | Scenario slide (PDF page 12): the message as displayed by willselfdestruct.com, from [Undisclosed Sender] to lilytuckrige@yahoo.com. (E14) |
| 15 | `screenshots/Fig15_slide13_message_destroyed.png` | Scenario slide (PDF page 13): “Message Has Been Destroyed” page. (E14) |
| 16 | `screenshots/Fig16_ethernet_header_packet_82936.png` | Ethernet II layer of packet 82936 (GET /secure/submit): source MAC 00:17:f2:e2:c0:ce, destination 00:1d:d9:2e:4f:60. (E07) |
| 17 | `screenshots/Fig17_ethernet_header_packet_83601.png` | Ethernet II layer of packet 83601 (the POST): same source MAC. Only the filter bar, details pane and status bar are shown; the packet list was cropped to avoid unrelated session data. (E07) |
| 18 | `screenshots/Fig18_mac_ip_inventory.png` | MAC/IP inventory of the capture (top 20 rows): 34,554 frames from 00:17:f2:e2:c0:ce with source IP 192.168.15.4; 2,154 frames from 00:1d:d9:2e:4f:60 with source IP 192.168.15.1. (E08) |
| 19 | `screenshots/Fig19_ip_to_mac_and_ARP_check.png` | Non-IP frames from the client MAC (28, all ARP) and MAC check for 192.168.15.4 (34,554 frames, one MAC only). (E08) |
| 20 | `screenshots/Fig20_gmailchat_cookie_packets.png` | Packets carrying gmailchat=jcoachj: 100 in total (first three and last three shown) and those nearest the POST (83326 and 84201), all to mail.google.com (74.125.19.17). (E09) |
| 21 | `screenshots/Fig21_cookie_packet_83326_gmailchat.png` | Packet 83326 (06:04:05.546193 UTC) with the Cookie header expanded. Only the gmailchat cookie pair is shown; all other cookie values and token fields are redacted. (E09) |
| 22 | `screenshots/Fig22_user_agent_comparison_no_cookie_check.png` | User-Agent comparison for the client MAC (identical string on Gmail and willselfdestruct requests) and the check that no willselfdestruct request carries a Cookie header (no output). (E11) |
| 23 | `screenshots/Fig23_slide14_class_roster.png` | Scenario slide (PDF page 14): Chemistry 109 class list (names only). (E12) |
| 24 | `screenshots/Fig24_slide7_dorm_room_router.png` | Scenario slide (PDF page 7): three residents share the room; Wi-Fi router installed with no password. (E15) |
| 25 | `screenshots/Fig25_slide8_sniffer_diagram.png` | Scenario slide (PDF page 8): devices connect through the router to a network switch with a logging host. (E15) |
| 26 | `screenshots/Fig26_slide5_full_headers_first_email.png` | Scenario slide (PDF page 5): full headers of the first email, with the Received line from 140.247.62.34 highlighted (Sun, 13 Jul 2008 17:21:01 -0700). (E13) |
| 27 | `screenshots/Fig27_slide6_reverse_dns.png` | Scenario slide (PDF page 6): host 140.247.62.34 resolves to G24.student.nitroba.org. (E13) |
