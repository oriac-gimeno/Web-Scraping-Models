# Web Scraping & Word Cloud Generator

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28%2B-FF4B4B?logo=streamlit)](https://streamlit.io/)
[![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-4.12%2B-green)](https://www.crummy.com/software/BeautifulSoup/)
[![WordCloud](https://img.shields.io/badge/WordCloud-1.9%2B-orange)](https://github.com/amueller/word_cloud)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](License.md)

An interactive **Streamlit web application** that generates a **Word Cloud** from the text content of up to five news websites or articles. The app performs text extraction, cleaning, and visualization, and lets the user download the result as a PNG image.

Originally developed as an individual project for the **IT Academy Data Analytics Reskilling program**, it demonstrates a complete pipeline from data extraction to visual output, with a focus on Spanish-language content.

Runs locally. See [Installation](#-installation).

---

## 🖼️ Screenshots

The same news article read twice, with the word limit set to 150 and to 25. A high limit gives the texture of the piece; a low one leaves only what it is really about.

<p align="center">
  <img src="https://github.com/user-attachments/assets/ea49f199-601f-40b7-ba49-05b2364af5f9" alt="Word cloud from a news article with the limit set to 150 words" width="330">
  &nbsp;&nbsp;
  <img src="https://github.com/user-attachments/assets/0114ba04-59c6-4707-9de7-3708dd9ac17e" alt="The same article with the limit set to 25 words" width="330">
</p>

---

## 📌 Table of Contents

- [✨ Key Features](#-key-features)
- [🖼️ Screenshots](#️-screenshots)
- [🛠️ Technologies Used](#️-technologies-used)
- [📦 Installation](#-installation)
- [🚀 Usage](#-usage)
- [📁 Project Structure](#-project-structure)
- [🧠 How It Works](#-how-it-works)
- [⚖️ Legal & Ethical Considerations](#️-legal--ethical-considerations)
- [🔮 Possible Improvements](#-possible-improvements)
- [📄 License](#-license)
- [📬 Contact](#-contact)

---

## ✨ Key Features

- **Text extraction**: reads the visible text of `<p>` tags from up to five user-provided URLs.
- **Smart text cleaning**:
  - Removes Spanish stopwords, prepositions, adverbs and monosyllables.
  - Filters out words of three letters or fewer.
  - Strips irrelevant words such as "comentarios" or "noticia", and the domain name of the source URL.
  - Handles special Unicode characters (zero-width space, non-breaking space).
- **Word cloud generation**:
  - Renders the most frequent terms with `WordCloud` and `matplotlib`.
  - The user sets how many words to display.
- **Downloadable output**: saves the word cloud as a PNG file.
- **Streamlit interface**: five URL fields, one button, immediate result.

---

## 🛠️ Technologies Used

| Technology / Library | Purpose |
|---|---|
| **Python 3.8+** | Core programming language |
| **Streamlit** | Web application framework |
| **Requests** | HTTP requests to fetch web pages |
| **BeautifulSoup (bs4)** | HTML parsing and text extraction |
| **WordCloud** | Generate word cloud images |
| **Matplotlib** | Display the word cloud in the app |
| **re (regex)** | Text cleaning and pattern removal |
| **base64 / io.BytesIO** | Encode the image for download |

---

## 📦 Installation

**1. Clone the repository**

```bash
git clone https://github.com/oriac-gimeno/Web-Scraping-Models.git
cd Web-Scraping-Models
```

**2. Create and activate a virtual environment** (recommended)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

**3. Install the dependencies**

```bash
pip install -r requirements.txt
```

**4. Run the app**

```bash
streamlit run Webscraping_WordCloud_Streamlit.py
```

Then open `http://localhost:8501`.

---

## 🚀 Usage

1. Enter up to five URLs of Spanish-language news sites or articles.
2. Set how many words the cloud should show. A low number surfaces the dominant terms, a high number gives the texture of the piece.
3. Click **Generar WordCloud**.
4. The app fetches the text, cleans it and displays the word cloud.
5. Click **Descarrega el WordCloud** to download it as a PNG.

Sites to try:

```text
https://elpais.com/
https://www.elmundo.es/
https://www.lavanguardia.com/
```

A URL can come back empty. Paywalls, cookie walls and pages that build their text in the browser all produce a page with no usable `<p>` content, and the app has no way around that by design.

---

## 📁 Project Structure

```text
Web-Scraping-Models/
├── README.md                                    This file
├── Webscraping_WordCloud_Streamlit.py           Main application script
├── PràcticaIndividualOriacGimenoFinal.docx.pdf  Original project documentation (Catalan)
├── requirements.txt                             Python dependencies
└── License.md                                   MIT License
```

---

## 🧠 How It Works

1. **User input**: five text fields for URLs.
2. **Fetching**: one GET request per URL, sending a browser user agent. Many news sites return nothing usable without one. This is a deliberate compromise and it is discussed in [Legal & Ethical Considerations](#️-legal--ethical-considerations). The HTML is parsed with BeautifulSoup and the text of every `<p>` tag is extracted.
3. **Text cleaning**:
   - The domain name is removed from the text to avoid bias.
   - Spanish stopwords, prepositions, adverbs and monosyllables are filtered out.
   - Words of three letters or fewer are discarded.
   - Special characters and irrelevant words are removed.
4. **Word cloud generation**: the cleaned text is passed to `WordCloud`, which counts frequencies and lays out the image.
5. **Display and download**: the image is shown in Streamlit and offered as a base64 PNG download.

---

## ⚖️ Legal & Ethical Considerations

What this project does is deliberately narrow. It reads the visible paragraph text of up to five URLs the user types, one request each, with no crawling, no link following and no rate pressure. It fetches pages that the person at the keyboard could have opened in five browser tabs.

It sends a browser user agent. Without one, many news sites return nothing usable, so the exercise would not run at all. That is worth naming rather than glossing over: a request that presents itself as a browser takes away the site's ability to tell automated traffic from a visitor, and a site that cannot tell cannot decide. At one request per URL, started by a person, for a classroom exercise, I consider that acceptable. At any scale where it would matter, I do not.

Which is why the roadmap below has no user agent rotation and no proxy support. Those are not performance features, they are ways of staying ahead of a site's ability to say no, and they are the line between reading a page and evading a decision.

Outside a classroom I do not use this approach at all. The tools I run in production take their data from official APIs, public feeds and files the user uploads themselves. Where a source would have required scraping or disguising a user agent, I dropped the source instead, and every one of those decisions is written down.

Knowing how to extract data from a page, and knowing where you stop, are different skills. This repository shows the first one. The production tools show the second.

Before scraping anything, read the site's `robots.txt` and its terms of service.

---

## 🔮 Possible Improvements

- Read and honour `robots.txt` before fetching, and skip any URL that disallows it.
- Asynchronous requests, with a polite delay between them.
- Handle pagination for multi-page articles.
- Named Entity Recognition and sentiment analysis.
- Let users upload custom stopword lists.

---

## 📄 License

MIT. See [License.md](License.md).

---

## 📬 Contact

- Website: [oriacgimeno.com](https://oriacgimeno.com)
- LinkedIn: [Oriac Gimeno](https://www.linkedin.com/in/oriacgimeno)
- GitHub: [oriac-gimeno](https://github.com/oriac-gimeno)
- Portfolio: [oriac-gimeno.github.io](https://oriac-gimeno.github.io/)
