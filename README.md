# Cursor Chat RTL Helper

Small helper script to make Cursor's chat interface display messages in **right‑to‑left (RTL)** layout for languages like Persian/Arabic, while keeping all **code blocks and editors left‑to‑right (LTR)**.

The script only changes text direction and alignment. **Fonts and sizes stay exactly as Cursor defines them.**

---

## Features

- 🔁 RTL layout for:
  - AI messages
  - User messages
  - Message lists and basic markdown content
- ↔️ Keep code strictly LTR:
  - Chat code blocks
  - Syntax‑highlighted code
  - Monaco editor (main code editor)
- No dependencies, no extensions – just a DevTools snippet.

---

## How to use (Desktop Cursor)

1. **Open Developer Tools**
   - In Cursor, press: `Ctrl + Shift + P`
   - Type: `Toggle Developer Tools` and run it  
   *(or use `Ctrl + Shift + I` if it works on your system)*

2. **Create a Snippet**
   - In the DevTools window, go to the `Sources` tab.
   - Open the `Snippets` section.
   - Create a new snippet (e.g. `cursor-rtl.js`).

3. **Paste this script into the snippet**

```js
(function () {
    const existing = document.getElementById('cursor-rtl-style');
    if (existing) existing.remove();

    const style = document.createElement('style');
    style.id = 'cursor-rtl-style';

    style.textContent = `
        /* Chat markdown & messages: RTL */
        .markdown-root,
        .markdown-root *,
        div[class*="markdown"],
        div[class*="Markdown"],
        div[data-message-role="ai"] .markdown-root,
        div[data-message-role="user"] .markdown-root {
            direction: rtl !important;
            text-align: right !important;
        }

        /* Chat input (composer) RTL */
        .aislash-editor-input, 
        .aislash-editor-input-readonly,
        .composer-human-message {
            direction: rtl !important;
            text-align: right !important;
        }

        .aislash-editor-placeholder {
            direction: rtl !important;
            text-align: right !important;
            right: 15px !important;
            left: auto !important;
        }

        /* Lists in markdown */
        .markdown-root ul, 
        .markdown-root ol {
            padding-right: 20px !important;
            padding-left: 0 !important;
        }

        /* Tables: outer LTR scroll, inner RTL content */
        .markdown-table-container {
            direction: ltr !important;
            overflow-x: auto !important;
            max-width: 100% !important;
            display: block !important;
            border-radius: 4px;
        }
        
        table.markdown-table {
            direction: rtl !important;
            width: max-content !important;
            min-width: 100% !important;
            border-collapse: collapse !important;
        }

        .markdown-table th,
        .markdown-table td {
            text-align: right !important;
            border: 1px solid var(--vscode-textSeparator-foreground, #444) !important;
            padding: 6px 10px !important;
        }

        /* Chat code blocks: force LTR, keep Cursor's fonts/sizes */
        .composer-message-codeblock,
        .composer-message-codeblock *,
        .ui-code-block,
        .ui-code-block *,
        .ui-default-code,
        .ui-default-code *,
        .ui-default-code__content,
        .ui-default-code__line,
        .ui-default-code__line-content,
        pre,
        code {
            direction: ltr !important;
            text-align: left !important;
            unicode-bidi: plaintext !important;
        }

        .composer-message-codeblock {
            direction: ltr !important;
            text-align: left !important;
        }

        /* Monaco editor: always LTR */
        .monaco-editor,
        .monaco-editor * {
            direction: ltr !important;
            text-align: left !important;
            unicode-bidi: plaintext !important;
        }

        /* Plan / questionnaire UI RTL (if present) */
        #composer-toolbar-section,
        .composer-questionnaire-toolbar {
            direction: rtl !important;
            text-align: right !important;
        }

        .composer-questionnaire-toolbar-header {
            direction: rtl !important;
            display: flex !important;
            flex-direction: row !important;
            justify-content: space-between !important;
        }

        .composer-questionnaire-toolbar-question-label {
            text-align: right !important;
            direction: rtl !important;
        }

        .composer-questionnaire-toolbar-option {
            direction: rtl !important;
            display: flex !important;
            flex-direction: row !important;
            align-items: center !important;
            justify-content: flex-start !important;
            text-align: right !important;
        }

        .composer-questionnaire-toolbar-option-label {
            margin-right: 8px !important;
            margin-left: 0 !important;
        }

        .composer-questionnaire-toolbar-freeform-input {
            text-align: right !important;
            direction: rtl !important;
        }

        .composer-questionnaire-toolbar-actions {
            direction: rtl !important;
            display: flex !important;
            flex-direction: row-reverse !important;
            justify-content: flex-end !important;
        }
    `;

    document.head.appendChild(style);

    const targets = document.querySelectorAll('.markdown-root');
    console.log('RTL style injected (markdown-root RTL, code LTR). Matched markdown-root:', targets.length);
})();
