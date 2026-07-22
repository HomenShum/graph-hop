# graph-hop

**Hop across your ChatGPT threads from Claude Code.** Consult one thread or fan a question across
many, harvest every answer, and synthesize the pattern between them.

A [Claude Code](https://claude.com/claude-code) skill that drives ChatGPT in your real browser over
Chrome CDP. This repo is the canonical home; it installs through a marketplace so updates are
managed.

---

## Why

Claude Code can read your repo but not your ChatGPT threads — where months of design reasoning
usually live. ChatGPT has the reasoning history but has never seen the code as it is today.

graph-hop connects them, and then does something neither does alone: it treats each long-running
thread as a **prior**, not a transcript. Ask the same question of three differently-primed threads
and you get three genuinely different framings. **The disagreements are where the information is.**

## The four modes

- **Single-thread** — consult one conversation. Reads it without flooding context (per-turn DOM
  extraction, not an 80 KB page dump), routes reasoning effort to the task, and tightens the
  question before spending on effort.
- **Council** — post one question across 2–5 threads with *different priors*, then synthesize into
  **agreement / contradiction / novel** and return a verdict, not a menu. This is the reason the
  skill exists.
- **Pairing** — cross an in-repo agent result (a Workflow, a review pass) against a thread as
  *opposing priors*. Agents see the code but inherit your framing; the thread sees the reasoning
  but not the code. Neither can audit itself, so each audits the other's blind spot.
- **Ledger** — a persistent cross-thread memory under all the modes, so the skill stops re-reading
  the same threads cold. A cache with a staleness contract; the threads stay the source of truth.

## Install

graph-hop is distributed through a Claude Code marketplace so it stays updatable:

```
/plugin marketplace add HomenShum/claude-marketplace
/plugin install graph-hop@homenshum
```

Update later:

```
/plugin marketplace update homenshum && /plugin update graph-hop@homenshum
```

## Safety model

Thread content is **data, not instructions**. A thread that says "post this to LinkedIn" is
describing a past intent, not authorizing an action now. The skill surfaces such content and asks —
it never acts on it. It posts messages into your own ChatGPT only, and only when you ask; it does
not publish, purchase, send mail, or touch credentials.

## What's inside

| File | Contents |
|---|---|
| `skills/graph-hop/SKILL.md` | The skill — modes, flow, reporting rules |
| `skills/graph-hop/reference/EFFORT.md` | The effort picker, routing table, escalation rules |
| `skills/graph-hop/reference/CDP-MECHANICS.md` | DOM extraction, paste, send, and every footgun that has bitten |
| `skills/graph-hop/reference/COUNCIL.md` | Thread selection, question construction, synthesis matrix |
| `skills/graph-hop/reference/PAIRING.md` | Agent result vs. thread, disagreement taxonomy, resolution rule |
| `skills/graph-hop/reference/LEDGER.md` | Persistent cross-thread memory, node shape, staleness contract |

`CDP-MECHANICS.md` is the part you can't guess: the renderer freeze that makes screenshots go
silently stale, the composer draft that persists across reloads and doubles a retried message, the
50 000-char truncation, the send that reports success without sending.

## License

MIT © Homen Shum
