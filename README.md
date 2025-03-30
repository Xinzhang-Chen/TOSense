<img width="1113" alt="TOSense Logo" src="https://github.com/user-attachments/assets/356a6ff6-9d96-4e1c-95da-ee0418ab2d6d" />

# TOSense – We Read, You Click


**TOSense** is a Chrome browser extension that demonstrates a proof-of-concept workflow for analyzing website Terms of Service (TOS) using a large language model (LLM). It enables basic LLM-powered interaction with TOS content, designed for academic exploration, prototyping, and feedback-driven development.

TOSense is part of the following research paper:

> **"ToSense: We Read, You Click"**\
> *Xinzhang Chen, Hassan Ali, Arash Shaghaghi, Salil S. Kanhere, Sanjay Jha*\
> *Under review at IEEE/IFIP DSN 2025*

> ⚠️ This is a **proof-of-concept** version. The current release focuses on demonstrating the workflow and integration with an external server hosting our LLM backend.

---

## ✨ Key Features

- 🧠 Simple LLM-based interface for querying Terms of Service
- 🔄 Communicates with a backend server to demonstrate the TOS-to-LLM pipeline
- 🛠️ Ideal for research demonstrations and future feature prototyping

---

## 🚀 Installation

### 📺 Installation Video  

https://github.com/user-attachments/assets/f47141f4-f1ca-42b9-a3ff-69ac477b2c8f





### Manual Installation Steps

1. Clone or download this repository.
2. Open [chrome://extensions](chrome://extensions) in your browser.
3. Enable **Developer mode** (top right corner).
4. Click **Load unpacked** and select the `chrome-mv3-prod` folder from this repo.
5. You should see **TOSense** appear in your extension bar.

---

## ℹ️ How to Use

### 📺 Usage Demo

https://github.com/user-attachments/assets/67a9b9cc-6e47-41c1-a8fa-96fbdab6213c



1. Open a new tab inside your browser (a landing page also works).
2. Click the **TOSense** extension icon (if it is hidden [by default], you need to click the extension icon first).
3. Enter a question or select a pre-configured question (e.g., “Can I permanently delete my account and data?”).
4. Send the question.
5. View the LLM-generated response in the popup interface.

> ⚠️ The current server is hosted on a low-spec personal machine. Expect possible delays or limited performance in LLM responses.

> ⚠️ Please note that the provided version will not use the ToS content extract from the current page; all the answers returned from the server will base on our pre-loaded
> LinkedIn ToS document. (Due to computing power limitations)

---

## 🧠 Architecture Overview

```txt
┌────────────┐     Sends Request (User Prompt)     ┌────────────┐
│  TOSense   ├────────────────────────────────────►│   Backend  │
│  (Chrome)  │◄────────────────────────────────────┤   Server   │
└────────────┘        Returns Response             └────────────┘
       │                                                  ▲
       └─ Page Context [❌ Not supported in this version]─┘

```

---

## 🛑 Current Limitations

- ❌ Does not detect or extract TOS from arbitrary web pages (but we already have the key component; more info checkout [tos-crawl](https://github.com/Xinzhang-Chen/tos-crawl))
- ❌ Does not provide fast access to pre-crawled TOS repositories
- 🐢 It relies on a low-powered backend for LLM responses
- 🌐 LLM model is a reduced version for performance reasons

These will be addressed in future versions.

---

## 📄 License

This project is licensed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**.  
See the [LICENSE](../LICENSE) file for more information.

---

## ⚠️ Disclaimer

This tool is provided solely for **non-commercial, academic research, and demonstration** purposes. The maintainers do not guarantee the performance, uptime, or accuracy of the LLM responses, especially under heavy usage.

> Users are responsible for complying with applicable laws and website terms of service.

---

## 👩‍💻 Maintainer

- Xinzhang Chen - xinzhang.chen@unsw.edu.au
- Hassan Ali - hassan.ali@unsw.edu.au
- Dr Arash Shaghaghi - a.shaghaghi@unsw.edu.au

🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧

This project is under **active development** 🛠️.

New features and improvements are being added continuously. **Stay tuned!**
