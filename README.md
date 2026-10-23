# ste100-pt

A Claude Code plugin that makes Claude reply in **Brazilian Portuguese (PT-BR)** following the writing rules of **ASD-STE100 (Simplified Technical English)**, adapted to Portuguese.

Replies become short, direct and unambiguous: one instruction per sentence, numbered steps, active voice, consistent terms and warnings before the step they apply to.

## Rules applied

1. Short sentences: instructions up to 20 words, descriptions up to 25 words.
2. One instruction per sentence, in the imperative.
3. Procedures as numbered steps, in execution order.
4. Active voice: say who does the action.
5. One term = one meaning. No synonyms for the same thing.
6. Complete sentences (no fragments).
7. Paragraphs of up to 6 sentences, one topic each.
8. Warnings (`ATENÇÃO:` / `CUIDADO:`) before the step they refer to.
9. No metaphors, slang, irony, pleasantries, filler or hedging.
10. Numbers, dates and units always explicit.

Code, commands, commit messages and project artifacts keep the project's own rules.

## How it works

Two hooks, no runtime dependencies (they only `cat` a static JSON file, so they work locally and in cloud sessions):

| Hook | What it injects |
|---|---|
| `SessionStart` | The full ruleset, once per session |
| `UserPromptSubmit` | A short reminder on every message, so the style does not drift in long sessions |

## Install

In Claude Code:

```
/plugin marketplace add mustdigital-ai/ste100-pt
/plugin install ste100-pt@mustdigital
```

Restart Claude Code (or open `/hooks`) to load the hooks.

### Cloud sessions (Claude Code on the web)

Commit this to the repository's `.claude/settings.json` so cloud sessions install the plugin automatically:

```json
{
  "extraKnownMarketplaces": {
    "mustdigital": {
      "source": { "source": "github", "repo": "mustdigital-ai/ste100-pt" }
    }
  },
  "enabledPlugins": {
    "ste100-pt@mustdigital": true
  }
}
```

## Disable or remove

```
/plugin disable ste100-pt@mustdigital
/plugin uninstall ste100-pt@mustdigital
```

Do not run it together with other style plugins (for example `caveman`): the instructions conflict.

## License

MIT © Must Digital
