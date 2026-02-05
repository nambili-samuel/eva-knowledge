# RAG SYSTEM - Document Knowledge Base
# ========================================

## NEW FEATURE: RAG (Retrieval-Augmented Generation)

Your bot can now read and search through **PDF, Word, and text documents**!

---

## WHAT IS RAG?

**RAG = Retrieval-Augmented Generation**

It's an AI system that:
1. Reads documents (PDF, DOCX, TXT, MD)
2. Chunks them into searchable pieces
3. Searches when users ask questions
4. Provides answers from documents

**Think of it as:** A smart library assistant that instantly finds relevant information from all your documents!

---

## HOW IT WORKS

### **1. You Upload Documents**
Upload files to GitHub repository:
- PDF files (research papers, guides, reports)
- Word documents (policies, procedures, manuals)
- Text files (notes, articles, data)
- Markdown files (documentation)

### **2. Bot Downloads & Processes**
- Extracts all text
- Splits into searchable chunks (500 words each)
- Creates keyword index
- Stores in memory

### **3. User Asks Question**
User: "What does the tourism guide say about Etosha?"

### **4. Bot Searches Documents**
- Searches ALL documents
- Finds relevant chunks
- Ranks by relevance
- Returns best matches

### **5. Smart Response**
Bot: "📄 From: namibia-tourism-guide.pdf

Etosha National Park is one of Africa's premier game reserves..."

---

## GITHUB REPOSITORY SETUP

### **Step 1: Create Repository**

1. Go to GitHub
2. Create new repository:
   - Name: `eva-knowledge`
   - Public or Private (both work)
   - Initialize with README

### **Step 2: Create Documents Folder**

```
eva-knowledge/
├── documents/           ← Create this folder
│   ├── namibia-tourism-guide.pdf
│   ├── etosha-wildlife-info.docx
│   ├── property-listings.txt
│   ├── himba-culture.md
│   └── ... (more documents)
├── README.md
└── .gitignore
```

### **Step 3: Upload Documents**

In the `documents/` folder, upload:
- ✅ PDF files
- ✅ Word documents (.docx, .doc)
- ✅ Text files (.txt)
- ✅ Markdown files (.md)

**Size limits:**
- Individual file: Up to 25MB
- Total: Unlimited

### **Step 4: Get Repository URL**

Your GitHub API URL will be:
```
https://api.github.com/repos/YOUR-USERNAME/eva-knowledge/contents/documents
```

Example:
```
https://api.github.com/repos/nambili-samuel/eva-knowledge/contents/documents
```

---

## ⚙️ CONFIGURATION

### **Environment Variable**

Set in Render Dashboard:
```
RAG_DOCUMENTS_URL=https://api.github.com/repos/YOUR-USERNAME/eva-knowledge/contents/documents
```

**If not set:** Uses default (nambili-samuel/eva-knowledge)

---

## DEPLOYMENT

### **Files to Upload:**

1. ✅ **document_rag.py** (NEW!)
2. ✅ **main.py** (UPDATED - includes RAG)
3. ✅ **requirements.txt** (UPDATED - adds PyPDF2, python-docx)
4. ✅ All other existing files

### **Requirements.txt (Updated):**

```
python-telegram-bot[job-queue,webhooks]==20.7
python-dotenv==1.0.0
requests==2.31.0
pandas==3.0.0
aiohttp==3.13.3

# RAG System Dependencies
PyPDF2==3.0.1
python-docx==1.1.0
```

### **Deploy Steps:**

1. Upload `document_rag.py` to Render
2. Upload updated `main.py`
3. Upload updated `requirements.txt`
4. Set `RAG_DOCUMENTS_URL` (optional)
5. Deploy!

---

## USER COMMANDS

### **For Everyone:**

```
/documents
/docs          (alias)
```
Shows list of available documents in library.

**Example:**
```
User: /documents
Bot: 📚 Document Library (5 documents)

1. 📄 namibia tourism guide
   _1,234 words_

2. 📄 etosha wildlife info
   _856 words_

... etc
```

