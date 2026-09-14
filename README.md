## Vũ Duy Khang

First-year Information Security student at PTIT Ho Chi Minh City, on the
blockchain track. I spend most of my time on smart contract security.

I have been around crypto since 2022, which is where the interest came from:
I wanted to understand why so many token contracts turn out to be traps.

### What I am working on

**[smart-contract-security-lab](https://github.com/Vuduykhang2306/smart-contract-security-lab)**
— an audit carried out end to end. A tax token with eight findings in it, a
runnable Foundry PoC for each, a full report, the patched contract, and a retest
suite. 20 tests, CI on every push. The report is
[here](https://github.com/Vuduykhang2306/smart-contract-security-lab/blob/main/reports/2026-09_MemeTax_audit-report.md);
the two findings worth your time are M-01 and M-02.

Next up, tracked as issues on that repo: a Foundry invariant suite, the same
properties under Echidna, and an Anchor lab to put real PoCs behind my Solana
checklist.

### Elsewhere

- **[aquaoracle-app](https://github.com/Vuduykhang2306/aquaoracle-app)** and
  **[Esp32_AquaOracle_Programm](https://github.com/Vuduykhang2306/Esp32_AquaOracle_Programm)**
  — IoT water-quality monitoring for aquaculture: ESP32 sensor node, Supabase,
  a PatchTST forecasting model, Flutter app. Took it to the national final of
  the Vietnam Youth Innovation Contest 2026.
- CTF, mostly cryptography. Top 13 in Vietnam on CyberTalents; captain of
  C0mt4m367 and of meobeo.

### A note on the older repos here

Several of them used to have Supabase and Gemini keys committed in the source,
plus a Wi-Fi password in the ESP32 firmware. I found them while reviewing my own
account, rewrote the history to remove them, and moved every project to
gitignored config files. The keys were already dead by then, but that is luck,
not a process. Writeup of what I missed on the first pass is in
[the lab's notes](https://github.com/Vuduykhang2306/smart-contract-security-lab/blob/main/docs/notes.md).

Auditing other people's contracts and not auditing your own is not a position
you can hold for long.

### Contact

vuduykhang23062008@gmail.com — open to Smart Contract Auditor internships,
Ho Chi Minh City or remote.
