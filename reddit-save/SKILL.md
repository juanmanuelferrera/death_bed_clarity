---
name: reddit-save
description: Fetch Reddit posts and save them to Kavya vault. Triggers on "reddit", "save from reddit", "dame lo de reddit", "reddit save", "fetch reddit".
user-invocable: true
---

# /reddit-save — Fetch and save Reddit content to Kavya

Fully automatic: fetch all posts, save all posts, no questions asked.

## Vault path

Target folder: `/Users/jaganat/Kavya/Reddit/`

## Usage

- `/reddit-save r/stoicism` — fetch and save all hot posts from r/stoicism
- `/reddit-save r/stoicism r/philosophy r/krishna` — fetch and save from multiple subreddits
- `/reddit-save r/stoicism top week` — fetch and save top posts from the past week
- `/reddit-save` — use default subreddits (see below)

## Default subreddits

When invoked with no arguments, automatically use:
- r/stoicism, r/philosophy, r/krishna, r/programming

## Workflow — FULLY AUTOMATIC, NO QUESTIONS

1. **Fetch** hot posts from all specified subreddits in parallel using Reddit MCP tools
2. **Skip** pinned/meta posts (weekly threads, rules posts, stickied mod posts)
3. **Fetch full content** for ALL remaining posts in parallel (use `get_post_content` with `comment_limit: 5`)
4. **Save ALL posts** as markdown files — no asking, no listing, no confirmation
5. **Report** a summary when done: "Saved N posts from r/sub1, r/sub2..."

**NEVER ask the user which posts to save. Save ALL of them automatically.**

## Filename format

`subreddit-slugified-title-8charhex.md`

- Slugify: lowercase, replace non-alphanumeric with `-`, collapse multiple `-`, trim, max 50 chars for the title portion
- Append `-` + 8 random hex chars
- Example: `stoicism-how-marcus-aurelius-dealt-with-anger-4f2a9c01.md`

## Content format

```markdown
# Post Title

**r/subredditname** | Score: 1234 | Comments: 56 | u/author
**Date:** YYYY-MM-DD
**Link:** https://www.reddit.com/r/subredditname/comments/postid/...

---

Post body content here...

---

## Top Comments

> **u/commenter1** (Score: 234)
> Comment text here...

> **u/commenter2** (Score: 123)
> Comment text here...
```

**IMPORTANT:** Always include the `**Link:**` line with the full Reddit URL for the post.

## Rules

- **NO user interaction** — fetch all, save all, report summary
- Fetch 10 posts per subreddit by default (adjustable with `limit N`)
- Include top 5 comments per saved post (skip AutoModerator and bot comments)
- If a post is just a link with no text body, include the link URL prominently in the body
- Keep the original language of the post (don't translate)
- Use parallel fetches and parallel writes for speed
- Skip pinned/stickied posts automatically
