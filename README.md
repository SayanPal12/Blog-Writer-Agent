# 🧠 LangGraph Blog Writing Agent

An end-to-end **multi-agent blog generation system** that plans, researches, writes, and enhances technical blog posts using LLM orchestration.

Built with **LangGraph, Groq LLMs, and Streamlit**, this project demonstrates a structured approach to long-form content generation using modular agents.

---

## 🚀 What This Project Does

Given a topic, the system:

1. **Decides whether research is needed**
2. **Fetches relevant evidence (if required)**
3. **Generates a structured blog plan**
4. **Writes sections in parallel**
5. **Merges content into a final blog**
6. **Optionally generates diagrams/images**
7. **Outputs production-ready Markdown**

---

## 🧩 Architecture Overview

This project uses a **graph-based multi-agent workflow**:

```
Router → Research → Planner → Workers → Reducer → Image Generator
```

### Core Components

* **Router**

  * Classifies the task as:

    * `closed_book` (no research)
    * `hybrid` (partial research)
    * `open_book` (fully research-driven)
  * Generates search queries when needed

* **Research Agent**

  * Uses Tavily search
  * Extracts and deduplicates structured evidence

* **Orchestrator (Planner)**

  * Creates a structured blog outline
  * Defines:

    * Goals
    * Subtopics
    * Word targets
    * Requirements (code, citations, etc.)

* **Worker Agents**

  * Each worker writes one section
  * Enforces:

    * Bullet coverage
    * Target word count
    * Optional citations/code

* **Reducer**

  * Merges all sections into final Markdown
  * Maintains ordering and structure

* **Image Pipeline**

  * Decides if diagrams are useful
  * Generates images using diffusion models
  * Injects them into the blog

---

## ✨ Features

### 🔍 Intelligent Research Routing

* Automatically determines when external knowledge is required
* Avoids unnecessary API calls for evergreen topics

### 🧠 Structured Planning

* Enforces high-quality blog outlines
* Prevents vague or redundant sections

### ⚡ Parallel Section Generation

* Multiple workers generate content simultaneously
* Improves speed and modularity

### 📚 Evidence-Grounded Writing

* Supports citation-based writing
* Prevents hallucinated claims in research mode

### 🧪 Code + Technical Depth

* Sections can include:

  * Minimal working examples
  * Debugging insights
  * Performance considerations

### 🖼️ Automated Diagram Generation

* Adds diagrams only when they improve understanding
* Avoids decorative or useless visuals

### 🧾 Streamlit UI

* Interactive interface to:

  * Generate blogs
  * View plans and evidence
  * Preview Markdown
  * Download outputs

### 📦 Export Options

* Markdown download
* Full bundle (Markdown + images)

---

## 🛠️ Tech Stack

* **LangGraph** – agent orchestration
* **Groq LLMs** – fast inference (LLaMA variants)
* **LangChain** – structured prompting + tools
* **Tavily API** – web search
* **Streamlit** – frontend UI
* **HuggingFace Inference** – image generation

---

## 📂 Project Structure

```
.
├── backend.py      # Core LangGraph pipeline
├── frontend.py     # Streamlit UI
├── images/         # Generated diagrams
├── *.md            # Generated blogs
```

---

## ⚙️ Setup

### 1. Install dependencies

```
pip install -r requirements.txt
```

### 2. Set environment variables

Create a `.env` file:

```
HF_TOKEN=your_huggingface_token
GROQ_API_KEY=your_groq_key
TAVILY_API_KEY=your_tavily_key
```

---

### 3. Run the app

```
streamlit run frontend.py
```

---

## 🧪 Example Workflow

1. Enter a topic:

   ```
   "How Retrieval-Augmented Generation works"
   ```

2. System:

   * Detects hybrid mode
   * Fetches recent sources
   * Builds structured plan

3. Output:

   * Multi-section blog
   * Code snippets
   * Diagrams (if useful)

---

## ⚠️ Limitations (Read This)

* No caching → repeated runs cost more
* Research quality depends on Tavily results
* Image generation may fail silently (fallback included)
* No evaluation metrics (yet)

---

## 🔮 Future Improvements

* Add caching layer for research + generation
* Add evaluation (BLEU / human scoring / rubric-based)
* Support multi-language output
* Improve image consistency (currently prompt-based)
* Add versioning for generated blogs

---

## 💡 Why This Matters

Most “AI blog generators” are just prompt wrappers.

This system:

* Breaks the task into **reasoned steps**
* Uses **structured intermediate representations**
* Enforces **quality constraints at every stage**

That’s the difference between:

> “Generate a blog”
> vs
> “Design a system that produces good blogs consistently”

---

## 🧑‍💻 Author

Built as a **multi-agent LLM system** exploring structured generation, planning, and orchestration.

---

## 📜 License

MIT License
