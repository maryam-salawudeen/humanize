# humanize

A prompt that makes any AI assistant write, code and make images like a careful person. Use it in ChatGPT, Gemini, Claude, Copilot or any assistant that takes custom instructions, either to clean up something AI made or to stop the assistant making it that way in the first place.

AI output gives itself away with the same habits over and over.

- **Writing:** "it's not just X, it's Y", a one-line closer after every paragraph, lists of three, dashes everywhere, "delve" and "pivotal", bold labels on every bullet, and "I hope this helps!" at the end.
- **Code:** a comment on every line, names like `data` and `result`, abstractions nobody needed, try/catch around everything, placeholder functions, invented APIs, and a paragraph of notes after the code.
- **Images:** plastic skin, perfect symmetry, glossy cinematic light, extra fingers, signs with gibberish text, and shadows that disagree with the light.

This prompt lists those habits, gathered from about 40 sources (see [SOURCES.md](SOURCES.md)), and says what to do instead. It tells the assistant to keep every fact and behaviour and add none, and to hand back humanized code with no extra notes.

It isn't a tool for fooling AI detectors. The aim is work you'd be glad to put your name to.

## Two versions

- [humanize.md](humanize.md) is the full prompt (about 12,000 characters): writing patterns, code rules, image rules, how to rewrite, how to match your voice and what to leave alone.
- [humanize-short.md](humanize-short.md) is a short version (about 1,200 characters) that fits ChatGPT's custom instructions box, so it applies to every chat.

## Install it globally

Set it up once and it applies to every chat or project in that assistant.

### Chat assistants

| Assistant | Where it goes | Version |
|---|---|---|
| ChatGPT | Settings → Personalization → Custom instructions | short |
| Gemini | Settings → Saved info | short |
| Claude (web, desktop, mobile) | Settings → Profile → personal preferences | short or full |
| Any other assistant | Its custom instructions, profile or memory setting, or paste the full version as your first message | short or full |

If you'd rather keep it separate from your everyday chats, make it its own assistant:

- **Custom GPT:** paste the short version into Instructions, upload `humanize.md` under Knowledge, and add "Follow humanize.md for every reply." The full prompt is longer than the 8,000-character Instructions box.
- **Gemini Gem or Claude project:** paste the full version as the instructions. If it doesn't fit, upload `humanize.md` as a file and tell it to follow the file.

### Coding assistants

Each of these reads a global instructions file on your computer. The commands add the full prompt to it (`>>` adds to the end, so anything already in the file stays).

**Claude Code** (as a `/humanize` skill):

```bash
mkdir -p ~/.claude/skills/humanize && { printf -- '---\nname: humanize\ndescription: Humanize writing, code and images. Use when asked to humanize or rewrite something, and when writing prose, code or image prompts.\n---\n\n'; curl -sL https://raw.githubusercontent.com/maryam-salawudeen/humanize/main/humanize.md; } > ~/.claude/skills/humanize/SKILL.md
```

**OpenAI Codex CLI:**

```bash
mkdir -p ~/.codex && curl -sL https://raw.githubusercontent.com/maryam-salawudeen/humanize/main/humanize.md >> ~/.codex/AGENTS.md
```

**Gemini CLI:**

```bash
mkdir -p ~/.gemini && curl -sL https://raw.githubusercontent.com/maryam-salawudeen/humanize/main/humanize.md >> ~/.gemini/GEMINI.md
```

**Cursor:** Settings → Rules → User Rules, then paste the full version.

**GitHub Copilot in VS Code:** open the Command Palette, run "Chat: New Instructions File", choose your user folder so it applies to every workspace, and paste the full version.

**Windsurf:** Settings → Customizations → Rules → Global, then paste the version that fits (global rules have a size limit, so use the short version if the full one is cut off).

To update later, run the same command again after deleting the old copy, or paste the new version over the old one.

## How to use it

Ask:

```
Humanize this: <paste your draft>
```

```
Humanize this code: <paste your code>
```

```
Does this image look AI-made? <attach the image>
```

For text, it sends back the rewrite and a short list of things to double-check. For code, it sends back only the code, with the same behaviour. If you paste a sample of your own writing first, it matches your voice, including your punctuation.

## Examples

Text before:

> It's not just a tool — it's a game-changer. Our platform seamlessly brings your team's tasks, files and messages together in one place, empowering teams to unlock their full potential and fostering collaboration, innovation, and growth. The future looks bright.

Text after:

> The platform puts a team's tasks, files and messages in one place.

The rewrite keeps the one fact the draft had and drops the rest, because the rest wasn't saying anything.

Code before:

```ts
// Function to check the URL
function checkUrl(u: any) {
  // check if url starts with https or http
  if (u.startsWith("https://") || u.startsWith("http://")) {
    return true; // return true
  } else {
    return false; // return false
  }
}
```

Code after:

```ts
// This is a basic protocol check, not complete SSRF protection.
// The server must also validate resolved IPs and redirects.
function hasAllowedProtocol(url: string): boolean {
  return url.startsWith("https://") || url.startsWith("http://");
}
```

Image prompt before:

> A beautiful woman, flawless skin, perfect face, ultra-detailed, cinematic lighting, 8k

Image prompt after:

> A woman in her thirties reading at a kitchen table by a window, overcast afternoon light, natural skin texture with visible pores, a few flyaway hairs, slightly creased linen shirt, 50mm lens, mild grain

## Credits

The writing rules build on [humanizer](https://github.com/blader/humanizer) by Siqi Chen and Wikipedia's [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing). The code rules build on my own human-readable code and commenting standard, and the image rules on Northwestern University's guide to spotting AI-generated images. Every other source is listed in [SOURCES.md](SOURCES.md).

## Contributing

Spotted an AI habit that isn't here, or a rule that does more harm than good? Open an issue or a pull request. Add the source you got it from to SOURCES.md, and keep the short version under 1,500 characters so it still fits ChatGPT's custom instructions.

## Licence

MIT. See [LICENSE](LICENSE).
