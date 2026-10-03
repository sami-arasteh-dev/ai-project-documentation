# AI Project Documentation Studio

A client-side web application that analyzes your project's source code files to automatically generate professional GitHub READMEs and website introduction copy using AI.

## 📋 Table of Contents
- [Features](#features)
- [Architecture & Tech Stack](#architecture--tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Universal Translator Engine](#universal-translator-engine)
- [Security & Privacy](#security--privacy)
- [Development](#development)

## ✨ Features

*   **Code-Based Analysis:** Ingests actual project files (HTML, PHP, JS, CSS, JSON, MD, TXT) to ensure generated documentation reflects real capabilities.
*   **Dual Output Generation:**
    *   **Website Copy:** Marketing-ready text for project landing pages.
    *   **GitHub README:** Structured Markdown with features, architecture, installation, and usage.
*   **Customizable AI Parameters:**
    *   **Language:** Support for Persian, English, Arabic, Turkish, German, and French.
    *   **Tone:** Professional, Technical, Startup, Friendly, Minimal.
    *   **Length:** Short, Medium, Long, Very Long.
*   **Universal Translator Engine:** A built-in Persian-to-English translation module with:
    *   In-memory, LocalStorage, and IndexedDB caching.
    *   SHA-256 hash-based cache keys.
    *   Dynamic DOM translation with `MutationObserver` support.
    *   Glossary support for forced translations.
*   **Privacy-First Design:** All processing happens in the browser. API keys are not hardcoded in the main UI (though the translator engine allows for private key storage).

## 🏗 Architecture & Tech Stack

*   **Frontend:** Vanilla HTML5, CSS3, JavaScript (ES6+).
*   **AI Integration:** Compatible with OpenAI-compatible APIs (e.g., GapGPT, Qwen).
*   **Caching:**
    *   `Map` for in-memory caching.
    *   `localStorage` for persistent lightweight caching.
    *   `IndexedDB` for large-scale translation storage.
*   **Security:** No server-side backend; client-side only.

## 📦 Prerequisites

*   A modern web browser (Chrome, Firefox, Edge, Safari).
*   An API Key from an AI provider (e.g., GapGPT, OpenAI).
*   Basic understanding of project file structures.

## 🚀 Installation

Since this is a static client-side application, no build process is required.

1.  Clone the repository or download the `github-ready.html` file.
2.  Open `github-ready.html` in any modern web browser.

```bash
git clone <repository-url>
cd <project-directory>
# Open index.html or github-ready.html in your browser
```

## 🖥 Usage

### Generating Documentation

1.  **Connect AI:**
    *   Enter your **API Base URL** (e.g., `https://api.gapgpt.app/v1`).
    *   Enter your **API Key**.
    *   Select the **Model** (e.g., `gapgpt-qwen-3.6`).
2.  **Configure Output:**
    *   Select **Output Language** (e.g., English, Persian).
    *   Choose **Tone** (e.g., Professional, Technical).
    *   Set **Output Length** (e.g., Medium).
3.  **Project Details:**
    *   Enter the **Project Name**.
    *   (Optional) Add a **Project Goal/Description** for context.
4.  **Upload Files:**
    *   Drag and drop your project files into the drop zone.
    *   Supported formats: HTML, PHP, JS, CSS, JSON, MD, TXT.
    *   *Note: Files are limited to 2MB each.*
5.  **Generate:**
    *   Click **"Analyze & Generate"**.
    *   Wait for the AI to process the files.
    *   View the generated **Website Intro** and **GitHub README** in the output panels.
6.  **Export:**
    *   Click **Copy** to copy text to clipboard.
    *   Click **Download** to save as `.txt` or `.md` files.

### Using the Universal Translator

1.  Look for the floating translation button (🇬🇧/🇮🇷) in the bottom-right corner.
2.  Click to toggle between Persian and English.
3.  The engine will automatically translate visible text, placeholders, titles, and ARIA labels.
4.  Translations are cached for performance.

## ⚙️ Configuration

### AI Settings
*   `baseUrl`: The endpoint for the AI API.
*   `apiKey`: Your secret API key.
*   `model`: The specific model identifier.
*   `temperature`: Creativity level (0.0 - 1.0).
*   `maxTokens`: Maximum output length.

### Translator Settings (in `<script>` block)
*   `apiKey`: Private API key for the translator engine.
*   `endpoint`: Translator API endpoint.
*   `glossary`: Object for forcing specific translations (e.g., `"شبکه افکار": "Thought Network"`).
*   `ignoredTags`: HTML tags to skip during translation (e.g., `SCRIPT`, `STYLE`).

## 🌐 Universal Translator Engine

This project includes a sophisticated translation engine (`Universal Translator Engine v3`) with the following capabilities:

*   **Multi-Layer Caching:** Uses `Map`, `localStorage`, and `IndexedDB` to minimize API calls and improve performance.
*   **Batch Processing:** Translates text in batches to optimize API usage.
*   **Dynamic DOM Support:** Uses `MutationObserver` to translate content added dynamically after page load.
*   **Attribute Translation:** Translates `placeholder`, `title`, `aria-label`, and `alt` attributes.
*   **Cache Management:**
    *   `window.UniversalTranslator.cacheInfo()`: View cache statistics.
    *   `window.UniversalTranslator.clearCache()`: Clear all cached translations.

## 🔒 Security & Privacy

*   **Client-Side Only:** No data is sent to a central server. All file processing and AI requests happen in the user's browser.
*   **API Key Handling:**
    *   In the main UI, the API key is entered into an input field and used only for the session.
    *   The translator engine allows for a hardcoded API key for private project use (as seen in the source).
*   **File Privacy:** Uploaded files are read locally and sent directly to the AI API. They are not stored by this application.

## 🛠 Development

### Project Structure
```
github-ready.html
├── HTML Structure
├── CSS Styles (Dark Theme)
├── Main Logic (Documentation Generator)
└── Translator Engine (Universal Translator v3)
```

### Adding New Languages
To add a new language to the dropdown, update the `<select id="language">` element in the HTML:
```html
<option value="Spanish">Español</option>
```

### Customizing the Prompt
The AI prompt is constructed in the `buildPrompt()` function. You can modify the system instructions or output format requirements there.

## 📄 License

This project is provided as-is. Ensure you comply with the terms of service of the AI provider you choose to use.
