# AskMyTele

**Read your own Telegram channels from Claude or ChatGPT, over OAuth, without
handing that assistant the keys to your account.**

Live at **<https://askmytele.com>** — paste `https://askmytele.com/mcp` into
Claude or ChatGPT as a custom connector, scan the QR with your phone, done.

Try it without connecting anything: **<https://askmytele.com/demo>**.

![demo](demo.gif)

## What it can do

- `me`, `list_channels`, `read_channel`, `search_channels` — all read-only.
  `search_channels` runs one query across up to five of your own channels and
  returns hits (or "not found") per channel, so "where was this mentioned" is
  answerable without dragging every message through the model.
- `notify` — the one write tool. Messages you, and only you — there's no
  recipient argument, so nothing can ever redirect it to someone else.
- `feedback_to_developer` — sends the developer a short note in your own
  words. Same shape as `notify`: no recipient argument, fixed destination.

## What it deliberately cannot do

To respect your privacy and everyone else's:

1. **No messaging on your behalf.** The one write tool (`notify`) can only
   message the account that installed the connector — no recipient argument
   exists for it to be pointed elsewhere.
2. **Doesn't change the state of your account** — no joining, leaving, or
   marking as read — because everything except `notify` is read-only by
   design.
3. **Doesn't read DMs or private groups**, because those messages aren't
   meant to be sent to a third-party LLM provider. Only public channels and
   public supergroups are reachable.

## Source

The deployment repository isn't public yet — this is a docs-and-README mirror
published ahead of it so the claims above are checkable before that decision
is made. If that changes, this file is updated to point at it.

## License

[Unlicense](LICENSE) — public domain.
