# LeekHunter – Architecture Overview (Alpha)

---

## 🔧 Purpose

LeekHunter is an AI-powered bug detector designed to analyze source code using Gemini API and highlight potential bugs directly within the developer's code editor (VS Code). This document outlines the system’s architecture and its key components.

---

## 🧱 System Components

### 1. **Prompt Engine**
- **Language:** TypeScript / Python (For Now)
- **Role:** Constructs structured prompts for the Gemini API and injects code dynamically.
- **Future:** Custom fine-tuned LLM may replace Gemini later.
- **Status:** Actively tested with multiple prompt versions.

### 2. **Gemini API (GoogleGenAI)**
- **Library:** `google.generativeai`
- **Usage:** Sends prompt + code → Receives JSON response
- **Status:** Stable; verified for multiple prompt versions

### 3. **Bug Parser / Validator (Planned)**
- Parses and validates JSON from Gemini
- Ensures correct field types: `bug_description`, `fix_suggestion`, `line_number`, `severity_level`
- ***NOTE***: Validations are performed manually 

### 4. **Code Scanner (Planned)**
- Scans project files in a directory (multi-language support: Python, JS, TS)
- Feeds each file into the prompt engine

### 5. **VS Code Extension (Planned)**
- Highlights bugs in real-time using the VS Code diagnostics API
- Displays bug tooltips: line number, severity, fix
- Optionally shows fix suggestions in a sidebar or hover card

---

## 🔄 Data Flow Diagram (Text-Based for Now)

```text
User Code File (.py, .js)
        ↓
   Code Scanner (Planned)
        ↓
   Prompt Engine (Python)
        ↓
   Gemini API (google.generativeai)
        ↓
Structured JSON Response (bug list)
        ↓
Bug Parser → UI Output / Logging (Planned)