### **For Admins:**

```
/sync_docs     - Sync documents from GitHub now
/rag_stats     - Show RAG system statistics
```

---

## 💬 HOW USERS INTERACT

### **Automatic Search:**

Users don't need special commands - just ask naturally!

**Example 1:**
```
User: "What does the guide say about lions?"
Bot: 📄 From: etosha-wildlife-info.pdf

Lions in Etosha National Park are among the most studied 
populations in Africa. The park hosts approximately 200-300 
lions across multiple prides...

_Source: Document Library_

More in documents: namibia-tourism-guide.pdf

Use /documents to see all available docs! 
```

**Example 2:**
```
User: "Property prices in Windhoek?"
Bot: 📄 From: property-listings.txt

Windhoek West Properties:
- 3 bedroom: N$1.2M - N$1.5M
- 4 bedroom: N$1.8M - N$2.5M
...

_Source: Document Library_
```

---

## SEARCH PRIORITY

Bot searches in this order:

1. **RAG Documents** (Highest priority)
   - Uploaded PDFs, DOCX, TXT
   - Most detailed information
   
2. **Knowledge Base**
   - CSV data from Gist
   - Quick facts

3. **No Results**
   - Helpful fallback message

---

## FEATURES

### **Intelligent Chunking:**
- Splits documents into 500-word chunks
- Maintains context
- Searchable keywords

### **Multi-Format Support:**
- ✅ PDF (via PyPDF2)
- ✅ Word (via python-docx)
- ✅ Text (native)
- ✅ Markdown (native)

### **Smart Search:**
- Exact phrase matching
- Word matching
- Keyword matching
- Proximity scoring
- Relevance ranking

### **Auto-Sync:**
- Checks for updates every hour
- Downloads new documents
- Updates changed documents
- Removes deleted documents

---

## TESTING

### **Test 1: Upload Document**

1. Create file: `test-document.txt`
   ```
   Namibia has unique wildlife including desert elephants.
   These elephants have adapted to survive in harsh conditions.
   ```

2. Upload to GitHub: `documents/test-document.txt`

3. In Telegram, send: `/sync_docs`

4. Ask: "Tell me about desert elephants"

5. Should get: Response from `test-document.txt` ✅

### **Test 2: Multiple Documents**

1. Upload 3 different documents about tourism
2. Sync: `/sync_docs`
3. Ask: "Best places to visit in Namibia?"
4. Should search ALL documents ✅
5. Returns most relevant chunk ✅

### **Test 3: List Documents**

```
You: /documents
Bot: Shows list of all documents ✅
```

---

## EXAMPLE DOCUMENTS TO UPLOAD

### **Tourism:**
- namibia-tourism-guide.pdf
- etosha-visitor-info.docx
- sossusvlei-guide.txt
- swakopmund-activities.md

### **Wildlife:**
- namibia-wildlife-guide.pdf
- desert-elephants-research.docx
- cheetah-conservation.txt

### **Culture:**
- himba-people-culture.pdf
- namibian-traditions.docx
- cultural-etiquette.txt

### **Real Estate:**
- property-market-report.pdf
- windhoek-listings.docx
- investment-opportunities.txt

### **Practical:**
- visa-requirements.pdf
- travel-safety-tips.docx
- getting-around-namibia.txt

---

## 🔧 ADMIN OPERATIONS

### **Sync Documents:**

```
You: /sync_docs
Bot: 📥 Syncing documents from GitHub...

✅ Documents Synced!

📚 Total documents: 8
🔍 Searchable chunks: 145
⏰ Last sync: 2026-02-05 14:30:00

Documents are now searchable!
```

### **Check Statistics:**

```
You: /rag_stats
Bot: RAG System Statistics

📚 Documents: 8
🔍 Chunks: 145
⏰ Last sync: 2026-02-05 14:30:00
📁 Source: GitHub

💡 Use /documents to see available files!
```

