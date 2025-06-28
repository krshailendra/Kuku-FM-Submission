# Multi-Agentic Prompt-to-Video Generation Pipeline

![Pipeline Overview](image1)

This project implements an end-to-end system for transforming textual prompts into audio-synchronized videos with expressive speech, stylized visuals, and precise narration alignment. The architecture leverages multi-agent LLMs, deep learning-based speech and emotion models, and advanced audio-visual processing. Below, we map every pipeline block (see diagram above) to the codebase and describe the technical components.

---

## 1. Input

- **Types:** Prompt (text), Audio+Text, Audio+Script
- **Entry Point:** User provides a prompt or a combination of audio and text/script.

---

## 2. Multi-Agentic Script Writer

- **Code:** [`Codes/Multiagentic Script Writer.ipynb`](Codes/Multiagentic%20Script%20Writer.ipynb)
- **Description:** Uses AutoGen to orchestrate 6 GPT-4-based agents, each responsible for a specific aspect of script generation (plot, dialogue, consistency, fact-checking, etc.).
- **Technical highlights:**
    - AutoGen LLM orchestration (`pyautogen`, `autogen-agentchat`)
    - Modular agent roles for coherence and creativity
    - Output: Draft script

---

## 3. Script Finaliser

- **Code:** [`Codes/Script Finaliser.ipynb`](Codes/Script%20Finaliser.ipynb)
- **Description:** Finalizes the draft script, injecting emotion markers and refining for audio effects.
- **Technical highlights:**
    - Emotion classification using BERT (`j-hartmann/emotion-english-distilroberta-base`)
    - Effect phrase mapping for expressive narration
    - Output: Finalized script with embedded effects

---

## 4. Script Parsing & Reporting

- **Code:** [`Codes/Script Parser Report Generator.ipynb`](Codes/Script%20Parser%20Report%20Generator.ipynb)
- **Description:** Analyzes the finalized script to extract structure, cues, and metadata for downstream processing.
- **Technical highlights:**
    - Scripting parsing and structure analysis
    - LangChain & FAISS for document handling

---

## 5. Thumbnail Generation & Style Transfer

- **Block:** Thumbnail Generator → Style Transfer GAN
- **Description:** Generates multiple thumbnail styles using GAN-based transfer for visual diversity.
- **(Code for these blocks not explicitly found, but referenced in your design.)**

---

## 6. TTS (Text-to-Speech) & Audio Synthesis

- **Code:** [`Codes/TTS.ipynb`](Codes/TTS.ipynb)
- **Description:** Converts script (with emotion tags) into expressive speech using TTS models (e.g., Kokoro-82M, OpenAI TTS).
- **Technical highlights:**
    - Emotion-synchronized voice synthesis
    - Integration with BERT emotion tags for prosody control

---

## 7. Audio Editing

- **Code:** [`Codes/Audio Editor.ipynb`](Codes/Audio%20Editor.ipynb)
- **Description:** Post-processes audio for background overlays, silence removal, and fade effects using `pydub`.
- **Technical highlights:**
    - Automated background/music overlay
    - Silence trimming, fade-in/out for naturalness

---

## 8. Transcription

- **Code:** [`Codes/Transcriber.ipynb`](Codes/Transcriber.ipynb)
- **Description:** Uses Whisper for accurate speech-to-text, enabling precise alignment of audio and script.
- **Technical highlights:**
    - OpenAI Whisper for robust ASR
    - Output: segmented, timestamped transcripts

---

## 9. Voice Cloning

- **Block:** Voice Cloner (details not in notebooks)
- **Description:** Clones voice for narration, ensuring consistency and personalization.

---

## 10. Audio Effects

- **Block:** Audio Effects (detailed in Audio Editor)
- **Description:** Adds further audio enhancements to the final track.

---

## 11. Synchronizer & Synchronized Visuals

- **Block:** ITS Synchronizer → Synchronized Visuals
- **Description:** Aligns script, audio, and visuals frame-by-frame (~24fps) for coherent video output.
- **Technical highlights:**
    - Uses transcript timing to synchronize generated visuals (e.g., via Stable Diffusion)
    - Automated thumbnail and scene style transfer for each segment

---

## 12. Output

- **Final Products:**
    - **Audio:** Emotion-rich narration, background effects, and voice cloning
    - **Video:** Synchronized visuals and thumbnails generated per script scene
    - **All outputs are fully automated and scalable**

---

## Key Technical Numbers

- **6 specialized GPT-4 agents** (AutoGen) for script generation
- **BERT-based emotion tagging** for every script segment
- **Kokoro-82M TTS** for high-fidelity, emotion-synced narration
- **Whisper ASR** for frame-accurate transcript alignment
- **24fps** video generation for smooth, natural output

---

## References

- See pipeline diagram above for the full architecture and flow.
- Notebooks are modular; each can be executed and tested independently.
- For more details on each block, refer to the respective Jupyter notebook.

---

## Credits

- System design, implementation, and technical contributions by the project team.