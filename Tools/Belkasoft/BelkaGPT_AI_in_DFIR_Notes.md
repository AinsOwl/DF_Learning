# BelkaGPT: Effective Artificial Intelligence in DFIR  
## 1️⃣ Introduction: AI Technologies and LLM

---

### 🔹 What is Artificial Intelligence (AI)?
AI refers to computer systems capable of performing tasks that usually require **human intelligence**, such as:
- Recognizing objects, sounds, and text  
- Reading and writing  
- Making assumptions, predictions, and decisions  

Some tasks easy for humans (e.g., telling a cat from a dog) were hard for early computers, which relied on explicit programming.  
Machine Learning (ML) changed that by enabling computers to **find patterns in data automatically**.


### 🔹 Machine Learning and Neural Networks
- **Machine Learning (ML):** Algorithms that allow computers to learn from data instead of following fixed rules.  
- **Neural Network:** A mathematical model inspired by the human brain that processes data through **neurons** organized in **layers**.  

Neural networks learn features and patterns in data to make predictions. When they contain many layers → **Deep Learning**.

Deep learning requires high computing power, made possible through advances in GPUs and processors. It enabled analysis of **unstructured data** (images, sound, text).

Example in DFIR: Belkasoft X uses neural networks to automatically detect and categorize images containing:
- Faces ; Weapons ; Pornographic material  ; Other objects of forensic interest  

---

### 🧩 Large Language Models (LLMs)

#### 🔹 What is an LLM?
An **LLM (Large Language Model)** is a deep learning system trained on massive text datasets to **understand and generate human language**.
It learns **statistical patterns** and **contextual relationships** among words (tokens) to predict text.


#### ⚙️ How LLMs Work

**1. Training Phase**
- Text is broken into **tokens** (words, subwords, or phrases).  
- The model learns relationships among tokens using **self-attention** mechanisms.  
- Each token gets a **numerical vector (embedding)** representing meaning and context.  
- Through repeated updates, embeddings and parameters evolve to reflect language structure and knowledge.  

🧩 **Embedding:** A numerical representation of a text unit capturing its **semantic meaning** and relationships.

**2. Inference Phase**
- Model receives user input (called a **prompt**).  
- It converts input into tokens and looks up embeddings.  
- Predicts the **next most probable token** repeatedly until completion.  

🗝️ **Prompt:** Text or instruction provided to the LLM that sets the context and defines the task.  


#### 🎲 Decoding and Randomness
LLMs don’t always pick the most probable token — they use **controlled randomness** to make outputs more natural.  
- **Temperature parameter** controls this:
  - Low temperature → Consistent, predictable output  
  - High temperature → Creative, varied output
    

#### 💡 LLM Capabilities
LLMs excel at:
- Generating human-like text  
- Answering questions  
- Summarizing large texts  
- Sentiment analysis  
- Reasoning over language-based tasks  

They serve as a **bridge between humans and other AI systems** (e.g., speech, vision).  
The LLM interprets data and presents it in a human-understandable form — making it the **core interface in AI ecosystems**.

---

### 🗣️ Automatic Speech Recognition (ASR)

#### 🔹 What is ASR?
ASR (Automatic Speech Recognition) converts **spoken audio → written text**.

It’s used in:
- Live captions  
- Voice typing  
- Transcription of meetings or recordings  


#### ⚙️ How ASR Works

**Training Phase:**
- Uses large datasets of audio and corresponding transcripts.  
- Learns how audio patterns (time-frequency features) map to letters or words.  
- Improves understanding of grammar, punctuation, and accents.

**Inference Phase:**
1. Detects speech segments in an audio recording.  
2. Converts them into time-based features.  
3. Predicts possible text units and refines them based on sentence context.  
4. Outputs formatted text (with punctuation, capitalization, etc.).  

---

### 🧠 Multimodal AI Systems

#### 🔹 From Single-Modality to Multimodality
Traditional AI models focused on one data type:
- LLM → text  
- ASR → audio  

Modern systems are **multimodal**, handling:
- Text ; Images  
- Audio ; Video  
- Sensor data  

This is crucial for complex tasks such as:
- Describing images  
- Answering questions about charts  
- Translating speech in videos  
- Summarizing meetings with slides  


#### ⚙️ How Multimodal AI Works

