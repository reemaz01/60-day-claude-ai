Day 40
Build Your Own AI Assistant

# Scene Partner – AI Screenwriting Assistant

## Project Overview

Scene Partner is an AI-powered browser application that helps writers practice screenplay dialogue. Users define two characters, choose a genre, describe a scene, and the AI generates screenplay-formatted dialogue while maintaining context throughout the conversation.

---

HTML FILE


[AI Assistant For ScreenPlay](scenepartner.html)


---

Screenshots

## 1. AI Assistant Interface

![AI Assistant](screenshots/home-page.png)

---

## 2. Generated Screenplay

![Generated Scene](screenshots/generated-scene.png)

---

## 3. System Prompt

![System Prompt](screenshots/system-prompt.png)

---

# System Prompt Summary

The assistant is instructed to act as a professional screenwriter instead of a chatbot.

Key behaviors:

- Generates screenplay-formatted dialogue.
- Uses screenplay tags for structured output.
- Continues scenes across multiple turns.
- Provides one concise writing tip after each response.
- Rejects off-topic requests while staying in character.
- Maintains screenplay formatting consistently.

---

# Features

- Character-based dialogue generation
- Multiple genres
- Scene length selection
- Real screenplay formatting
- Context-aware conversations
- Browser-based UI
- Direct Anthropic API integration
- Dark cinematic interface

---

# Tech Stack

- HTML
- CSS
- JavaScript
- Anthropic Claude API

---

# Key Learnings

During this project I learned:

- Designing effective system prompts is just as important as frontend development.
- Structuring AI output using custom tags makes rendering predictable.
- Maintaining conversation history is necessary because Claude's API is stateless.
- Good UI design improves the writing experience.
- Separating prompt logic from rendering logic makes the application easier to maintain.

---

# Future Improvements

- Export screenplay as PDF
- Export Final Draft (.fdx)
- Character memory across sessions
- Voice playback
- Multi-character scenes
- Beat-by-beat scene generation

---

