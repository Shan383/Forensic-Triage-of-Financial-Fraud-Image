# 🔍 Forensic Triage of Mantooth.E01 – Financial Fraud Investigation

## 📌 Case Overview
This repository documents a complete forensic triage of the disk image `Mantooth.E01`, conducted as part of the **Cyberster Blue Team Internship (Phase Two, Week 10)**. The investigation focused on identifying evidence of financial fraud, including cheque washing, identity theft, and anti-forensic techniques.

## 🛠️ Tools Used
- **Autopsy 4.19+** – Primary forensic platform
- **FTK Imager** – Hash verification and image mounting
- **Registry Explorer** – Windows registry hive analysis
- **PECmd (Eric Zimmerman)** – Prefetch file parsing
- **EvtxECmd** – Event log extraction
- **LEcmd** – LNK file analysis

## 🎯 Key Findings

### 1. Image Integrity
- **MD5 Hash:** `312172101a169f2720793bde3d9df8c`
- Verified using Autopsy Data Source Integrity module and FTK Imager

### 2. Partition Layout
| Partition | File System | Size | Offset |
|-----------|-------------|------|--------|
| vol_vol1 | NTFS | 100 MB | 1,048,576 bytes |
| vol_vol2 | NTFS | 59.62 GB | 105,906,176 bytes |

### 3. Hidden Files (Alternate Data Streams)
| File Name | Path | Significance |
|-----------|------|---------------|
| HARDCORE.jpg | `/vol_vol2/Users/Wes Mantooth/Documents/My poem.txt:HARDCORE.JPG` | Hidden JPEG in ADS |
| pfah603.jpg | `/vol_vol2/Users/Wes Mantooth/Documents/ADS/readthis.txt:pfah603.jpg` | Second hidden JPEG |

### 4. Deleted Files Analysis
- **CameraShy.exe** – Deleted on `2007-08-04 21:04:26 PKT`
- Original path: `/vol_vol2/Users/Wes Mantooth/Documents/CameraShy.exe`
- **Recoverable:** Yes ($R file intact, MFT entry 1590 preserved)

### 5. Steganography Tool Identified
**CameraShy.exe** – Tool used to hide encrypted messages inside GIF images
- Developed by Hacktivismo
- Requires password extraction
- Commonly used for covert communication

### 6. Web Search History (Google – July 12, 2007)
| Search Term | Date |
|-------------|------|
| "atm card stealing" | 2007-07-12 |
| "check washing" | 2007-07-12 |
| "making meth" | 2007-07-12 |

### 7. Xcopy Execution Analysis
- **Prefetch File:** `XCOPY.EXE-8E0707F2.pf`
- **Run Count:** 15 times
- **Last Executed:** `2007-08-24 17:47:34 PKT`
- **Significance:** Bulk file copying – potential data exfiltration

### 8. LNK File Analysis (Selected)
| LNK Filename | Target Path | Status |
|--------------|-------------|--------|
| ATM_THEFTS1.ppt.lnk | E:\Business Ideas\ATM_THEFTS1.ppt | MISSING |
| Bill_Gates.gif.lnk | F:\Pix\Bill_Gates.gif | MISSING |
| Checks.lnk | C:\Users\Wes Mantooth\Documents\Checks | Existing |

### 9. Print Spool Artifacts
- **File:** `prescription.gif` (printed via Epson Stylus Photo RX420)
- **Size:** 245,760 bytes
- **Significance:** Document printed but possibly never saved to disk

## 📁 Repository Structure