1. **Encoding Inputs** into embeddings:  
   - Image → Patch embeddings (visual tokens)  
   - Audio → Acoustic embeddings  
   - Text → Token embeddings  

2. **Alignment:**  
   - Aligns embeddings from different modalities into a shared space.  
   - Uses **projection layers** or **cross-attention** to link them.  
   - Trained with paired data (e.g., image–text pairs).  

3. **Generation/Decision:**  
   - Decoder (often an LLM) processes aligned embeddings + user prompt.  
   - Generates text output or makes classification decisions.  


#### 🖼️ Example: Image Captioning
**Training:**
- Vision encoder breaks an image into visual tokens.
- These embeddings are mapped into the LLM’s token space.
- Fine-tuned on image–text tasks (captions, Q&A).

**Inference:**
- Encode the image → Visual embeddings  
- Pass to LLM → Combined with text prompt  
- LLM attends to visual tokens → Generates caption step-by-step  

---

## 📝 Quiz Review

| Question | Answer |
|-----------|--------|
| 1. What does LLM stand for? | Large Language Model |
| 2. Main purpose of LLMs | To process natural language and generate human-like text |
| 3. What is an embedding? | A numerical vector capturing the semantic meaning of text units |
| 4. What is a prompt? | A piece of text or instruction given to an LLM to define its task |
| 5. Purpose of Deep Learning | Finding patterns in unstructured data (images, text) |
| 6. Not an LLM strength | Predicting stock prices with accuracy |

---

### ⚖️ AI’s Advantages and Downsides


#### 🔹 How AI Systems Learn
AI systems are trained on large datasets — including **text, images, audio, video, logs, and sensor data**.  
During training, these raw signals are converted into **numerical representations (embeddings)** that are optimized to predict or describe targets such as:
- Classifying or describing an image  
- Transcribing speech  
- Forecasting demand  
- Planning an action  
- Generating text  

This process enables AI to generalize patterns and perform complex human-like tasks — but it also introduces limitations.


#### ⚠️ Common Limitations and Risks of AI

**1. Sounds confident but can be wrong**  
- Generative models may “hallucinate” or fabricate information.  
- Image captioning models might confuse visually similar objects.

**2. Becomes outdated**  
- Models are trained on past data.  
- As real-world contexts change (new slang, fraud techniques, or laws), their accuracy declines.

**3. Sensitive to small changes**  
- Minor prompt edits or parameter tweaks can yield drastically different results.  
- Outputs may not be repeatable.

**4. Weak at strict logic**  
- Lacks tools for multi-step reasoning, math precision, or causal understanding without external support.

**5. Cannot cite sources natively**  
- Without document linking or retrieval systems, it cannot reliably trace where facts come from.

**6. Reflects data bias**  
- Training data imbalance can cause performance variation across accents, demographics, or niche fields.

**7. Privacy and security risks**  
- User inputs may be stored or shared depending on the AI provider.  
- Vulnerable to *prompt injection attacks* or data leaks.

**8. Resource-intensive**  
- Large models consume substantial computing power, cost, and energy — especially for audio/video processing.


#### 🧭 Best Practices in Using AI

**Keep a human in the loop**  
- Always review AI outputs in high-stakes or sensitive contexts.  
- Define what “good enough” accuracy means before deployment.

**Tie answers to trusted sources**  
- Connect AI models to internal documents or databases to improve factual reliability.

**Test and monitor continuously**  
- Check model accuracy regularly.  
- Track quality drift, audit confidence scores, and maintain logs.

**Deploy smartly**  
- Choose whether AI runs **locally** (better control, privacy) or **in the cloud** (scalability, convenience).

---

## 📝 Quiz Review

| Question | Answer |
|-----------|--------|
| 1. Which example is explicitly listed as a real-time ASR use? | Live captions |
| 2. How can an ASR system handle different accents? | Through multiple iterations of training on labeled speech from many accents |
| 3. What makes an AI system multimodal? | It can process or generate multiple data types |

---

## 2️⃣ Usage of AI in DFIR

### 🔹 How AI Can Help in DFIR
Traditional digital forensics tools automate **data acquisition, decryption, and extraction**, but the real challenge starts **after** extraction — when thousands of artifacts must be manually examined. AI adds immense value in analyzing **media files and textual content**, tasks that traditionally take hours of manual review.

### ⚙️ AI in Different DFIR Workflows

