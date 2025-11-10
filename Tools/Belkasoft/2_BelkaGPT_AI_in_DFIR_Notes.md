# 🧠 BelkaGPT
*BelkaGPT: Effective Artificial Intelligence in DFIR – Part 2*

---
## How BelkaGPT Works
**BelkaGPT** is a collection of AI technologies integrated into **Belkasoft X**. It processes case artifacts and enables investigators to query data using **natural language**. Before answering questions, it builds an **AI-readable knowledge base** from analyzed case data.

### 🔹 Processing Workflow
1. **Belkasoft X Parsing**
   - Extracts forensic data: chats, calls, emails, browser history, media, geolocation, logs, etc.
2. **BelkaGPT Preprocessing**
   - Converts **audio/video → text**  
   - Performs **image analysis** (object, face, scene detection)
3. **Knowledge Base Creation**
   - All extracted artifact properties (texts, timestamps, metadata, EXIF, etc.) are transformed into structured, AI-readable format.

🧩 **Supported Artifacts:** BelkaGPT can analyze **1500 + artifact types** supported by Belkasoft X.

⚠️ **Scope Limitation:** BelkaGPT does **not** process raw or binary data.  
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
**BelkaGPT** includes built-in **speech-to-text transcription** for audio and video evidence. It can automatically convert spoken language into text for easier review, searching, and natural-language querying.

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
  - Filters ; Global filters  
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
## 💬 Working with BelkaGPT Q&A  
**BelkaGPT Q&A** helps investigators uncover **hidden patterns and relationships** in case data — such as fraud, phishing, human interactions, or suspicious events. Unlike keyword search, it identifies **concepts, meanings, and associations** between artifacts.
🔍 Example: It can infer possible fraud or collusion even if the keywords “fraud” or “money transfer” never appear explicitly.

## How You Can Use BelkaGPT
BelkaGPT can assist with:
- Detecting specific topics or incidents (e.g., *data leaks*, *forgery*)  
- Determining if two or more individuals **communicated directly**  
- Understanding **relationships between people or groups**
⚙️ **Tip:** If your question is simple (e.g., *pictures with GPS on a given date*), it’s faster to use **traditional search or filters**. Use BelkaGPT for **conceptual exploration** — start broad, identify leads, and then verify via search or filters.

## Where BelkaGPT Works Best
BelkaGPT performs best on **text-rich artifacts**, such as:
- Emails, SMS, and chats  
- Documents and notes  
- Calendar entries and logs  
- Audio/video **transcripts**  
- Picture **descriptions**  
It also interprets **metadata** (filenames, timestamps, EXIF) to connect contextual clues and system events.

## Verifying BelkaGPT Replies
- BelkaGPT’s answers are **grounded in actual case data** — not hallucinations.  
- If no relevant data is found, it clearly reports that fact.  
- Every response includes **artifact references** for verification.  
- Clicking a reference opens the related artifact or message group in **Artifacts view**.
⚠️ **Note:** A “negative” answer doesn’t mean data doesn’t exist — it may simply not be relevant to your phrasing. Always combine BelkaGPT with keyword, timeline, and file-system analysis.

## Asking BelkaGPT Questions
After preprocessing completes:
1. From **Main Menu → BelkaGPT**, open the **BelkaGPT Q&A window**.  
   - You can start using it while preprocessing runs (results will be partial).  
2. Type a question in the input field and press **Send**.  
   - To cancel a query, click **X** while waiting.  
Each answer is grounded in the **top 3 relevant artifacts** and lists them below.  

🎛️ **Controls:**
- **Navigation buttons:** open artifacts in the Artifacts window.  
- **Information icons:** show artifact properties.  
- **Show more:** display additional related artifacts.
🗨️ For chat artifacts, a reference may represent an entire conversation segment. Clicking it opens the first message of that group.

## Topics in BelkaGPT
**Topics** organize Q&A sessions like conversation threads.
- A new **topic** is created automatically when BelkaGPT Q&A opens.  
- It is renamed to match your first question.  
- Topics appear in the **left panel**.

