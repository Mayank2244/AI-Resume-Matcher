# 🏗️ AI Resume Matcher - Architecture Diagram

## System Architecture

```mermaid
graph TB
    subgraph Frontend["🎨 Frontend Layer"]
        Index["index.html<br/>Upload Interface"]
        Extract["extract.html<br/>Results Display"]
        Download["download_form.html<br/>Download Manager"]
    end

    subgraph API["🔌 FastAPI Backend"]
        Main["main.py<br/>FastAPI App"]
        Routes["HTTP Routes<br/>GET / POST"]
    end

    subgraph Processing["⚙️ Processing Pipeline"]
        Parser["resume_parser.py<br/>PDF Extraction"]
        Preprocess["preprocess.py<br/>Text Cleaning"]
        Extract_Text["Text Extraction<br/>& NLP"]
    end

    subgraph Matchers["🧠 Matching Engines"]
        GPT["gpt_matcher.py<br/>Groq AI Matching"]
        Cosine["cosine_matcher.py<br/>TF-IDF Similarity"]
        Keyword["key_matcher.py<br/>Keyword Analysis"]
        Hybrid["hybrid_matcher.py<br/>Combined Scoring"]
    end

    subgraph External["☁️ External Services"]
        Groq["Groq API<br/>llama-3.1-8b-instant"]
        SpaCy["spaCy NLP<br/>en_core_web_sm"]
        SKLearn["scikit-learn<br/>TF-IDF Vectorizer"]
    end

    subgraph Storage["💾 Data Layer"]
        Uploads["uploads/<br/>PDF Files"]
        Results["Results Data<br/>Scores & Matches"]
    end

    subgraph Config["⚙️ Configuration"]
        Env[".env<br/>GROQ_API_KEY"]
        Requirements["requirements.txt<br/>Dependencies"]
    end

    User["👤 User"]
    
    User -->|Upload Resumes| Index
    User -->|View Results| Extract
    User -->|Download| Download
    
    Index -->|Submit| Routes
    Routes -->|Process| Main
    
    Main -->|Parse PDFs| Parser
    Parser -->|Extract Text| Preprocess
    Preprocess -->|Clean & Tokenize| Extract_Text
    
    Main -->|Select Method| Matchers
    
    GPT -->|API Call| Groq
    Cosine -->|Analyze| SKLearn
    Keyword -->|NLP Processing| SpaCy
    Hybrid -->|Combine All| Main
    
    Extract_Text -->|Input| Matchers
    
    Main -->|Store| Uploads
    Matchers -->|Output| Results
    Results -->|Display| Extract
    
    Env -->|Configure| Main
    Requirements -->|Dependencies| Main
    
    Extract -->|Download| Download
    Download -->|Retrieve| Results

    style Frontend fill:#e1f5ff
    style API fill:#fff3e0
    style Processing fill:#f3e5f5
    style Matchers fill:#e8f5e9
    style External fill:#fce4ec
    style Storage fill:#f1f8e9
    style Config fill:#ede7f6
    style User fill:#ffebee
```

---

## 📋 Component Description

### **Frontend Layer**
- **index.html**: Upload resumes and job descriptions
- **extract.html**: Display matching results and scores
- **download_form.html**: Download selected resumes

### **FastAPI Backend**
- **main.py**: Core application logic and request handling
- **Routes**: REST API endpoints

### **Processing Pipeline**
- **resume_parser.py**: Extract text from PDF files using PyMuPDF
- **preprocess.py**: Clean and normalize text data
- **NLP Processing**: Tokenization and text preparation

### **Matching Engines** (Choose one or hybrid)
1. **GPT Matcher**: AI-powered scoring via Groq API
2. **Cosine Matcher**: TF-IDF vectorization and similarity
3. **Keyword Matcher**: Pattern and keyword matching
4. **Hybrid Matcher**: Weighted combination of all methods

### **External Services**
- **Groq API**: Fast AI inference (llama-3.1-8b-instant)
- **spaCy**: Natural language processing
- **scikit-learn**: Machine learning and text vectorization

### **Storage**
- **uploads/**: Temporary PDF storage
- **Results Data**: Matching scores and analysis

---

## 🔄 Data Flow

```
User → Upload Resumes → Parser → Preprocess → NLP
   ↓
Select Algorithm → Matcher → External Service → Scoring
   ↓
Results → Display → Download
```

---

## ⚙️ Configuration

- `.env`: Store sensitive API keys (GROQ_API_KEY)
- `requirements.txt`: Python dependencies
- `Procfile`: Deployment configuration