**1. Large Language Models (LLMs)**  
Devices under investigation often store years of messages, emails, notes, and logs.  
LLMs can:
- Analyze massive text datasets for topics or keywords  
- Detect emotional tone (sentiment analysis)  
- Summarize or cluster communication patterns  

This saves time and helps investigators spot relevant context quickly.

**2. Image Captioning**  
Traditional classification narrows focus (e.g., detecting faces, guns), but remains limited in scope.  
AI-powered image captioning can describe entire scenes, turning visual evidence into **searchable text**.

Examples:
- Recognize contextual clues (clocks, signs, reflections)  
- Search for precise scenarios:  
  *“a boy near a gas station”*  
  *“a man wearing a blue shirt with a logo”*  

This transforms images into searchable intelligence, improving triage efficiency.

**3. Automatic Speech Recognition (ASR)**  
Voice messages and calls are common evidence sources.  
AI converts speech to text for quick scanning and keyword searches.  
Combined with LLMs, investigators can:
- Run **natural-language queries** over transcripts  
- Perform **sentiment analysis**  
- Identify relevant speech fragments without replaying hours of audio  

### 🧠 AI as a Forensic Assistant, Not a Replacement
AI **augments** forensic workflows rather than replacing core tools.  
By transforming **images, audio, and text** into **searchable digital signals**, it:
- Reduces manual workload and fatigue  
- Shortens review cycles  
- Allows experts to focus on **interpreting** and **defending** conclusions  

---

## 3️⃣ Implementation Challenges in DFIR

### 🔸 Reliability
AI operates only within the limits of its **training data**.  
LLMs can misinterpret rare or domain-specific information and often **cannot admit uncertainty** — they generate a response regardless of factual accuracy.

### 🔸 Validation and Reproducibility
Digital forensics demands **repeatable and verifiable** results.  
AI outputs, however, may vary due to:
- Randomness in generation  
- Prompt sensitivity  
- Parameter changes  

This poses a challenge for evidentiary standards and reproducibility.

### 🔸 Transparency and Explainability
Deep neural networks function as **black boxes** — they provide answers without showing how those answers were derived.  
In court, if an investigator cannot explain the reasoning behind a model’s output, that evidence may be questioned or rejected.

### 🔸 Deployment Concerns
AI models often require **high computing power** and are frequently hosted in the **cloud**.  
For DFIR labs, cloud usage is typically **prohibited** due to confidentiality and data-protection laws.

Running AI **locally** preserves data integrity but demands:
- Sufficient GPU or CPU resources  
- Compatible hardware  
- Technical expertise for maintenance  

This makes adoption challenging for smaller or resource-limited labs.

---

## 4️⃣ Making AI Work for Digital Forensics

To safely and effectively use AI in DFIR:

1. **Clearly mark AI-generated outputs**  
   - Ensure investigators know which conclusions were AI-assisted.

2. **Ensure verifiability**  
   - Trace every AI response back to the original artifact.  
   - Transparency is critical for admissibility in court.

3. **Respect real-world lab constraints**  
   - Design AI tools to function on modest setups (CPU-only if needed).  

4. **Enable scalability**  
   - Distributed systems can share workloads across machines, improving performance in large or urgent cases.

### 🤖 What is BelkaGPT?

**BelkaGPT** is a generative-AI assistant built into **Belkasoft X**, designed specifically for **digital forensic investigations**. It processes case data extracted from Belkasoft X and answers investigator queries in **natural language**.

### Key Advantages:
- **Offline operation** → no sensitive data leaves the forensic environment.  
- **Local processing** → aligns with DFIR lab security requirements.  
- **Optimized performance** → runs on typical forensic workstations; faster with GPUs but functional on CPU-only systems.  

Unlike generic AI tools like ChatGPT, **BelkaGPT knows your case data** and **never relies on cloud servers**, ensuring forensic confidentiality and control.

---

## 📝 Quiz Review

| Question | Answer |
|-----------|--------|
| 1. What statement about ChatGPT and BelkaGPT is correct? | They are both LLMs and AI |
| 2. What is true about an average LLM? | It can determine the sentiment or emotional tone of text; it can provide answers to questions in natural language |
| 3. What are the main benefits of using BelkaGPT in DFIR compared to ChatGPT? | BelkaGPT works offline (no sensitive data leaves the lab); BelkaGPT understands the case data |

---

## 5️⃣ Getting Started with BelkaGPT and BelkaGPT Hub

