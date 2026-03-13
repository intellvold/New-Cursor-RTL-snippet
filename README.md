(function () {
    const existing = document.getElementById('cursor-rtl-style');
    if (existing) existing.remove();

    const style = document.createElement('style');
    style.id = 'cursor-rtl-style';

    style.textContent = `
        /* --- 1. متن پیام‌های AI و کاربر (RTL + فونت مناسب) --- */
        .markdown-root,
        .markdown-root *,
        div[class*="markdown"],
        div[class*="Markdown"],
        div[data-message-role="ai"] .markdown-root,
        div[data-message-role="user"] .markdown-root {
            direction: rtl !important;
            text-align: right !important;
            font-size: 16px !important;      /* کمی بزرگ‌تر از پیش‌فرض، کوچیک‌تر از 18 */
            line-height: 1.9 !important;
        }

        /* ورودی کاربر پایین صفحه */
        .aislash-editor-input, 
        .aislash-editor-input-readonly,
        .composer-human-message {
            direction: rtl !important;
            text-align: right !important;
            font-size: 16px !important;
            line-height: 1.9 !important;
        }

        .aislash-editor-placeholder {
            direction: rtl !important;
            text-align: right !important;
            right: 15px !important;
            left: auto !important;
        }

        /* لیست‌ها */
        .markdown-root ul, 
        .markdown-root ol {
            padding-right: 20px !important;
            padding-left: 0 !important;
        }

        /* جدول‌ها (مثل قبل) */
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

        /* --- 2. کدها کاملاً LTR + فونت نرمال --- */
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
            font-size: 13px !important;      /* اندازه مناسب برای کد */
            line-height: 1.6 !important;
        }

        /* اطمینان از اینکه بلوک کد تحت تأثیر RTL والد قرار نگیرد */
        .composer-message-codeblock {
            direction: ltr !important;
            text-align: left !important;
        }

        /* ویرایشگر موناکو (ادیتور کد اصلی) */
        .monaco-editor,
        .monaco-editor * {
            direction: ltr !important;
            text-align: left !important;
            unicode-bidi: plaintext !important;
        }

        /* --- 3. Plan / Questionnaire (در صورت وجود) --- */
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
