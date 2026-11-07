# Fragment / TON Username NFT Auction Drain — Victim Report

> **To:** [@p05h](https://medium.com/@p05h) · [X](https://twitter.com/p05h)  
> **Re:** [*"Sophisticated Telegram-Based Scam Designed to Fool Fragment Users"*](https://medium.com/@p05h/sophisticated-telegram-based-scam-designed-to-fool-fragment-users-7d06334db111)

Hey p05h,

I read your article after getting hit by a scam targeting Fragment username NFT sellers. Total loss was **~41 TON/GRAM** — not life-changing money, but the attack was polished enough that I want to put everything on record. You've already documented the core mechanism; this is a real-world case study with full on-chain traces, the bot payload decoded, the phishing domain WHOIS, and the full exported Telegram chat.

I'm not asking you to solve anything. Just — **this is what happened to me**, end to end. Use it however you want for your research or write-ups.

---

## Table of Contents

1. [Quick Summary](#1-quick-summary)
2. [Victim & Asset Info](#2-victim--asset-info)
3. [How the Social Engineering Worked](#3-how-the-social-engineering-worked)
4. [The Malicious Mini App — Technical Breakdown](#4-the-malicious-mini-app--technical-breakdown)
5. [On-Chain Evidence](#5-on-chain-evidence)
6. [Phishing Domain Infrastructure (WHOIS)](#6-phishing-domain-infrastructure-whois)
7. [Full Conversation Log](#7-full-conversation-log)
8. [What I Still Don't Understand](#8-what-i-still-dont-understand)
9. [Closing Notes](#9-closing-notes)

---

## 1. Quick Summary

| Field | Value |
|---|---|
| **Attack type** | Forced auction drain via malicious Telegram Mini App |
| **Target** | Telegram Username NFT `@bitcoinsort` |
| **Loss** | ~41 GRAM/TON |
| **Attacker handle** | `@urs82vtsge` (display name: *Michael Moore*) |
| **Malicious bot** | `@AuctionsGramBot` |
| **Phishing domain** | `friendssender.com` |
| **Date** | November 5–6, 2026 |

The key difference from a typical phishing job: **no wallet was compromised, no seed phrase was leaked, no suspicious app was downloaded.** Everything happened through what looked like a legitimate Fragment interaction inside the Telegram Mini App sandbox. The on-chain funds went to the attacker's wallet when I won *my own auction* — which should have returned the funds to me as the winner/seller.

---

## 2. Victim & Asset Info

- **Username NFT:** `@bitcoinsort`
- **NFT Smart Contract:** `EQAS4jiOrK8Kc8-xTVO-wdZkQbzIsK1b7rQRYRdF__zYvbx_`
- **Victim wallet (now decommissioned):** `UQBpHv78E9L2Xi_xU78-V0uyZ0uditsguFv1cEQXeYF9H7Ji`
- **Original purchase price:** 15 GRAM

---

## 3. How the Social Engineering Worked

### Phase 1 — The warm approach (Nov 5)

The attacker ("Michael Moore", `@urs82vtsge`) cold-messaged me saying he saw my username while browsing the platform and asked if he could make an offer in GRAM. It looked totally organic — no weird links, no urgency.

```
[10:29] Michael Moore: yo, i happened to see your page while browsing the platform
[10:59] Me: Hey, which page are you talking about?
[11:24] Michael Moore: Can I make an offer for @bitcoinsort in gram?
[11:31] Me: Sure, what is your offer?
```

### Phase 2 — The highball offer (Nov 6, early morning)

He came back the next morning — 6:58 AM my time — with:

```
[06:58] Michael Moore: I can offer 280 TON for @bitcoinsort
[09:25] Michael Moore: Does that sound reasonable?
```

280 TON for a handle I bought for 15 GRAM. That's a 18x return. I was interested.

```
[09:38] Me: Great! I can list it on Fragment for you now. Standard Fragment transactions
            have a 5% fee. Would you be open to ~295 TON so I can clear the 280 net?
[09:43] Michael Moore: The offer is ready in Fragment, accept it when you are ready
```

Notice he didn't respond to my counter-offer. He just said *"the offer is ready."* I didn't know what offer he was talking about — nothing showed up on `fragment.com/username/bitcoinsort` on my end.

### Phase 3 — Confusion and the Mini App injection

I listed it properly on Fragment and sent him the direct link. He kept ignoring the link and repeating:

```
[10:56] Michael Moore: You need to click the blue button and then connect your wallet
```

That's when he eventually sent the malicious payload (after I ran out of funds from the first auction round, more on that below):

```
[12:55] Michael Moore: https://t.me/miniapp/fragment/username/bitcoinsort
[12:55] Michael Moore: now I specifically paid 300 TON to make it more expensive, you know?
```

> **Important:** In Telegram, that text displayed as a plain-looking URL. It did NOT render as a hyperlink in his chat bubble, which made it look like a raw informational string rather than a clickable link. I copied it into another chat to open it — and that's where it became a hyperlink and I clicked it.

Inside the Mini App, everything visually appeared to be `fragment.com`. The URL bar showed Fragment. No alarm bells.

I clicked "Accept Offer." I connected Tonkeeper. I approved what appeared to be a minimal gas fee. And my handle was immediately put up for public auction on Fragment — without me knowingly listing it.

### Phase 4 — The pressure cooker (the fake bidding war)

As soon as the auction started, bids appeared *instantly.* The attacker then pivoted to psychological pressure:

```
[11:21] Michael Moore: it looks like you accidentally started the auction [screenshot]
[11:25] Michael Moore: You can't cancel the auction once someone's already bid.
                        Main thing is just buy it from yourself or you'll lose the NFT.
                        The money you bid basically comes straight back to your wallet anyway.
[11:26] Michael Moore: Since your auction has started, place a bid of 111 or 222 TON.
                        This will push the price higher. After the auction ends, I'll pay you 300 TON.
[11:27] Michael Moore: Just place a big bet so no one beats you, you'll get your money back exactly.
```

This is a classic pressure + false reassurance combo. He told me:

1. You accidentally started the auction (created guilt + urgency)
2. Bidding on your own auction returns the money (false)
3. I'll make it worth your while afterwards (future-promise bait)

I didn't have 111–222 TON. I had a small amount and bid ~42 GRAM trying to hold the username. I ran out of funds.

### Phase 5 — The "good faith" 2 TON transfer (bait to keep me bidding)

```
[11:53] Michael Moore: Let me send you 2 ton — for outbid. Ok?
[11:55] Michael Moore: Place a 42 ton bid now. I sent [the 2 TON].
```

He literally sent me 2 TON to keep me in the auction. Why? Because every bid I placed went straight into the drainer wallet. He had financial incentive to keep me bidding.

> **Sending me 2 TON to get 42 back is a +2000% ROI on his investment in my trust.**

### Phase 6 — The second round (same trick)

After I ran out of funds again, he sent the malicious Mini App link a second time, claiming he had raised the offer to 300 TON. Same flow, second drain.

```
[13:01] Michael Moore: [screenshot of auction] Fuck
[13:01] Michael Moore: Its all because TON is becoming GRAM the network is overloaded right now,
                        and this kind of thing happens sometimes...
[13:02] Michael Moore: You cannot cancel the auction if someone has already placed a bid.
                        Important thing is to buy it from yourself.
```

The "network overload / TON to GRAM migration" excuse is a scripted line. It's designed to explain away any anomaly without raising suspicion.

---

## 4. The Malicious Mini App — Technical Breakdown

### The payload

The link shown in chat:
```
https://t.me/miniapp/fragment/username/bitcoinsort
```

The actual hyperlink target (visible in the exported HTML of the chat):
```
https://t.me/AuctionsGramBot/offer?startapp=WzAsMzAwLCJiaXRjb2luc29ydCIsIk5GVCIsNywxNzkzOTg3NjM4Mjc2LCI1ZjEzOTgwZDhkNDFjYjIzIl0=
```

The display text is a fake `fragment` path. The actual link routes to `@AuctionsGramBot` with a base64 `startapp` parameter.

Decoding the base64 payload:
```
WzAsMzAwLCJiaXRjb2luc29ydCIsIk5GVCIsNywxNzkzOTg3NjM4Mjc2LCI1ZjEzOTgwZDhkNDFjYjIzIl0=
```
```json
[0, 300, "bitcoinsort", "NFT", 7, 1793987638276, "5f13980d8d41cb23"]
```

This tells the malicious bot exactly which NFT to drain, the amount, and a session/tracking token. The bot was **pre-loaded with the target asset** before the attacker even sent the link.

### The intermediate domain (friendssender.com)

When I tried to inspect the Mini App via Telegram Web and Firefox DevTools, I caught this redirect chain:

**Step 1 — Initial request (302 redirect):**
```http
GET https://friendssender.com/?tgWebAppStartParam=WzAsMzAwLCJiaXRjb2luc29ydCIs...
    #tgWebAppData=user={"id":7119402520,"username":"xelovryx",...}

HTTP/2 302 Found  [627ms]
→ Location: https://fragment.com/username/bitcoinsort#tgWebAppData=...
```

**Step 2 — Frame injection attempt (blocked):**
```
GET https://fragment.com/username/bitcoinsort#tgWebAppData=user={...}
NS_ERROR_XFO_VIOLATION
```

Fragment sets `X-Frame-Options: sameorigin`, which blocked the iframe embed. But by then, the Telegram session data (`id`, `username`, `auth_date`, `hash`, `signature`) had already been forwarded to `friendssender.com`.

> **If you visit `friendssender.com` directly in a browser, it instantly 302-redirects to `fragment.com`.** That's the cover — it looks like a Fragment mirror/helper, not a phishing endpoint.

### What the Mini App actually does

Based on what I observed (and consistent with your article):

1. It renders a spoofed Fragment UI inside the Telegram Mini App sandbox.
2. The "Accept Offer" button doesn't execute a standard Fragment sale — it calls a smart contract function that **puts the NFT into a new auction with the attacker's wallet as the designated recipient of funds**.
3. The victim sees `fragment.com` in the Mini App header. The wallet connect popup shows a minimal gas fee. Everything looks normal.
4. After signing: the NFT is auctioned. Bids from the victim flow to the attacker's wallet — not back to the victim as the auction "winner."

---

## 5. On-Chain Evidence

### Transaction 1 — 41 GRAM drain (first auction round)

| Field | Value |
|---|---|
| **Tx Hash** | `6ff0a7caccc8bbb565b4edf57f1af8d9bb8eb303021b18e228607714eae237c7` |
| **Explorer** | [tonviewer.com →](https://tonviewer.com/transaction/6ff0a7caccc8bbb565b4edf57f1af8d9bb8eb303021b18e228607714eae237c7) |
| **Description** | I won the auction. The NFT came back to me. The 41 GRAM bid went to the attacker, not returned to my wallet as the winning bidder/seller. |
| **Recipient (drainer wallet)** | `UQDdNeOvNs1cJbnZcYi1Bsc8g1DDJruLh3ExuDOVoc1N6Rm2` |

### Transaction 2 — Secondary wallet (second auction round, ~6 GRAM)

| Field | Value |
|---|---|
| **Wallet** | `UQDCU728sEINKVci8Fmnpy_Pw4rP_PPjhtRC8jIK8wKA2Rt4` |
| **Explorer** | [gram.org/address →](https://gram.org/address/EQDCU728sEINKVci8Fmnpy_Pw4rP_PPjhtRC8jIK8wKA2Ua9) |
| **Description** | Used in the second auction round. Different wallet — could indicate rotating drainer addresses or a separate bot operator. |

### Transaction 3 — The 2 TON "bait" sent to me

| Field | Value |
|---|---|
| **Tx Hash** | `0cb262d13ec164c3783d35fa9e0963e69d4784e142ee7a06cfb51dfe91d2a883` |
| **Explorer** | [tonviewer.com →](https://tonviewer.com/transaction/0cb262d13ec164c3783d35fa9e0963e69d4784e142ee7a06cfb51dfe91d2a883) |
| **Description** | The 2 TON the attacker sent me to keep me bidding. Proof this is a coordinated operation — not opportunistic. |
| **Sender (attacker funding wallet)** | `UQAC73o3h81Yoo_aGoIGPcqWgX_r6OensBnDAkPUYNMwo-hz` |

### Auction behavior worth noting

Both times the auction started, **an instant bid appeared within seconds.** Either the attacker/team has bots watching Fragment for new auctions triggered by their own Mini App, or the auction participants are entirely controlled by them. The bidding war was synthetic — designed to create urgency and push the victim to keep spending to outbid phantom competitors.

---

## 6. Phishing Domain Infrastructure (WHOIS)

Domain: **`friendssender.com`**

```
Registrar:        TUCOWS.COM CO. / Tucows Domains Inc.
Registrar IANA ID: 69
Created:          2026-10-10T20:34:24Z
Expires:          2027-10-10T20:34:24Z
Status:           clientTransferProhibited, clientUpdateProhibited

Nameservers:
  - jermaine.ns.cloudflare.com
  - katelyn.ns.cloudflare.com

IP:               104.21.24.210 (Cloudflare proxy)
ASN:              AS13335 — CLOUDFLARENET, US

Registrant:       REDACTED FOR PRIVACY
Registrant Country: KN (Saint Kitts and Nevis)
Registrant Email: https://tieredaccess.com/contact/3a74e23b-eea5-4425-84a2-7623b001e2c1
```

> **27 days old at the time of the attack.** Domain was registered October 10, 2026 — purpose-built for this campaign. Saint Kitts and Nevis registration + Cloudflare proxy + Tucows registrar is a pattern worth flagging in threat intel databases.

---

## 7. Full Conversation Log

The complete exported Telegram chat (HTML format with screenshots) is included in this repository under [`telegram_chat_export/messages.html`](./telegram_chat_export/messages.html).

Open it in any browser — no server needed. It includes:
- All messages with exact timestamps (GMT-05:00)
- 5 screenshots shared during the conversation
- The raw hyperlink source for the malicious Mini App (the display text vs. the actual `href` are different — visible in the HTML source)

**Key message timestamps for quick reference:**

| Time (Nov 6) | Event |
|---|---|
| `09:43` | Attacker: *"The offer is ready in Fragment, accept it when you are ready"* |
| `11:21` | Attacker sends screenshot + *"it looks like you accidentally started the auction"* |
| `11:25` | Attacker: *"buy it from yourself, the money comes straight back to your wallet"* (lie) |
| `11:53` | Attacker: *"Let me send you 2 TON for outbid"* — the bait transfer |
| `11:55` | Attacker: *"Place a 42 TON bid now. I sent."* |
| `12:55` | Attacker sends malicious Mini App link (second round, 300 TON offer) |
| `13:01` | Attacker: *"Its all because TON is becoming GRAM, the network is overloaded"* |
| `13:04` | Attacker: *"They will refund it in 24 h"* (they didn't) |

---

## 8. What I Still Don't Understand

A few technical questions I couldn't fully reverse-engineer on my own. If you have insight on any of these, I'd genuinely appreciate it:

**Q1: How did accepting the Mini App offer put my NFT into auction?**  
When I "accepted the offer" through `@AuctionsGramBot`, the wallet prompt looked like a standard Fragment gas fee. What contract call was actually being signed? Was it a `transfer` or `auction_start` function on the NFT contract with a custom beneficiary address baked in?

**Q2: Why did my wallet stay connected to fragment.com the whole time?**  
Even after multiple page reloads, my Tonkeeper stayed connected and appeared to show my wallet. If this was a session hijack via the forwarded `tgWebAppData`, how was the state maintained across reloads? Or did the malicious contract just reference my wallet as the NFT owner while routing payment elsewhere?

**Q3: Were the instant auction bids from bots or coordinated wallets?**  
Both auction rounds had bids within seconds of the auction starting. The bidder wallets may be different from the two drainer wallets listed above. Is this a known bot cluster associated with this type of drain?

**Q4: Is `@AuctionsGramBot` still active?**  
The bot was live as of November 6, 2026. If it's still running, the encoded `startapp` payloads could be a way to map their active targets.

---

## 9. Closing Notes

What made this hard to catch — even for someone who was actively paying attention:

- ✅ The domain in the Mini App UI showed `fragment.com` — not a lookalike
- ✅ The wallet connect popup looked standard (small gas fee, familiar UI)
- ✅ The attacker's social engineering was patient — no urgency at first contact
- ✅ He sent me actual TON to keep the trust alive
- ✅ His "technical explanations" (network overload, auction mechanics) were plausible enough in the moment

The only real anomaly I caught in real time was that the Mini App link didn't render as a hyperlink in the chat — which is why I copy-pasted it into another chat to open it. That should have been a bigger red flag. If Telegram renders a t.me link as plain text in certain contexts, something is off.

Feel free to use everything in this repo — wallets, payloads, domain data, chat logs — for your research or threat intelligence work. No attribution needed.

Stay sharp.

— *𝔈𝔩 ℜ𝔦𝔠𝔥* (`@xelovryx`)

---

*Repository also contains the original exported Telegram chat in HTML format (`telegram_chat_export/`) with all screenshots intact.*
