# AskMyTele

**Read your own Telegram channels from Claude or ChatGPT, over OAuth, without
handing that assistant the keys to your account.**

Live at **<https://askmytele.com>** — paste `https://askmytele.com/mcp` into
Claude or ChatGPT as a custom connector, scan the QR with your phone, done.

Try it without connecting anything: **<https://askmytele.com/demo>**.

## What it can do

- `me`, `list_channels`, `read_channel`, `search_channels` — all read-only.
  `search_channels` runs one query across up to five of your own channels and
  returns hits (or "not found") per channel, so "where was this mentioned" is
  answerable without dragging every message through the model.
- `notify` — the one write tool. It sends a Telegram message **to the account
  that installed the connector, and to nobody else.** There is no recipient
  argument of any kind — the destination is derived from your session, not
  supplied by the caller, so no prompt injection can name a third party. Logging
  in also subscribes you to the bot that delivers this, once, as you, and the
  login screen says so before it happens.
- `feedback_to_developer` — sends the developer a short note in your own
  words. Same shape as `notify`: no recipient argument, fixed destination.

## What it deliberately cannot do

The product's central claim is a restraint claim, and it's meant to be
checked, not taken on faith:

- **No join, no leave, no invite. Ever.** Channel-joining and invite-import
  calls are not wrapped and will not be. An agent that can join arbitrary
  channels is a botnet node.
- **Nothing you do here is visible to anyone else**, except the two writes
  above — both fixed-destination, both consented to before they happen. No
  sending to a third party, no reacting, no posting, no editing, no deleting.
- **No marking read.** Reading a channel here never touches your unread state.
- **No discovery of anything you're not already in.** Username resolution and
  global search are not exposed to the caller — you can only read channels
  already in your own dialog list. There is no way to hand this assistant a
  channel you haven't joined and have it look inside.
- **Public surfaces only.** Public broadcast channels and public supergroups
  are readable; private channels, private groups, DMs and saved messages never
  appear in any response — filtered server-side, so a private channel is
  *absent*, not merely unlabeled.
- **You never name a peer directly.** Tools take a channel name; Telegram's
  internal peer reference is re-derived server-side from your own dialog list,
  never accepted as caller input.
- **Revocable without asking us.** The connection shows up in Telegram under
  Settings → Devices like any other linked session. Terminate it there and
  this stops working immediately — no ticket, no email.

## Source

The deployment repository isn't public yet — this is a docs-and-README mirror
published ahead of it so the claims above are checkable before that decision
is made. If that changes, this file is updated to point at it.

## License

[Unlicense](LICENSE) — public domain.