---

### 🔹 BelkaGPT System Requirements
BelkaGPT is optimized to run efficiently even on **mid-range forensic workstations**. Most DFIR labs already have suitable hardware due to password cracking or imaging workloads.

#### 🖥️ Recommended Configuration:
- **RAM:** ≥ 32 GB  
- **GPU:** Discrete **NVIDIA GPU** with **12+ GB VRAM** and **CUDA 12.x support**  
  - GPU acceleration improves GPT processing **4–60× faster**  
- **CPU:** If no GPU is available, BelkaGPT can run on a **high-end CPU (10K+ benchmark score)**  
  - Performance will be slower compared to GPU-based setups  

🧩 **Check your system:**
- **CPU benchmark:** [https://www.cpubenchmark.net](https://www.cpubenchmark.net)  
- **CUDA-enabled GPUs:** [NVIDIA CUDA GPU List](https://developer.nvidia.com/cuda-gpus)

### ⚙️ GPU Environment Setup
If your workstation includes a supported GPU, configure CUDA and cuDNN for acceleration.

#### 1. Install CUDA 12.x or Later  
- **Download:** [CUDA 12.9.0 Download Archive](https://developer.nvidia.com/cuda-12-9-0-download-archive)  
- **Setup Guide:** [CUDA Installation Guide (Windows)](https://docs.nvidia.com/cuda/archive/12.9.0/cuda-installation-guide-microsoft-windows/index.html)

#### 2. Install cuDNN 9.x for CUDA 12.x  
- **Download:** [cuDNN Downloads](https://developer.nvidia.com/cudnn-downloads)  
- **Setup Guide:** [cuDNN Installation Guide](https://docs.nvidia.com/deeplearning/cudnn/installation/latest/index.html)

### 🔧 Configuring Environment Variables
After installation, configure CUDA and cuDNN paths.
1. Open Windows search → type **“Edit the system environment variables”** → open the result.  
2. Go to **Advanced → Environment Variables**.  
3. Add new variables:
   - `CUDA_PATH`  
   - `CUDA_PATH_V12_8`  
4. Edit the **Path** system variable → add these lines:
   - 'C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.8\bin'
   - 'C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.8\lib'
   - 'C:\Program Files\NVIDIA\CUDNN\v9.13\bin\12.9'
6. Restart the PC.  
7. Verify installation by opening Command Prompt (Admin) and typing: nvcc --version

#### For Trial Version of Belkasoft X:
- On first launch, you’ll be prompted to **download BelkaGPT resources**.  
- If you skipped this earlier, close and reopen Belkasoft X to get the prompt again.

#### For Licensed Version:
1. Check that your **license includes BelkaGPT**  
- Path: `Home → License Information`  
2. If missing, contact **sales@belkasoft.com**  
- Include your **license/dongle ID**  
- You’ll receive an updated license file (free update)  
- Replace the old license file in your installation directory  
3. Log in to the **Customer Portal** → go to **Downloads** → download **BelkaGPT resources**.  
4. Extract `belkasoft-resources.zip` to a convenient folder.

### 🧩 Installing BelkaGPT Resources
1. Run `BelkaGptResources.msi`.  
2. Follow the installation wizard.  
3. Choose an appropriate installation path (any convenient directory).  
4. After installation, verify that the **folder hierarchy** matches the provided structure.

---
## 🧠 BelkaGPT Hub — Distributed AI Processing in DFIR
---

### 🔹 What is BelkaGPT Hub?

**BelkaGPT Hub** is an **offline, distributed AI processing system** that enables scalable use of BelkaGPT features within **Belkasoft X**. It allows data preprocessing tasks to be offloaded from local machines to more powerful **processing nodes** on the same local network.
Performance scales **linearly** with the number of connected nodes — meaning more nodes = faster data preparation.

🧩 **Key Purpose:**  
To accelerate preprocessing for BelkaGPT analysis — especially useful when:
- Workstations have only CPUs or entry-level GPUs  
- Large datasets require heavy processing  

> ⚠️ *BelkaGPT Hub is a separate licensed module and is not included in the Belkasoft X trial version.*

### ⚙️ How BelkaGPT Hub Works

BelkaGPT Hub manages distributed AI processing through the following workflow:

1. **Belkasoft X** analyzes a data source and sends AI-related tasks to the **BelkaGPT Hub**.  
2. **The Hub** queues and routes these tasks to available **BelkaGPT workers** (processing nodes).  
   - The Hub and worker can be on the same machine in small setups.  
3. **Workers** perform the AI processing — preferably on GPUs (CPU fallback is possible).  
4. **Results** are sent back through the Hub to the original **Belkasoft X client**.

### 🔧 Connecting Belkasoft X to BelkaGPT Hub
To enable distributed AI processing via the Hub:

1. **Install and configure** the required Hub components.  
   - Contact support for setup assistance: **support@belkasoft.com**  
2. In **Belkasoft X**, go to:  
   `Home → Settings → BelkaGPT`  
3. Under **Select where to perform BelkaGPT processing**, choose:  
   **On a BelkaGPT Hub**  
4. In the **Hub location** field, enter the machine’s name or IP address.  
5. In the **Port** field, enter `5672` (default Hub port).  
6. Click **Apply**.  
   - If successful, the **status indicator** turns **green**.

> 📝 Note: Using BelkaGPT Hub requires an additional **license module**.

### 🖥️ Minimum Hardware Requirements (for BelkaGPT Workers)

| Component | Requirement |
|------------|--------------|
| **GPU** | CUDA-compatible, ≥ 12 GB VRAM |
| **RAM** | 32 GB or more |
| **CPU** | Any modern processor |
| **Network** | 100+ Mbps local connection |

💡 *Workers can be dedicated servers or even teammates’ GPU-enabled workstations.*

### 🧩 Scalability and Performance

| Question | Answer |
|-----------|--------|
| **Can I use multiple GPUs on one node?** | Yes — up to **8 GPUs per node** (as of Belkasoft X v2.9). |
| **Is distributed processing faster than one strong server?** | It depends on **total GPU tensor cores** (roughly tied to VRAM). If multiple nodes have more combined cores, they’ll outperform a single server. |
| **How does performance scale with additional nodes?** | **Linearly** — doubling nodes halves processing time. Example: 5 hours with 2 nodes → ~2.5 hours with 4 nodes. |
| **How many processing nodes can I add?** | There is **no upper limit**. |
| **How does the Hub manage multiple tasks?** | Tasks are queued **FIFO** (first-in, first-out). The Hub can distribute jobs across workers for concurrent task handling. |

**Notes**
- No limit on processing nodes.  
- Up to 8 GPUs per node (Belkasoft X v2.9+).  
- FIFO task queuing for concurrent jobs.  
- Data processing only (inference offloading planned).

### ⚡ Current Capabilities and Limitations

| Feature | Status |
|----------|--------|
| **Accelerates data preprocessing** | ✅ Supported |
| **Accelerates inference (answer generation)** | 🚧 Not yet — planned for future release |
| **Supports larger AI models on bigger GPU clusters** | ❌ Not currently; BelkaGPT uses the same model across configurations |
| **Supports offline operation** | ✅ Fully offline |
| **Supports local network deployment** | ✅ Yes, for secure on-premise setups |

---
## 6️⃣ Reviewing Artifacts in Belkasoft X

### 🔹 Artifacts Window Overview
Artifacts = extracted forensic data (chats, images, documents, etc.).

**Layout**
- **Left:** Structure & Overview tabs  
- **Middle:** Artifact list  
- **Right:** Properties pane  
- **Bottom:** Tools pane  
- **Top:** Report, mini-timeline, global filter

### 🧭 Structure vs Overview
- **Structure Tab:** Shows data sources and artifact origins.  
- **Overview Tab:** Groups all artifacts of one type together for easy review.

### 💬 Artifact List Views
- **Bubble View:** Chat-style, user-friendly.  
- **Table View:** Sortable, filterable columns for technical analysis.  
- Right-click → *Show contacts* for per-user chat breakdown.

**Tools Pane:** Displays viewers like Hex, SQLite, Registry, or Plist depending on artifact type.

**Properties Pane:** Shows metadata for selected items.

### 🕒 Top Controls
- **Report:** Export checked items.  
- **Mini-timeline:** Filter artifacts by date range.  
- **Global filter icon:** Apply filters across views (orange when active).

## 7️⃣ Filtering Data in Belkasoft X
**Purpose:** Narrow down artifacts efficiently in large datasets.
Filtering works in:
- Artifacts window  
- Connection Graph  
- Timeline (largest dataset)

### ⚙️ Creating Filters
1. Click **funnel icon** in column header.  
2. Configure criteria (From, Message, Time, etc.).  
3. Click **Apply** → filtered list appears.
**Editing:** Reopen funnel icon to modify.  
**Clearing:** Use *Clear* or *Reset to default*.


### ➕ Multiple Criteria
Combine filters (e.g., “From” + “Message”).  
Applied filters appear highlighted in **blue**.
Use **Find** box to search large lists (e.g., contacts).  
Option *Add checked items to filter* combines multiple searches.


**🧩 Generated Filters:** Some criteria (like *Analysis result*) appear only after Belkasoft X performs AI-based analysis — e.g., detecting faces, text, or guns in images.

### 🖼️ Gallery and Global Filters
- In Gallery View → right-click to add/modify filters.  
- Global filter (blue funnel icon) applies across all lists.  
- Filters by text, date, profile, data source, or bookmark.  
- Icon turns yellow when active.

---
## 8️⃣ Searching Artifacts in Belkasoft X 🔍

### 🔹 Purpose of Searching
After artifact extraction, you may need to **search through text-based data** to locate specific evidence. Search works alongside filters to quickly narrow down the review set.
Belkasoft X automatically **indexes all text-based artifact properties** — text content, metadata, timestamps, etc. This makes searches extremely fast, even on large cases.

> ⚠️ **Note:** Don’t confuse profile search (performed during data source analysis) with artifact search (performed after extraction).  
> Example: Belkasoft X extracts an Outlook mailbox and documents first — *then* you can search inside their extracted text.

### 🧭 How to Run a Search
You can start a search in two ways:
- Press **Ctrl + F**, or  
- Go to **Dashboard → Actions → Search artifacts**
This opens the **Search window**, where you can define your search parameters.

### ⚙️ Search Options

#### 1. **Word or Phrase**
- Finds all artifacts containing a specific word or phrase.  
- **Not case-sensitive**.  
- Searches for **whole-word matches**.  
- Use `*` for partial matches.  
- Optionally enable **Treat as regex** for **regular expression** searches.
🧩 *Example:*  
- `win*` → matches *win*, *wine*, *window*  
- `*in*` → matches *skin*, *within*, *Instagram*
**Use regex when:** You don’t know the exact term (e.g., searching for unknown credit card patterns, email formats, etc.).

#### 2. **Words from File**
- Use when you have a **keyword list** (e.g., names, terms, codenames).  
- Belkasoft searches all listed words in one operation.  
- Can also treat entries as regex patterns.
🗂️ Ideal for batch keyword searches — saves time in large investigations.

#### 3. **Predefined Searches**
Belkasoft includes built-in search lists, such as:
- Adult or suspicious site names  
- City names  
- Disposable (one-time) email domains  
- Steganography or encryption app names  
📁 Path to predefined lists: `C:\Program Files\Belkasoft Evidence Center X\App\Resources\Search\Names\`
These text files are **customizable** — investigators can add or edit terms as needed.

### 🧱 Search Scope Options
At the bottom of the Search window, two dropdowns define **where** to search:
1. **Select a data source:** Choose one or multiple data sources to include.
2. **Select types to search in:** Limit the search to certain artifact types (e.g., Documents, Chats, Downloads).
Each list includes **root checkboxes** for easy bulk selection.
💡 **Tip:** It’s more efficient to search all sources first, then use filters within the *Search Results* window to narrow down.

### 🚀 Executing the Search
Click **OK** to begin. The search appears as a background process in the **Tasks window**.
Because all artifacts are indexed, searches are near-instantaneous, even with massive data volumes.

### 🧩 Special Search Operators
| Operator | Function | Example | Matches |
|-----------|-----------|----------|----------|
| `*` | Wildcard for zero or more characters | `win*` | win, wine, window |
| `?` | Wildcard for a single character | `?hat` | what, that |
| `~` | Fuzzy search (max two edits) | `what~` | what, that, hat, wat |

**Indexing:**  
All extracted artifacts (words, metadata, timestamps, etc.) are indexed for high-speed searching.  
These indexes form a **Key dictionary**, accessible from the **Dashboard → Actions** menu.

### 🧠 Related Tools
- **Regular Expression Syntax:** Advanced pattern-based search for emails, IDs, or credit cards.  
- **Search Results Window:** Displays all matching artifacts, allowing further filtering, tagging, and reporting.

---
