<img width="1113" alt="TOSense Logo" src="https://github.com/user-attachments/assets/356a6ff6-9d96-4e1c-95da-ee0418ab2d6d" />

# TOSense – We Read, You Click


**TOSense** is a Chrome browser extension that demonstrates a proof-of-concept workflow for analyzing website Terms of Service (TOS) using a large language model (LLM). It enables basic LLM-powered interaction with TOS content, designed for academic exploration, prototyping, and feedback-driven development.

TOSense is part of the following research papers:

> **"TOSense: We Read, You Click"**\
> *Xinzhang Chen, Hassan Ali, Arash Shaghaghi, Salil S. Kanhere, Sanjay Jha*\
> IEEE/IFIP DSN (Dependable Systems and Networks) 2025 — [IEEE Xplore abstract](https://ieeexplore.ieee.org/abstract/document/11068347)

> **"Demo: TOSense – What Did You Just Agree to?"**\
> *Xinzhang Chen, Hassan Ali, Arash Shaghaghi, Salil S. Kanhere, Sanjay Jha*\
> IEEE LCN (Local Computer Networks) 2025 — [IEEE Xplore abstract](https://ieeexplore.ieee.org/abstract/document/11146330)

> ⚠️ This is a **proof-of-concept** version. The current release focuses on demonstrating the workflow and integration with an external server hosting our LLM backend.

---

## ✨ Key Features

- Simple LLM-based interface for querying Terms of Service
- **On-page ToS link detection** using `tosLinkScorer`
- Communicates with a backend server to demonstrate the TOS-to-LLM pipeline
- Ideal for research demonstrations and future feature prototyping

---

## 🚀 Installation

### Installation Video  

https://github.com/user-attachments/assets/f47141f4-f1ca-42b9-a3ff-69ac477b2c8f





### Manual Installation Steps

1. Clone or download this repository.
2. Open [chrome://extensions](chrome://extensions) in your browser.
3. Enable **Developer mode** (top right corner).
4. Click **Load unpacked** and select the `chrome-mv3-prod` folder from this repo.
5. You should see **TOSense** appear in your extension bar.

---

## ℹ️ How to Use

### Usage Demo

https://github.com/user-attachments/assets/67a9b9cc-6e47-41c1-a8fa-96fbdab6213c



1. Open a new tab inside your browser (a landing page also works).
2. Click the **TOSense** extension icon (if it is hidden [by default], you need to click the extension icon first).
3. Enter a question or select a pre-configured question (e.g., “Can I permanently delete my account and data?”).
4. Send the question.
5. View the LLM-generated response in the popup interface.

> ⚠️ The current server is hosted on a low-spec testing server. Expect possible delays or limited performance in LLM responses. Server will be adjusted in the next iteration.

---

## Architecture Overview

```txt
          ┌──────────────────────┐
          │  Web Page (DOM)      │
          │  <a> … footer/nav …  │
          └──────────┬───────────┘
                     │
                     │  tosLinkScorer
                     │  (rank likely ToS links)
                     ▼
┌──────────────┐     popup UI      ┌───────────────┐
│  TOSense     │──────────────────►│   Backend     │
│  Extension   │   query / queue   │   Server      │
└──────────────┘                   └───────────────┘

```
- The extension does client-side scoring to find candidate legal pages.
- All Q&A and indexing happen in a single Backend.

---

## 🔎 `tosLinkScorer` (overview)

A lightweight, explainable heuristic that ranks links most likely to be ToS/Privacy/Legal.

**Signals & Weights**
- **Positive (+):** `pathExact` (+6), `pathContains` (+4), `textExact` (+5), `textContains` (+3), `ariaOrTitle` (+2), `footer` (+2), `headerOrNav` (+1), `query` (+1)  
- **Negative (–):** `promo` (–5), `refund` (–4), `careersBlog` (–3), `badExt` (–2), `dateLike` (–1)  
- **Threshold:** `WEIGHTS.threshold = 10` (links below this are discarded)

**How it matches**
- **Path exact:** strict match on fixed slugs (e.g., `/terms-of-service`, `/privacy-policy`); *no “and/&” flexibility here*.  
- **Path contains / anchor text / aria-title / query:** flexible regex tolerates spacing and **“and/&”** variants (e.g., `terms[ *](and|&)[ *]conditions`).  
- **Placement boosts:** adds `+2` if in **footer**, else `+1` if in **header/nav** (mutually exclusive).

**Negatives**
- `promo`, `refund`, `careersBlog`: penalize if matched in path or text.  
- `badExt`: penalize if URL path ends with unwanted extensions (pdf/docx/pptx).  
- `dateLike`: small penalty if path or text looks like a date.  

**Per-page selection**
1. Score every `<a href>`.  
2. Keep the **highest score per URL with hash removed**.  
3. Filter by threshold → sort desc → return **top-N** (default 5) as `{ href, text, score, breakdown }`.  

---

## 🛑 Current Limitations

- **No crawling/indexing inside the extension**: discovery is client-side; extraction and embeddings run on an external backend (see [tos-crawl](https://github.com/Xinzhang-Chen/tos-crawl)).
- **Backend capacity & model size**: current demo backend is low-powered and uses a reduced LLM, which may affect speed and answer quality.
- **Content variability**: geo/language gates, PDFs, and heavy client-side rendering can degrade backend extraction quality.

_Planned work will address these limitations in subsequent iterations._

---


## ⚠️ Disclaimer

This tool is provided solely for **non-commercial, academic research, and demonstration** purposes. The maintainers do not guarantee the performance, uptime, or accuracy of the LLM responses, especially under heavy usage.

> Users are responsible for complying with applicable laws and the website's terms of service.

---

## 📄 License

This project is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**.  
See the [LICENSE](./LICENSE) file for more information.

---

## 👩‍💻 Maintainer

- Xinzhang Chen - xinzhang.chen@unsw.edu.au
- Hassan Ali - hassan.ali@unsw.edu.au
- Dr Arash Shaghaghi - a.shaghaghi@unsw.edu.au

🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧

This project is under **active development** 🛠️.

New features and improvements are being added continuously. **Stay tuned!**
