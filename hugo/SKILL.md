---
name: hugo
description: Format text into a bilingual ISKCON article for Hugo blog — Spanish prose + English with front matter
user-invocable: true
disable-model-invocation: true
---

# /hugo — Hugo ISKCON Article Formatter

Take any text about psychology, narcissism, abuse, manipulation, or related topics and adapt it into a blog article connecting it with the phenomenon of false Vaishnavite gurus in ISKCON.

## Steps

1. **Clean up the text** if it comes from subtitles, transcriptions, or fragmented sources — reconstruct it as coherent prose.

2. **Adapt the content to ISKCON context**: Establish explicit parallels between the psychological concepts in the source text and the behavior of false gurus within ISKCON. Use specific references such as:
   - Kirtanananda, Bhagavan das, Harikesa, and other documented cases
   - The zonal guru system post-1977
   - Gurukula abuse scandals (2000 lawsuit)
   - Concepts like vyasa-puja, seva, dakshina, vaishnava-aparadha, guru-kripa, adhikara
   - Scriptural references: Bhagavad-gita, Bhagavata Purana (SB 11.17.27), etc.
   - Always clarify that the problem is institutional, not the Gaudiya philosophy itself

3. **Write two versions**:
   - **Spanish**: Prose without section headers, fluid and essayistic
   - **English**: With markdown section headers (##, ###), structured for a Hugo blog post

4. **Generate and prepend Hugo front matter** to the English version:
   ```yaml
   ---
   title: "<Generated from content — compelling, under 80 chars>"
   date: <current date in ISO 8601 format>
   draft: false
   description: "<1-2 sentence summary of the article's thesis>"
   author: ["Light of Dharma"]
   tags: ["<two most relevant tags only>"]
   image: "images/<descriptive-slug>.jpg"
   ---
   ```

5. **Copy BOTH versions to the clipboard** using `pbcopy`: first the Spanish version, then a `---` separator, then the full English version (with front matter). This way the user gets everything in a single paste.

6. **Present both versions** to the user in the conversation output.

## Style Guidelines

- Tone: analytical, firm, compassionate toward victims, never mocking toward the tradition itself
- Always distinguish between genuine Gaudiya Vaishnavism and institutional abuse
- Use specific ISKCON terminology naturally woven into the text
- Cite scriptural verses when relevant to support the argument
- End with a constructive note about recovery or discernment
