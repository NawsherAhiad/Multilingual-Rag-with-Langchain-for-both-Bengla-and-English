# 📚 Bangla and English RAG QA App

A Bengali Question Answering app powered by **LangChain**, **FAISS**, **Hugging Face Embeddings**, and **Google Gemini**. The app reads text from `ocr_output.txt`, chunks it, creates vector embeddings, and answers questions in Bengali using retrieved context.

---

## 🌟 Features

- ✅ Supports Bengali questions and answers
- ✅ Custom hybrid retrieval (keyword + vector search)
- ✅ Uses Google Gemini (via LangChain) for answering
- ✅ Streamlit interface for easy interaction

---

## 🧰 Requirements

- Python 3.9 to 3.11
- Google Gemini API key
- pip, virtualenv (optional but recommended)

---

## 🏗️ Setup Instructions
2. Create and activate a virtual environment
On Windows:

python -m venv env
env\Scripts\activate

On macOS/Linux:
python3 -m venv env
source env/bin/activate


3. Install required packages
pip install --upgrade pip
pip install -r requirements.txt


4. Prepare your text data
Place your Bengali OCR or input text into a file called:
ocr_output.txt


5. Download NLTK data
Run once:
python -c "import nltk; nltk.download('punkt')"


6. Set your Google Gemini API Key
.env file
Create a .env file:
GOOGLE_API_KEY=your-api-key

Load it in your Python code:
from dotenv import load_dotenv
load_dotenv()



🧠 Build the Vector Index (Run Once)
python build_faiss_index.py

🛠️ Extra Setup Notes
Install Tesseract-OCR binary
Required for pytesseract. On Windows:

Download: https://github.com/UB-Mannheim/tesseract/wiki

Add install path (e.g. C:\Program Files\Tesseract-OCR) to PATH.

Tesseract language packs (for Bangla)
Make sure ben.traineddata is in the tessdata folder.

PDF2Image dependency
Install Poppler binary:

Windows: https://github.com/oschwartz10612/poppler-windows/releases

Add poppler/bin/ to PATH.



### 1. Clone the repository


git clone https://github.com/yourusername/bangla-rag-app.git
cd bangla-rag-app




🚀 Run the App
bash
Copy code
streamlit run app.py
Open http://localhost:8501 in your browser.

🧪 Example Query
অনুপমের ভাষায় সুপুরুষ কাকে বলা হয়েছ?
Expected Answer:
শুম্ভনাথ


📦 Project Structure
bash
Copy code
bangla-rag-app/
├── app.py                  # Streamlit frontend
├── build_faiss_index.py    # One-time vector builder
├── preprocess_recursive.py # Chunking and cleaning logic
├── ocr_output.txt          # Input Bengali text
├── faiss_multilingual/     # Vector index (auto-generated)
└── README.md


📌 To Do
 Add PDF upload
 Deploy on Streamlit Cloud or Render
 Add question history sidebar
 Improve MCQ extraction


Answering following Questions
 
○ What method or library did you use to extract the text, and why? Did you face 
any formatting challenges with the PDF content?
    ans: I used OCR to extract data from the given pdf as it has unicode issues. PyPDFLoader, PYmuPDFLoader,
         and PyPDF2 didn't work so I go for OCR, using pdf2image, pytesseract.
  
○ What chunking strategy did you choose (e.g. paragraph-based, 
sentence-based, character limit)? Why do you think it works well for semantic 
retrieval?
    ans: Recursive character-based chunking with a fixed character limit and overlap. before doing that, I classified by pdf contents
         such as MCQs, paragraph, author inroduction, lesson introduction etc, I think it works well as The RecursiveCharacterTextSplitter
         tries to split text first on natural boundaries (e.g., paragraphs or sentences) before falling back to smaller units and Sentence Transformers
        (like paraphrase-multilingual-MiniLM) work best with inputs of ~512 tokens.

○ What embedding model did you use? Why did you choose it? How does it 
capture the meaning of the text?
    ans: I used the "sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2" embedding model. as it support multiple language,
         its compact yet powerful, built on MiniLM, it’s lightweight and fast while still delivering strong semantic performance.
         For Paraphrase Training, The model is fine-tuned on paraphrase mining and semantic textual similarity tasks, making it ideal for capturing meaning across different phrasings.

○ How are you comparing the query with your stored chunks? Why did you 
choose this similarity method and storage setup?
    ans: i didnt set up any
  
○ How do you ensure that the question and the document chunks are compared 
meaningfully? What would happen if the query is vague or missing context?
    ans: Im also looking for the answer.



○ Do the results seem relevant? If not, what might improve them (e.g. better 
chunking, better embedding model, larger document)?
    ans: I dont see the results are relevent. I beleive better chunking with better clusification will improve a lot initially. 

---
## 📜 License
MIT License. Free to use and modify.

## ✨ Author
Developed by Md. Ahied Mahi Chowdhury
Inspired by LangChain + Gemini for Bengali NLP 🚀
