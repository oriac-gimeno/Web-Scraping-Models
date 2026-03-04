# Web Scraping & Word Cloud Generator

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28%2B-FF4B4B?logo=streamlit)](https://streamlit.io/)
[![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-4.12%2B-green)](https://www.crummy.com/software/BeautifulSoup/)
[![WordCloud](https://img.shields.io/badge/WordCloud-1.9%2B-orange)](https://github.com/amueller/word_cloud)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An interactive **Streamlit web application** that generates a **Word Cloud** from the text content of up to five news websites or articles. The app performs web scraping, text cleaning, and visualization, allowing users to download the resulting word cloud as a PNG image.

Originally developed as an individual project for the **IT Academy Data Analytics Reskilling program**, this tool demonstrates a complete pipeline from data extraction to visual output, with a focus on Spanish-language content.

👉 **Live demo:** *[Add your Streamlit Community Cloud URL here, e.g., https://your-app.streamlit.app]*

---

## 📌 Table of Contents

- [✨ Key Features](#-key-features)
- [🛠️ Technologies Used](#️-technologies-used)
- [📦 Installation](#-installation)
- [🚀 Usage](#-usage)
- [📁 Project Structure](#-project-structure)
- [🧠 How It Works](#-how-it-works)
- [⚖️ Legal & Ethical Considerations](#️-legal--ethical-considerations)
- [🔮 Future Improvements](#-future-improvements)
- [📄 License](#-license)
- [📬 Contact](#-contact)

---

## ✨ Key Features

- **Web Scraping**: Extracts visible text from `<p>` (paragraph) tags of up to five user-provided URLs.
- **Smart Text Cleaning**:
  - Removes Spanish stopwords, prepositions, adverbs, and monosyllables.
  - Filters out words with 3 or fewer letters.
  - Strips irrelevant words like "comentarios", "noticia", and the domain name of the source URL.
  - Handles special Unicode characters (`\u200b`, `\xa0`).
- **Interactive Word Cloud Generation**:
  - User selects the maximum number of words to display (via `st.number_input` in the code; currently fixed at 250 in the final version).
  - Visualizes the most frequent terms using `WordCloud` and `matplotlib`.
- **Downloadable Output**: Saves the generated word cloud as a high‑quality PNG file.
- **User‑Friendly Interface**: Built with Streamlit for a smooth, responsive experience.

---

## 🛠️ Technologies Used

| Technology/Library | Purpose |
|--------------------|---------|
| **Python 3.8+** | Core programming language |
| **Streamlit** | Web application framework |
| **Requests** | HTTP requests to fetch web pages |
| **BeautifulSoup (bs4)** | HTML parsing and text extraction |
| **WordCloud** | Generate word cloud images |
| **Matplotlib** | Display the word cloud in the app |
| **re (regex)** | Text cleaning and pattern removal |
| **base64 / io.BytesIO** | Encode image for download |

---

## 📦 Installation

Follow these steps to run the app locally:

1. **Clone the repository:**
   git clone https://github.com/oriac-gimeno/Web-Scraping-Models.git
   cd Web-Scraping-Models
Create and activate a virtual environment (recommended):

bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
Install the required dependencies:

bash
pip install -r requirements.txt
If you don't have a requirements.txt yet, create it with:

text
streamlit
wordcloud
matplotlib
requests
beautifulsoup4
Run the Streamlit app:

bash
streamlit run Webscraping_WordCloud_Streamlit.py
Open your browser at http://localhost:8501 and start exploring.

🚀 Usage
Enter up to five URLs of news sites or articles (in Spanish) in the input fields.

(Optional) The code includes a commented section for setting the number of words – you can uncomment and adjust as needed.

Click the "Generar WordCloud" button.

The app will scrape the text, clean it, and display the resulting word cloud.

Click the "Descarrega el WordCloud" link to download the image as a PNG file.

Example URLs to test:

https://elpais.com/

https://www.elmundo.es/

https://www.lavanguardia.com/

📁 Project Structure
text
Web-Scraping-Models/
├── 📜 README.md                       # This file
├── 📜 Webscraping_WordCloud_Streamlit.py   # Main application script
├── 📜 PràcticaIndividualOriacGimenoFinal.docx.pdf   # Original project documentation (in Catalan)
├── 📜 LICENSE                          # MIT License
├── 📜 requirements.txt                  # Python dependencies (to be created)
└── 📜 .gitignore                        # (optional)
🧠 How It Works
User Input: The app provides five text fields for URLs.

Scraping: For each URL, it sends a GET request with a realistic User-Agent header to avoid blocking. The HTML is parsed with BeautifulSoup, and text is extracted from all <p> tags.

Text Cleaning:

The domain name is removed from the text (to avoid bias).

Spanish stopwords, prepositions, adverbs, and monosyllables are filtered out using predefined sets.

Words of length ≤3 are discarded.

Special characters and irrelevant words (e.g., "comentarios") are eliminated.

Word Cloud Generation: The cleaned text is fed into WordCloud, which counts word frequencies and creates a visual layout.

Display & Download: The word cloud is shown in the Streamlit app. A base64‑encoded download link allows saving the image as PNG.

⚖️ Legal & Ethical Considerations
Respect robots.txt: Always check a website’s robots.txt file and terms of service before scraping.

Rate Limiting: The current version does not implement delays; for multiple or frequent requests, consider adding polite delays.

Personal Use: This tool is intended for educational and personal projects. Do not use it for mass scraping or commercial purposes without permission.

🔮 Future Improvements
✅ Add asynchronous requests to speed up scraping.

✅ Rotate user‑agents and implement proxy support.

✅ Handle pagination for multi‑page articles.

✅ Add Named Entity Recognition (NER) and sentiment analysis.

✅ Allow users to upload custom stopword lists.

✅ Deploy on Streamlit Community Cloud for a live demo.

📄 License
This project is licensed under the MIT License – see the LICENSE file for details.

📬 Contact
GitHub: oriac-gimeno

LinkedIn: Oriac Gimeno

Portfolio: https://oriac-gimeno.github.io/

⭐ If you find this project useful, please consider giving it a star on GitHub!

text