📁 **Topic Management:**
- ➕ *New Topic* — start a new session  
- ✏️ *Edit* — rename  
- 🗑️ *Delete/Rename* — via right-click context menu  
Each topic is **searchable** for fast navigation between questions and answers.

⚠️ **Note:** BelkaGPT does **not retain conversational context** across questions. Each query is processed independently.

## Filters in BelkaGPT Q&A
Filters restrict BelkaGPT’s scope to specific artifacts or time ranges.

### 🔸 Filtering by Profile or Data Source
1. In **Artifacts → Structure tab**, check profiles to target.  
2. Right-click → **Ask BelkaGPT about checked profiles**.  
   - A topic will be created scoped to those profiles.
📝 Supported levels:
- Profile ; Profile group  
- Data source  
(Individual artifact-level filtering is **not supported**.)

### 🔸 Filtering by Timeframe
1. In **Artifacts window**, set a date range in the **global filter**.  
2. Select the desired profiles or data sources.  
3. Right-click → **Ask BelkaGPT about checked profiles**.
This creates a topic scoped to that time range and source.

## Bookmarks
You can bookmark BelkaGPT results like other analysis findings.
- Right-click an answer → **Bookmark checked items**  
- Choose an existing or new category  

Each bookmark stores:
- The **question**
- The **answer**
- The **referenced artifacts**

## Reports
You can include BelkaGPT sessions in reports.
### 🧾 To export:
- Right-click a **topic** → **Create report** → choose format  
- To export **all topics**, click **Create report** above the topic list
> Note: BelkaGPT reports contain only **questions and answers**, not the referenced artifacts themselves.

## Automating BelkaGPT via CLI
You can automate BelkaGPT workflows through the **Belkasoft X Command-Line Interface (CLI)** — useful for repetitive or standardized investigations.

### ⚙️ Using the Command Line Configurator
1. Go to the installation directory → `App` subfolder  
2. Run:  
3. In the **BelkaGPT options** section, configure:

| Option | Function |
|---------|-----------|
| **Enable BelkaGPT** | Launches data preprocessing for Q&A |
| **Questions** | Enter initial questions (one per line) |
| **Questions file path** | Load predefined questions from a text file |

After analysis, you can review:
- Answers in the CLI output  
- Full responses in the **BelkaGPT window**

### 🧩 Automating Media and Image Analysis
To automate:
1. Create an **Analysis Profile** with:
- Picture description  
- Picture classification  
- Speech recognition  
2. Select this profile under **Analysis Options** in the CLI Configurator.

📘 **More info:** [Automating DFIR Workflows with Belkasoft X](https://belkasoft.com/automating-digital-forensic-workflows-with-belkasoft-x)
⚠️ The **Automation feature** is *not included* in **Belkasoft Evidence Reader**.

## 🧩 BelkaGPT Q&A — Quiz Review

| # | Question | Correct Answer |
|---|-----------|----------------|
| 1 | Which of the following types of data does BelkaGPT use in its answers? | ✅ Email text and properties<br>✅ Recognized audio texts<br>✅ Calendar events |
| 2 | What does BelkaGPT provide references to when answering queries? | ✅ The most relevant artifacts in the case data |
| 3 | What type of content does BelkaGPT primarily focus on when looking for relevant artifacts? | ✅ Text |
| 4 | How many relevant artifacts does BelkaGPT show by default? | ✅ 3 artifacts |
| 5 | Which of the following tasks can BelkaGPT help with? | ✅ Looking for evidence in the case data |
| 6 | What is a recommended practice when using BelkaGPT? | ✅ Use BelkaGPT to find a clue, then check the findings, and use other methods to ensure that nothing is missing |
| 7 | What options do you have to export BelkaGPT questions and answers into PDF format? | ✅ Create a report for a selected topic<br>✅ Create a report for all BelkaGPT topics at once |

---
