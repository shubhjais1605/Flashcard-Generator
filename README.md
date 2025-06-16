
#  AI Flashcard Generator



> 📘 A lightweight, LLM-powered tool to convert educational content into flashcards.

---


---
## 🖼️ UI Screenshots

![Screenshot 2025-07-16 205813](Screenshot (17).png)

![Screenshot 2025-07-16 205832](Screenshot (18).png)

![Screenshot 2025-07-16 210126](Screenshot (20).png)

---

## 📑 Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Setup and Installation](#setup-and-installation)
- [How to Run](#how-to-run)
- [Sample Execution](#sample-execution)
- [Design Decisions & Prompt Engineering](#design-decisions--prompt-engineering)
- [Project Structure](#project-structure)
- [Future Work](#future-work)

---

## 🚀 Project Overview

This tool streamlines the study process by automatically generating flashcards from educational content such as textbook chapters, lecture notes, or articles.

Built with **Streamlit** and powered by **Zephyr-7B-β** (via Hugging Face), it offers an intuitive UI and delivers clean, structured Q&A flashcards that can be exported to **Quizlet** or **CSV**.

---

## ✅ Features

### 🔹 Core Features

- ✅ **Multiple Content Inputs** – Paste text or upload `.txt` / `.pdf` files.
- ✅ **LLM-Powered Generation** – Generate a custom number of flashcards using Zephyr-7B.
- ✅ **Interactive UI** – Streamlit-based frontend for simplicity and clarity.
- ✅ **Subject-Specific Context** – Optional subject selection improves relevance.

### 🔸 Bonus Features

- ✅ **Quizlet Export** – Download in `.txt` format (tab-separated).
- ✅ **CSV Export** – Download a `.csv` file of generated flashcards.
- ✅ **Robust JSON Parsing** – Handles minor LLM output errors for stable performance.

---

## 🛠️ Tech Stack

| Layer              | Tools / Libraries |
|-------------------|-------------------|
| Language           | Python            |
| UI Framework       | Streamlit         |
| Model              | Zephyr-7B-β via Hugging Face Inference API |
| Text Processing    | PyMuPDF (fitz)    |
| Data Handling      | pandas            |
| JSON Parsing       | demjson3          |
| HTTP Requests      | requests          |

---

## 🧰 Setup and Installation

### 1. Clone the Repository

```bash
git clone https://github.com/shubhjais1605/Flashcard-Generator
cd FlashCard-Generator
```

---

### 2. Create and Activate Virtual Environment

**For Unix/macOS:**
```bash
python3 -m venv venv
source venv/bin/activate
```

**For Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 4. Get Your Hugging Face API Token

- Visit [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens) and generate a **User Access Token** (with write permissions).
- You’ll be prompted to paste this token into the Streamlit sidebar during app usage.

---

## ▶️ How to Run

```bash
streamlit run app.py
```

- Visit the local URL shown (usually `http://localhost:8501`) to access the app.

---

## 🧪 Sample Execution

### 🔹 Input Text

```
Photosynthesis is a process used by plants, algae, and certain bacteria to convert light energy into chemical energy...
```

### 🔹 Sample Flashcards (JSON)

```json
[
  {
    "question": "What are the two stages of photosynthesis?",
    "answer": "The two stages are the light-dependent reactions and the light-independent reactions (Calvin cycle)."
  },
  {
    "question": "Where do the light-dependent reactions occur?",
    "answer": "They occur in the thylakoid membranes of chloroplasts."
  }
]
```

---

### 🔹 Export Files

**quizlet_import.txt**

```
Where do the light-dependent reactions occur?    They occur in the thylakoid membranes of chloroplasts.
```

**flashcards.csv**

```csv
question,answer
Where do the light-dependent reactions occur?,They occur in the thylakoid membranes of chloroplasts.
```

## 🧠 Design Decisions & Prompt Engineering

### 🔸 Why Zephyr-7B-β?

- Instruction-tuned for Q&A tasks  
- Efficient and open-source  
- Easy integration with Hugging Face Inference API  

---

### 🔸 Prompt Engineering Strategy

Prompt used in `llm_handler_hf.py`:

```python
prompt = f"""<|system|>
You are an expert flashcard creator. Your task is to generate exactly {num_cards} question-answer flashcards based on the provided text.
Your entire response MUST be a single, valid JSON list of objects. Each object must have a "question" key and an "answer" key.
Do not add any introduction, explanation, or any text outside of the main JSON list.
Your response must start with '[' and end with ']'.</s>
<|user|>
Generate flashcards for the following text on the subject of '{subject}':
---
{text}
---</s>
<|assistant|>
"""
```

---

### 🔸 JSON Cleanup Handling

- `fix_json_format()` strips out extra text or missing brackets.  
- Uses `demjson3` for lenient parsing.  
- Robust error handling for API failures, timeouts, and decoding issues.  

---

## 📁 Project Structure

```
.
├── app.py              # Main Streamlit UI
├── llm_handler_hf.py   # Hugging Face API & prompt logic
├── requirements.txt    # Dependency list
├── .gitignore          # Files to ignore in Git
├── .env.example        # Example for API token handling
└── README.md           # You're reading it!
```

---

## 🔮 Future Work

- 📝 **Flashcard Editor** – Let users edit flashcards before exporting.  
- 📦 **Anki Export** – Add `.apkg` support via `genanki`.  
- 🧠 **Topic Clustering** – Group questions by sub-topic or difficulty.  
- 🚀 **Public Deployment** – Host on Streamlit Cloud or Hugging Face Spaces.  
- 🌐 **Multi-language Support** – Generate flashcards in different languages.  

---




