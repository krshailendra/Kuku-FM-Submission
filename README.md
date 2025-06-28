# 🚀 Multi-Agentic Prompt-to-Content (Audio + Video) Generation Pipeline

---

## 🤖 How Our Solution Automates Content Generation for Kuku FM

Our multi-agentic pipeline provides a comprehensive, fully automated content generation system tailored for Kuku FM’s needs:

- **🔁 End-to-End Workflow:** The entire journey from prompt or idea to final audio-visual output is automated, requiring minimal human intervention. This matches Kuku FM’s vision of scaling content production using generative AI.
- **👥 Multi-Agent Collaboration:** By leveraging specialized GPT-4 agents for ideation, writing, editing, and fact-checking, the system ensures each piece of content is creative, coherent, and accurate.
- **🎭 Emotionally-Rich Narration:** Automated emotion tagging with BERT and expressive voice synthesis using Kokoro-82M bring human-like emotion and engagement to each story, elevating listener experience.
- **🎶 Personalized Audio Editing:** Background music, silence removal, and fade effects are dynamically applied based on detected emotions, ensuring polished and immersive audio quality.
- **⚡ Rapid Turnaround & Scale:** The pipeline can operate 24/7, generating hundreds or thousands of scripts and corresponding audio episodes daily, supporting Kuku FM’s goal of scalable, personalized content creation.
- **🖼️ Seamless Visual Integration:** Thumbnails and synchronized visuals are generated automatically, enabling rapid production of engaging audio-visual content for social media and in-app promotion.
- **💸 Reduced Costs & Faster Time-to-Market:** By automating routine content creation tasks, Kuku FM can significantly reduce reliance on large creative teams while maintaining high content quality and variety.

Together, these features make our solution a perfect fit for Kuku FM’s mission to use generative AI for scalable, high-quality, and engaging audio content that attracts and retains listeners at scale.

---

![Pipeline Diagram](https://github.com/user-attachments/assets/cea709c7-cd75-4e41-86f7-a7ed76f2de21)

This project implements an end-to-end system for transforming textual prompts into audio-synchronized videos with expressive speech, stylized visuals, and precise narration alignment. The architecture leverages multi-agent LLMs, deep learning-based speech and emotion models, and advanced audio-visual processing. Below, we map every pipeline block (see diagram above) to the codebase and describe the technical components.

---

> **🗂️ Output Samples:**  
All generated outputs—including finalized scripts, audio files, and video samples from the automated pipeline—are available for review in the following Google Drive folder: [Project Outputs on Google Drive](https://drive.google.com/drive/folders/1pYmqrKBPigrozc9iqW0ZCftgiU7IyKNa).  
This repository of outputs demonstrates the end-to-end capabilities of our system, showcasing examples of emotion-tagged scripts, expressive audio narration, audio-visual synchronization, and stylized thumbnails as produced by each stage of the pipeline.

---

## 1️⃣ Input

- **Types:** Prompt (text), Audio+Text, Audio+Script
- **Entry Point:** User provides a prompt or a combination of audio and text/script.

---

## 2️⃣ Multi-Agentic Script Writer

- **Code:** [`Codes/Multiagentic Script Writer.ipynb`](Codes/Multiagentic%20Script%20Writer.ipynb)
- **Description:** Uses AutoGen to orchestrate 6 GPT-4-based agents, each responsible for a specific aspect of script generation (plot, dialogue, consistency, fact-checking, etc.).
- **Technical highlights:**
    - 🧠 AutoGen LLM orchestration (`pyautogen`, `autogen-agentchat`)
    - 🤝 Modular agent roles for coherence and creativity
    - ✍️ Output: Draft script

---

## 3️⃣ Script Finaliser

- **Code:** [`Codes/Script Finaliser.ipynb`](Codes/Script%20Finaliser.ipynb)
- **Description:** Finalizes the draft script, injecting emotion markers and refining for audio effects.
- **Technical highlights:**
    - 🧑‍💻 Emotion classification using BERT (`j-hartmann/emotion-english-distilroberta-base`)
    - 🎬 Effect phrase mapping for expressive narration
    - 📜 Output: Finalized script with embedded effects

---

## 4️⃣ Script Parsing & Reporting

- **Code:** [`Codes/Script Parser Report Generator.ipynb`](Codes/Script%20Parser%20Report%20Generator.ipynb)
- **Description:** Analyzes the finalized script to extract structure, cues, and metadata for downstream processing.
- **Technical highlights:**
    - 📄 Scripting parsing and structure analysis
    - 🔍 LangChain & FAISS for document handling

---

## 5️⃣ Thumbnail Generation & Style Transfer

- **Block:** Thumbnail Generator → Style Transfer GAN
- **Description:** Generates multiple thumbnail styles using GAN-based transfer for visual diversity.
- **🖌️ (Code for these blocks not explicitly found, but referenced in your design.)**

---

## 6️⃣ TTS (Text-to-Speech) & Audio Synthesis

- **Code:** [`Codes/TTS.ipynb`](Codes/TTS.ipynb)
- **Description:** Converts script (with emotion tags) into expressive speech using TTS models (e.g., Kokoro-82M, OpenAI TTS).
- **Technical highlights:**
    - 🗣️ Emotion-synchronized voice synthesis
    - 🎤 Integration with BERT emotion tags for prosody control

---

## 7️⃣ Audio Editing

- **Code:** [`Codes/Audio Editor.ipynb`](Codes/Audio%20Editor.ipynb)
- **Description:** Post-processes audio for background overlays, silence removal, and fade effects using `pydub`.
- **Technical highlights:**
    - 🎵 Automated background/music overlay
    - ✂️ Silence trimming, fade-in/out for naturalness

---

## 8️⃣ Transcription

- **Code:** [`Codes/Transcriber.ipynb`](Codes/Transcriber.ipynb)
- **Description:** Uses Whisper for accurate speech-to-text, enabling precise alignment of audio and script.
- **Technical highlights:**
    - 🔊 OpenAI Whisper for robust ASR
    - ⏱️ Output: segmented, timestamped transcripts

---

## 9️⃣ Voice Cloning

- **Block:** Voice Cloner (details not in notebooks)
- **Description:** Clones voice for narration, ensuring consistency and personalization.

---

## 🔟 Audio Effects

- **Block:** Audio Effects (detailed in Audio Editor)
- **Description:** Adds further audio enhancements to the final track.

---

## 1️⃣1️⃣ Synchronizer & Synchronized Visuals

- **Block:** ITS Synchronizer → Synchronized Visuals
- **Description:** Aligns script, audio, and visuals frame-by-frame (~24fps) for coherent video output.
- **Technical highlights:**
    - 🎬 Uses transcript timing to synchronize generated visuals (e.g., via Stable Diffusion)
    - 🏞️ Automated thumbnail and scene style transfer for each segment

---

## 1️⃣2️⃣ Output

- **Final Products:**
    - 🎧 **Audio:** Emotion-rich narration, background effects, and voice cloning
    - 🎞️ **Video:** Synchronized visuals and thumbnails generated per script scene
    - 🤖 **All outputs are fully automated and scalable**

---

## 🔢 Key Technical Numbers

- **6 specialized GPT-4 agents** (AutoGen) for script generation
- **BERT-based emotion tagging** for every script segment
- **Kokoro-82M TTS** for high-fidelity, emotion-synced narration
- **Whisper ASR** for frame-accurate transcript alignment
- **24fps** video generation for smooth, natural output

---

## 📚 References

- See pipeline diagram above for the full architecture and flow.
- Notebooks are modular; each can be executed and tested independently.
- For more details on each block, refer to the respective Jupyter notebook.
