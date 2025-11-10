# 🧠 BelkaGPT
*BelkaGPT: Effective Artificial Intelligence in DFIR – Part 2*

---
## How BelkaGPT Works
**BelkaGPT** is a collection of AI technologies integrated into **Belkasoft X**.  
It processes case artifacts and enables investigators to query data using **natural language**.  
Before answering questions, it builds an **AI-readable knowledge base** from analyzed case data.

### 🔹 Processing Workflow
1. **Belkasoft X Parsing**
   - Extracts forensic data: chats, calls, emails, browser history, media, geolocation, logs, etc.
2. **BelkaGPT Preprocessing**
   - Converts **audio/video → text**  
   - Performs **image analysis** (object, face, scene detection)
3. **Knowledge Base Creation**
   - All extracted artifact properties (texts, timestamps, metadata, EXIF, etc.) are transformed into structured, AI-readable format.

🧩 **Supported Artifacts:** BelkaGPT can analyze **1500 + artifact types** supported by Belkasoft X.

⚠️ **Scope Limitation:**  
BelkaGPT does **not** process raw or binary data.  
It works **only with parsed artifacts**, e.g.:
- ✅ WhatsApp chat data extracted from SQLite tables  
- ❌ The raw SQLite database file itself  


### BelkaGPT Q&A Process
When you ask a question:
1. BelkaGPT **interprets the query**.  
2. It retrieves **semantically relevant artifacts** from the knowledge base.  
3. Applies **relevance scoring** to rank matches.  
4. Generates a **human-readable answer** grounded in:
   - The top 3 relevant artifacts  
   - Your question  
   - Internal system instructions (prompt)
📎 Each BelkaGPT response remains **traceable to its original artifacts**, ensuring forensic defensibility.

### Core Principles and Capabilities

| Capability | Description |
|-------------|-------------|
| **Offline Operation** | Runs entirely without internet access. |
| **Flexible Processing** | Allows partial or deferred preprocessing to save resources. |
| **Multimodal Input** | Handles text, pictures, audio, and video. |
| **Domain-Specific Behavior** | Can respond “no data found” instead of hallucinating. |
| **Traceable Output** | Every answer can be linked back to original evidence. |
| **Report Integration** | Results can be bookmarked and included in reports. |

---

## BelkaGPT Analysis Options
BelkaGPT supports two analysis modes:

### 🔸 During Initial Analysis
- When defining **data-source analysis options**, enable **BelkaGPT operations**.  
- Preprocessing runs automatically across selected artifact types during data import.

### 🔸 On-Demand from Artifacts Window
- After artifact extraction, open the **Artifacts window**.  
- Run **BelkaGPT operations** manually on specific profiles (e.g., Chats, Pictures, Documents).  
- Useful when focusing AI resources on artifact types most relevant to the case.

### ⚠️ System Requirement Notice
If BelkaGPT resources are **not installed**, Belkasoft X displays a configuration warning in analysis settings.
> **Important:** BelkaGPT requires a **PostgreSQL case database**.  
> It **does not** work with **SQLite-based cases**.

---

## 🎙️ Speech Recognition in Audio and Video
---

### 🔹 Overview
**BelkaGPT** includes built-in **speech-to-text transcription** for audio and video evidence.  
It can automatically convert spoken language into text for easier review, searching, and natural-language querying.

**Key Specs**
- Supports **audio/video files up to 30 minutes long**
- Works with **European, Asian, and Semitic languages**  
  *(see full list on the BelkaGPT page)*
- Other languages may transcribe, but with reduced accuracy

### ⚙️ Enabling Speech-to-Text During Data Source Analysis
When adding a new data source:
1. Open **Add a data source**  
2. Go to the **Media** tab  
3. Enable one or both options:
   - ✅ *Convert audio to text*  
   - ✅ *Convert audio from video to text*
This automatically performs transcription during the initial artifact extraction.

### 🧩 On-Demand Speech Recognition
You can also run transcription manually, after analysis:
1. Open the **Artifacts** window  
2. Right-click the **Audio** or **Video** profile  
   - Select **Convert audio to text**, or  
   - Select multiple items → right-click → **Convert checked audios to text**
3. Progress appears under the **Tasks** tab

Once complete:
- Transcribed text appears in **Tools pane → Item text**
- Also visible in the artifact’s **Text field** under **Properties**

### 🔍 Integration with Search and Filters
- The **Text field** is **indexed**  
- Transcriptions become searchable via:
  - Keyword search  
  - Filters  
  - Global filters  
  - Natural-language queries (if preprocessed for BelkaGPT)

### ⚠️ Important Notes

| Mode | Preprocessing for BelkaGPT Q&A | Notes |
|------|--------------------------------|-------|
| **Initial analysis** | ❌ Disabled by default | Must be manually enabled on the **BelkaGPT tab** |
| **On-demand (Artifacts window)** | ✅ Enabled automatically | Transcriptions become searchable immediately |

## 🧩 BelkaGPT Media & Speech Recognition — Quiz Review

| # | Question | Correct Answer |
|---|-----------|----------------|
| 1 | What does one need to do to make BelkaGPT work on case data? | ✅ Download and install **BelkaGPT resources**<br>✅ Enable **BelkaGPT** when adding a data source |
| 2 | Which media analysis operation does BelkaGPT **NOT** perform? | ❌ **Deepfake detection** |
| 3 | To perform audio transcription using BelkaGPT, which option must be selected? | ✅ **Convert audio to text** |
| 4 | What must be done to recognize speech in video files and query it with BelkaGPT? | ✅ Check **Convert audio from video to text** in Media options<br>✅ Check **Enable BelkaGPT** in BelkaGPT options |
| 5 | What describes the languages supported for audio recognition by BelkaGPT? | 🌐 **A wide range of global languages**, including European, Asian, and Semitic families |
| 6 | For which kind of artifacts can you create custom classification categories in BelkaGPT? | 🖼️ **Pictures** |

---

