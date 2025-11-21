# 🧠 Project Master Plan: NeuroLens
**Slogan:** Every Brain Learns Differently  
**Hackathon Theme:** AI for Accessibility and Equity

---

## 1. Project Summary & Vision
NeuroLens is an adaptive AI learning assistant that instantly transforms standard educational materials (textbooks, PDFs, images) into personalized formats tailored to the user's neurocognitive profile.

Current education systems are designed for the "average" brain. Students with Dyslexia, ADHD, Visual Impairments, or Language Barriers often struggle with static, dense learning materials. NeuroLens bridges this gap by using Multimodal AI to "see" a textbook page and reconstruct it—changing the layout, tone, and structure to match how the user's brain processes information best.

---

## 2. Strategic Alignment (Judging Criteria)
This project is engineered to score high across all Horizon Hacks criteria:

- **Impact & Traction:** Targets a massive, underserved demographic (neurodiverse students, elderly, refugees). Creates equity by making the same information accessible to everyone.  
- **Innovation:** Goes beyond simple OCR. Uses Generative AI to rebuild content using cognitive science principles (Bionic Reading, Feynman Technique).  
- **Novelty:** Rejects the boring "file upload -> summary" pattern. Features an empathetic, gamified "Onboarding Wizard" that builds a profile for the user.  
- **Feasibility (Zero-Cost):** Architecture relies entirely on high-performance, free-tier AI models (Google Gemini 1.5 Flash), making it sustainable and accessible to deploy anywhere.

---

## 3. UI/UX Design Philosophy
**Goal:** Minimize Cognitive Load. The interface must not fight the user; it must flow with them.

- **Visual Language:** Clean whitespace, soft pastel color palettes (calming), large typography, and rounded UI elements.  
- **Onboarding:** A chat-based, step-by-step "Wizard" rather than static forms.  
- **Accessibility (A11y):** High contrast modes, screen reader compatibility, keyboard navigation support.  
- **Feedback:** "Breathable" loading animations to reduce anxiety during processing.

---

## 4. Detailed User Flow (The "Wizard")
The application follows a linear, 6-step narrative flow designed to build empathy.

### Step 1: Splash & Vision
- **Visual:** A pulsing, modern "Brain/Lens" logo in the center.  
- **Text:** "Breaking barriers in education."  
- **Action:** Single button: "Start Journey".

### Step 2: Identity
- **AI Persona:** Warm and supportive.  
- **Prompt:** "Hello! I am NeuroLens. How should I address you?"  
- **Interaction:** Typing the name triggers a personalized greeting animation.

### Step 3: Context (Age/Level)
- **Prompt:** "Nice to meet you, [Name]! 🚀 What is your current education level?"  
- **Selection:**  
  - 🎒 Primary (7-10): Triggers simple language & emojis.  
  - 🏫 High School (11-17): Triggers relatable, peer-level tone.  
  - 🎓 University/Pro: Triggers academic precision.

### Step 4: Goal Setting
- **Prompt:** "How can I help you today?"  
- **Selection:**  
  - 📝 Exam Prep: Focuses on bullet points & active recall.  
  - 📚 Deep Understanding: Focuses on analogies & storytelling.  
  - 🌍 Language Help: Focuses on translation support.

### Step 5: The "Superpower" (Mode Selection)
- **Prompt:** "What is the hardest part about reading for you? I will adapt the page to fit your brain."  
- **Grid Menu:**  
  - 🧠 Laser Focus (ADHD)  
  - 📖 Easy Read (Dyslexia)  
  - 👶 Feynman (Simplify)  
  - 🌉 Language Bridge (Global)  
  - 👁️ Eagle Eye (Vision)  
  - 🃏 Flashcards (Exam)

### Step 6: Input & Magic
- **Action:** "Open Camera" or "Upload Image".  
- **Process:** A "Neuro-transformation" loading screen.  
- **Result:** A split-screen view (Original vs. AI Adapted Content).

---

## 5. Technical Specifications & Mode Logic

### A. Architecture (Zero-Cost Stack)
- **Frontend:** React.js (Vite), Tailwind CSS, Framer Motion.  
- **Backend:** Python (FastAPI).  
- **AI Engine:** Google Gemini 1.5 Flash (Free Tier via Google AI Studio).  
  - **Why Gemini Flash?** Multimodal (can see images natively), extremely fast, large context window, free for up to 15 RPM.  
- **TTS (Text-to-Speech):** Browser Native `window.speechSynthesis` API (Zero cost, no external API needed).

### B. Mode Logic (Prompt Engineering + CSS)
The backend receives the image and the selected mode. It constructs a specific prompt for Gemini to generate HTML content.

1. **ADHD Mode (Laser Focus)**
   - **Frontend:** `font-family: Inter`, increased line height, "Focus Green" background accents.  
   - **AI Instruction:** "Simulate Bionic Reading. Wrap the first few letters of every word in `<b>` tags. Break long paragraphs into short chunks. Add '🔑 Key Takeaway' summaries at the end of sections."

2. **Dyslexia Mode (Easy Read)**
   - **Frontend:** `font-family: OpenDyslexic` (custom font), increased letter spacing, background "Cream/Off-White" (#FFFDD0) to reduce visual stress.  
   - **AI Instruction:** "Rewrite complex sentences into simple, linear structures (Subject-Verb-Object). Avoid italics. Use clear, unambiguous language."

3. **Simplification Mode (Feynman)**
   - **AI Instruction:** "Act as a tutor for a [User Age] year old. Identify complex jargon and replace it with simple analogies. (e.g., 'Mitochondria' -> 'Energy Factory'). Use ASCII art diagrams where possible to explain concepts."

4. **Language Bridge Mode (Global)**
   - **AI Instruction:** "Keep the text in the original language. However, identify difficult academic terms and insert the user's native language translation in parentheses immediately after the word. Example: 'Velocity (TR: Hız)'."

5. **High Visibility Mode (Eagle Eye)**
   - **Frontend:** High Contrast Theme (Black Background, Neon Yellow Text). Maximize font size.  
   - **AI Instruction:** "Extract only the core text. Remove all decorative descriptions. Format as a clean, large-print list."

6. **Flashcard Mode (Exam)**
   - **AI Instruction:** "Analyze the image and generate a JSON output of Question-Answer pairs based on the material. Format: `[{ 'q': '...', 'a': '...' }]`."  
   - **Frontend:** Renders interactive flip-cards based on the JSON response.

---

## 6. Implementation Plan (Prompt for LLM Developer)
If you are an AI assistant helping me build this, please follow these constraints:

- **No Paid APIs:** Use only `google-generativeai` library for Python.  
- **Mock Data:** If the API fails during testing, provide a robust mock response so the UI development doesn't stop.  
- **Styling:** Use Tailwind CSS for all styling. Ensure the design is "Mobile First".  
- **Code Structure:** Keep the React components modular (`Onboarding.jsx`, `ResultView.jsx`, `ModeSelector.jsx`).  
