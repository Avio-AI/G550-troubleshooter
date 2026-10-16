# G550 Troubleshooter

AI-assisted fault isolation for the Gulfstream G550 / GV-SP, grounded in the aircraft's own maintenance data (AMM, FIM, WDM, IPC, TPG, FlightSafety MTM).

- **CAS / fault code**: autocomplete over all 3,733 FIM fault-index entries (message, CMC code, ATA, FIM page). Selected procedures are loaded into the case automatically.
- **Describe the squawk**: free text plus phase of flight, altitude, speed, SAT, cabin altitude / ΔP / rate, observed readings, CMC history, recent maintenance and checks already done.
- **AI troubleshooting chat**: Claude searches the manuals itself (fault index, FIM procedures, BM25 page search, page reads, catalog), builds a ranked differential, recommends the most discriminating next check, and cites every fact. Tap any citation to read that manual page.
- **Search Manuals**: direct keyword search with no AI or API key needed. Works offline after "Download all manuals" in Settings.
- Cases are saved on the device and can be exported as Markdown for the work order.

## Architecture

This repo holds only the app (one static `index.html`) and contains **no manual content**. The manual index lives in a separate **private** repo (`G550-Manual-Data`). The app reads it through the GitHub API with a read-only token entered on the device. AI calls go straight from the browser to `api.anthropic.com` with your own API key. There is no server.

## Setup

1. **Pages**: Settings → Pages → Deploy from branch → `main` / root. The app runs at `https://<owner>.github.io/<repo>/`.
2. **Token**: GitHub → Settings → Developer settings → Fine-grained tokens → new token. Set Repository access to *Only* `G550-Manual-Data` and Permissions to **Contents: Read-only**.
3. Open the app → ⚙ Settings: enter the Anthropic API key, the data repo (`Avio-AI/G550-Manual-Data`), and the token.
4. On a phone, use "Add to Home Screen" for full-screen use.

## Notes

- Keys are stored only in that browser's local storage (untick "Remember" on shared devices). Anyone with your Anthropic key can spend on your account: use a key with a spend limit.
- Decision aid only. The current revision of the approved maintenance data governs all maintenance and return-to-service actions.
- Library: AMM Rev 41, FIM Rev 30, WDM Rev 33, IPC Rev 41, TPG Rev 28, FSI MTM. Known gaps are listed in Settings.
