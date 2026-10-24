# لمحة · Lamha

**صحتك بلمحة · Your health, at a glance.**
A remote health check-in that turns a laptop or phone camera into a measuring tool: 30 seconds, no devices, and it keeps working offline.

**Live:** https://kurdim12.github.io/lamha/ · Patient `#patient` · Doctor `#doctor` · Partner center `#facility`

Hacktoberfest 2026 · Digital Health & Wellness track.

## What it does

1. **Silent 30-second measurement.** Heart rate comes from the camera with rPPG: MediaPipe Face Landmarker picks forehead and cheek regions, then the POS algorithm, a 0.7–3.0 Hz band-pass, and FFT plus peak counting. Each reading has a signal-quality index (SQI); below the threshold the answer is "remeasure", never a guess. Respiratory rate (estimated) and RMSSD are shown only relative to the patient's own baseline.
2. **«احكيلي».** The patient describes symptoms in Jordanian Arabic through the Web Speech API (`ar-JO`), typing, or the demo scripts. A deterministic dialect glossary fills the Extraction schema. Optional Qwen3-32B via Groq never overrides the rules.
3. **Triage.** Red flags, then NEWS2-inspired pulse and respiration points, then a quality gate. Deterministic rules always win.
4. **Report.** Written in Jordanian Arabic and readable aloud. Advice comes only from vetted advice cards (with a dose guard), plus a QR code for the doctor and a print-ready layout.
5. **Emergency.** 911 appears first. With consent, the nearest partner center gets an alert; it acknowledges with «استلمنا», and after 3 minutes without an ack the alert escalates to the next partner.
6. **Doctor dashboard.** A priority queue, a code-generated pre-visit note, and a Patient Health Forecast: median+MAD baseline, CUSUM, and a 48-hour linear trend with an 80% prediction interval.

## Run it

Open `index.html` in Chrome, or use the live link above. Camera and mic need HTTPS or a local file. Load the page once while online so the libraries and the face model get cached, then cut the internet and it keeps working. Only browser speech-to-text needs a connection; use typing or the demo scripts offline.

## Privacy

Video and audio never leave the device and are never stored. Only numbers and structured symptoms are kept, in this browser's localStorage, under a pseudonymous ID. The partner centers and the patient «أبو محمد» are synthetic demo data. Nothing calls 911 or any real hospital.

**Not a medical device and not a diagnosis.** Lamha is a triage and early-warning aid; the decision always belongs to a clinician.

## License

Apache-2.0. Open models and libraries: MediaPipe Tasks Vision (Apache-2.0), Chart.js (MIT), qrcodejs (MIT), optional Qwen3 (Apache-2.0).
