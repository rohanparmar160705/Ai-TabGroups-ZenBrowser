# ✨ Ai Tab Groups for Zen Browser ✨
‼️This is still Work-in-Progress ‼️

https://github.com/user-attachments/assets/fc792843-b1da-448e-ba00-63322a3d9c99


## Pre-requisites
- Enable userChrome Customizations:
    In `about:config` go to `toolkit.legacyUserProfileCustomizations.stylesheets` and set it to True.
- Install and Setup the userChrome.js Loader from [Autoconfig](https://github.com/MrOtherGuy/fx-autoconfig/tree/master)
- Install the Tab groups config from [Advanced Tab Groups](https://github.com/Anoms12/Advanced-Tab-Groups)
    If you already have a TabGroup Config you can skip this
  
## Setup and Install
- Copy and paste the `tab_sort.uc.js` file to your `chrome/JS` folder.
### AI Setup
1. For Gemini (RECOMMENDED)
    - Set `gemini { enabled:true }` in `apiConfig` and `ollama { enabled:false }` in `apiConfig`
    - Get an API Key from [Ai Studios](https://aistudio.google.com)
    - Replace `YOUR_GEMINI_API_KEY` with the copied API key
    - Dont change the gemini model since 2.0 has very low rate limits (unless you are rich ig)
2. For Ollama
    - Download and install [Ollama](https://ollama.com/)
    - Install your prefered model. The script uses  `llama3.1` by default
    - Set  `ollama { enabled:true }` in `apiConfig` and  `gemini { enabled:false }` in `apiConfig`
    - Set the model you downloaded in ollama.model: in the config (you can see the models by doing `ollama list` in terminal)
- Open Zen browser, go to `about:support` and clear start up cache.
- Done. Enjoy ^^


## How it works?

The script uses a more sophisticated multi-stage process to group your tabs:

1.  **Phase 1: Deterministic Pre-Grouping (Strong Signals):**
    *   **Opened From Same Tab:** Groups tabs that were opened from the same parent tab.
    *   **Content Type:** Identifies common content types (e.g., "Dev Docs", "Spreadsheet", "Social Media") based on URL and title patterns, then groups them.
    *   **Keywords & Hostnames:** Groups tabs sharing common keywords in their titles or identical hostnames (e.g., "github.com").

2.  **Phase 2: Similarity-Based Pre-Grouping (TF-IDF):**
    *   For tabs not caught by Phase 1, it analyzes the text content (title and description) using **TF-IDF** (Term Frequency-Inverse Document Frequency) and **Cosine Similarity**.
    *   Tabs with highly similar text content are grouped together.

3.  **Phase 3: AI-Powered Grouping:**
    *   Any tabs *still* ungrouped are sent to the configured AI (Gemini or Ollama).
    *   The AI is given the context of all previously formed groups (from Phase 1 & 2) and suggests categories for the remaining tabs, either fitting them into existing groups or proposing new ones.

4.  **Consolidation:**
    *   Finally, all generated group names are checked for near-duplicates (e.g., "Project Doc" and "Project Docs") using Levenshtein distance, and similar names are merged to ensure consistency.

*   The script primarily uses tab titles, URLs, and descriptions for context.
*   Groups are generally formed if they meet a minimum tab count (default is 2), though AI-derived groups might be created for single important tabs.
*   You can customize AI prompts and other settings in the configuration.
*   The "Clear" button only clears ungrouped, non-pinned tabs in the current workspace.

**Peace <3**

