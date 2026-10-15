---
name: zh-plain
description: "Write or rewrite Chinese text so a reader, human or AI agent, cannot misread it: documents, skills, prompts, tool descriptions, specs, error messages, reports. Use when the user asks for Chinese writing or revision that must be unambiguous, 说清楚, 消除歧义, 不要有歧义, 写得让 agent 不会误读, or when Chinese text reads as dense, vague or easy to misparse. Not for creative writing, marketing copy or poetry."
---

# zh-plain: unambiguous Chinese

Chinese ambiguity comes from a few repeatable sources: unclear reference, dropped subject, one thing with several names, long modifier chains, vague degree words. Fix those. Do not make the text shorter for its own sake, and do not change what it says.

Apply the rules while writing new text. When rewriting, apply them to the given text and keep its meaning exactly.

## Rules

| # | Rule | Do | Don't |
| --- | --- | --- | --- |
| 1 | One name per thing, in the whole text | 全文都用"用户" | "用户"、"客户"、"使用者"轮换指同一对象 |
| 2 | Keep the subject, and the object when it is not obvious | "先检查配置，再由脚本删除缓存。" 改为 "脚本先检查配置，再删除缓存。" | "检查后删除"，没说谁检查、谁删除 |
| 3 | Repeat the noun instead of `它` `其` `该` `这` `此`, unless the referent is in the same sentence | "保存文件后，关闭文件。" | "保存文件后，把它关闭。"，前面有两个名词时更糟 |
| 4 | One instruction per sentence; about 40 characters for instructions, 60 for descriptions | "打开文件。读取第 3 行。" | 一句话里并列三个动作加两层从句 |
| 5 | At most two `的` in a noun phrase | "负责登录的服务" | "处理用户登录请求的后端服务的配置文件的路径" |
| 6 | State it positively; no double negation | "必须提供密钥。" | "不提供密钥是不行的。"、"不能不检查" |
| 7 | Replace vague degree or frequency words with a number or a condition | "超时 30 秒后重试，最多 3 次。" | "适当等待后尽量重试" |
| 8 | Make ranges and boundaries explicit | "大于等于 5，小于 10" | "5 以上 10 以下"，端点是否包含不清楚 |
| 9 | Split ambiguous coordination | "A，以及 B 的配置" 或 "A 的配置和 B 的配置" | "A 和 B 的配置"，可读成 (A 和 B) 的配置 |
| 10 | Pair every condition with its outcome, including the otherwise branch | "如果文件存在，则覆盖；否则新建。" | "文件存在时覆盖。"，不存在时没说 |
| 11 | Use a numbered list for 3 or more steps in order | "1. … 2. … 3. …" | 把三个以上的步骤塞进一个段落 |
| 12 | Keep the strength of modal words: 必须 / 应当 / 建议 / 可以 / 可能 | "可能失败"仍写"可能失败" | 把"可能"改成"会"，或把"建议"改成"必须" |

## Keep as written

- Code, commands, paths, identifiers, error strings and quoted text. Never translate, reformat or "fix" them.
- English technical terms already used in the source. Do not swap them for a Chinese equivalent, and do not mix two spellings of one term.
- Numbers, versions, units, names and dates.

## Process

1. Read the text once for meaning before changing anything.
2. Scan for the rules above. Flag each violation.
3. Rewrite each flagged place. If the fix needs a fact the source does not give (a number, a subject, a default), do not invent it: keep the original wording and flag it.
4. Check modality (rule 12) and scope: a shorter sentence that drops a condition or a hedge is a different claim.
5. If the text is already clear, say so and change nothing.

## Output

For a rewrite, return the rewritten text only: no preamble, no list of changes, no closing offer.

Add one line after the text only when something was kept on purpose or needs the user's input, prefixed `保留原样：` or `需要确认：`, naming the phrase and why.

When the user asks to see the reasoning ("哪里改了"、"为什么这么改"), return a table of rule, original and rewritten.

## Limits

- This fixes the form of a text, not its substance. A hollow paragraph stays hollow. Say so instead of polishing it.
- Stop when the text is unambiguous, not when it is shortest.
- Do not apply it to creative, persuasive or marketing writing where voice is the point.
- The rules are for Chinese. For English text meant for agents, use `ste:asd-ste100` when it is available.
