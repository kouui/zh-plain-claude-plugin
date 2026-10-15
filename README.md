# zh-plain-claude-plugin

Claude Code plugin for writing unambiguous Chinese: documents, skills, prompts, tool descriptions, specs, error messages.

One style per plugin, so each can be enabled or disabled on its own in `enabledPlugins`.

## Skills

| Skill | Purpose |
| --- | --- |
| `zh-plain` | 12 rules that remove the usual sources of Chinese ambiguity: unclear reference, dropped subject, several names for one thing, long modifier chains, vague degree words, unclear boundaries, lost modal strength |

Call it as `/zh-plain:zh-plain`, or let Claude load it when you ask for Chinese writing that must not be misread.

## Install

This repo is a single plugin. It is listed in the [magic-claude-code-plugin](https://github.com/kouui/magic-claude-code-plugin) marketplace:

```bash
claude plugin marketplace add kouui/magic-claude-code-plugin
claude plugin install zh-plain@magic-claude-code-plugin -s user
```

To try a local checkout without installing: `claude --plugin-dir <this folder>`.

## Layout

```text
.claude-plugin/plugin.json
skills/zh-plain/SKILL.md
```

## TODO

- A check script, like `ste-lint.py` in the STE plugin (`uv` single-file script). Only a few Chinese rules can be checked mechanically: sentence length, the number of `的` in a noun phrase, pronouns (`它` `其` `该` `这` `此`) with no clear referent. It may help less than the STE linter, so decide after using the skill for a while.
- Run the rules on real documents and skills, then drop or reword the rules that do not earn their place.

## Related

For English text meant for agents, see [ste-claude-plugin](https://github.com/kouui/ste-claude-plugin) (ASD-STE100).
