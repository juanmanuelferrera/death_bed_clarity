---
name: clipboard
description: Format the last produced text with proper paragraphs, add a title with emojis, and copy to clipboard
user-invocable: true
disable-model-invocation: true
---

# /clipboard — Format and Copy to Clipboard

Take the last text produced in this conversation, format it properly, and copy it to the system clipboard.

## Steps

1. **Identify the last text produced** in the conversation (article, summary, response, etc.)
2. **Fix paragraphs**: Ensure proper paragraph separation with blank lines between sections
3. **Add a title**: Create an appropriate title at the very first line using relevant emojis that match the topic
4. **On the next line**, place the formatted text with corrected paragraphs
5. **Copy to clipboard**: Use `pbcopy` via Bash to copy the complete formatted text (title + body) to the system clipboard
6. **Confirm** to the user that it has been copied

## Rules

- Always use emojis in the title that are relevant to the content
- Keep paragraph spacing clean — one blank line between paragraphs
- Do not alter the meaning or content of the text, only fix formatting
- Use `pbcopy` to copy to the macOS clipboard
- Confirm when done
