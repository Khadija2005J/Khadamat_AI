# Khadamat AI

**A bilingual (French / Moroccan Darija) AI assistant for Moroccan administrative procedures.**

Ask a question by text or voice, get an answer grounded in a curated knowledge base of Moroccan administrative services, find the nearest administrative office, and check that your file (dossier) is complete before you go.

## Features

- **Ask in French or Darija** – text or voice input; answers can be read aloud.
- **Retrieval-Augmented Generation (RAG)** – answers are grounded in `morocco_admin_dataset.md` using multilingual embeddings and a FAISS vector index, then phrased by Google Gemini.
- **Voice** – speech-to-text with Google Speech Recognition (`ar-MA` and `fr-FR`), text-to-speech with ElevenLabs or gTTS as a fallback.
- **Document analysis** – upload an administrative document and ask questions about it.
- **Nearby offices** – geocode an address and list the closest administrative centers.
- **Dossier verification & QR code** – check which documents are missing for a procedure and generate a QR code summary.

## Tech stack

| Layer | Tools |
|-------|-------|
| UI | Streamlit |
| API (optional) | FastAPI + Uvicorn (`/ask-text/`, `/ask-audio/`) |
| RAG | LangChain, FAISS, `paraphrase-multilingual-MiniLM-L12-v2` embeddings |
| LLM | Google Gemini (`langchain-google-genai`) |
| Voice | SpeechRecognition, ElevenLabs, gTTS |
| Location | geopy |

## Project structure

```
Khadamat_AI/
├── app.py                     # Streamlit application
├── morocco_admin_dataset.md   # Knowledge base used by the RAG engine
└── backend/
    ├── main.py                # FastAPI endpoints
    ├── rag_engine.py          # Embeddings, FAISS index, Gemini chain
    ├── voice_processor.py     # Speech-to-text and text-to-speech
    ├── location_service.py    # Geocoding and nearby centers
    ├── requirements.txt
    └── .env.example
```

## Getting started

**Prerequisites:** Python 3.10+, a microphone for voice input, and API keys for Google Gemini (required) and ElevenLabs (optional).

```bash
git clone https://github.com/Khadija2005J/Khadamat_AI.git
cd Khadamat_AI

python -m venv venv
# Windows: venv\Scripts\activate   |   macOS/Linux: source venv/bin/activate
pip install -r backend/requirements.txt

cp backend/.env.example backend/.env   # then add your keys
streamlit run app.py
```

### Environment variables

| Variable | Required | Purpose |
|----------|----------|---------|
| `GOOGLE_API_KEY` | Yes | Gemini language model |
| `HUGGINGFACEHUB_API_TOKEN` | No | Hugging Face endpoint fallback |
| `ELEVENLABS_API_KEY` | No | Natural voice output (gTTS is used otherwise) |

## Author

Khadija Alaoui Mrani – [GitHub](https://github.com/Khadija2005J)