---

## 💡 USE CASES

### **1. Tourism Agency:**
Upload comprehensive guides:
- Destination guides
- Activity catalogs
- Pricing sheets
- Travel itineraries

Users get instant answers from official documents!

### **2. Real Estate:**
Upload property information:
- Listings
- Market reports
- Investment guides
- Legal documents

Buyers get accurate, detailed information!

### **3. Cultural Center:**
Upload educational content:
- History documents
- Cultural guides
- Traditional knowledge
- Language resources

Visitors learn authentic information!

### **4. Conservation:**
Upload research:
- Wildlife studies
- Conservation reports
- Environmental data
- Species information

Researchers and tourists access real data!

---

## ADVANTAGES

### **vs Manual Q&A:**
- ❌ Manual: Update bot code for each new fact
- ✅ RAG: Just upload document, instant knowledge

### **vs Knowledge Base CSV:**
- ❌ CSV: Limited format, no long-form content
- ✅ RAG: Full documents with context

### **vs External Links:**
- ❌ Links: Users must leave Telegram
- ✅ RAG: Answers directly in chat

---

## 📋 CHECKLIST

### **Setup:**
- [ ] Create GitHub repository
- [ ] Create `documents/` folder
- [ ] Upload first document
- [ ] Set `RAG_DOCUMENTS_URL` env variable (optional)
- [ ] Deploy updated bot
- [ ] Run `/sync_docs` in Telegram
- [ ] Test with question

### **Ongoing:**
- [ ] Add new documents to GitHub
- [ ] Run `/sync_docs` manually or wait for auto-sync
- [ ] Monitor `/rag_stats` for statistics
- [ ] Update documents as needed

---

## 🚨 TROUBLESHOOTING

### **Issue: No documents synced**

Check:
1. Is `RAG_DOCUMENTS_URL` correct?
2. Is GitHub repo public? (or token configured)
3. Check Render logs for errors
4. Try `/sync_docs` manually

### **Issue: Can't read PDF**

Make sure:
1. PDF is text-based (not scanned image)
2. File size < 25MB
3. PyPDF2 is in requirements.txt

### **Issue: Searches not finding documents**

Check:
1. Are documents synced? (`/rag_stats`)
2. Is query too specific?
3. Try broader search terms

---

## 📊 LOGS TO EXPECT

On startup:
```
📚 Syncing RAG documents...
📥 Syncing documents from GitHub...
✅ Processed namibia-tourism-guide.pdf: 25 chunks, 1234 words
✅ Processed etosha-wildlife.docx: 18 chunks, 856 words
✅ Document sync complete: 2 new, 0 updated
📚 Total documents: 2
🔍 Total searchable chunks: 43
✅ RAG ready: 2 docs, 43 chunks
```

---

## 🎉 RESULT

Your bot now has:

✅ **Static Knowledge** (CSV from Gist)
✅ **Dynamic Documents** (GitHub repository)
✅ **Conversational Intelligence** (smart responses)
✅ **Automated Engagement** (polls, stories, weather)
✅ **Never Sleeps** (self-ping system)

= **The Most Powerful Namibia Bot Ever!** 🇳🇦🤖📚

---

## 🔄 WORKFLOW

```
1. You create/update document
   ↓
2. Upload to GitHub
   ↓
3. Bot auto-syncs (hourly)
   or manual /sync_docs
   ↓
4. Document processed into chunks
   ↓
5. User asks question
   ↓
6. Bot searches documents
   ↓
7. Returns relevant answer
   ↓
8. User satisfied! ✅
```

---

## GET STARTED

**Right Now:**

1. Create GitHub repo: `eva-knowledge`
2. Add folder: `documents/`
3. Upload one document (any topic)
4. Deploy updated bot
5. Run `/sync_docs`
6. Ask question about the document
7. Get instant answer! 🎉

Your bot is now a **document-powered knowledge engine**! 
