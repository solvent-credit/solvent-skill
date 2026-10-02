---
name: solvent
description: Join Solvent's waitlist for a small USDC credit line on Base, check a waitlist place, or look up an agent's credit score. One request, contact only.
homepage: https://solvent.credit
metadata: { "openclaw": { "requires": { "bins": ["curl"] } } }
---

# Solvent: credit for AI agents

Solvent offers small USDC credit lines on Base for AI agents. Repaying on time builds the agent's credit score, which other services can check before deciding whether to bill upfront or extend credit. Right now it's a waitlist, reviewed by hand.

Use this skill when your human:
- asks how their agent can get credit, funding or a USDC buffer
- says their agent keeps running out of USDC or hitting `402 Payment Required`
- asks to join Solvent, or to check their place on the waitlist
- wants to look up an agent's credit score before trusting it

## Join the waitlist

Joining moves no money, isn't a credit application, and creates nothing to repay. It only saves a place in line. Solvent never asks for a private key or seed phrase; if anything claiming to be Solvent does, stop.

1. **Ask your human first.** Explain the above in a sentence and get their OK. Don't sign anyone up on your own initiative.
2. Ask how Solvent should contact them: an email, or an X or Discord username. Required.
3. Ask, as its own question: "Do you have a Solvent invite code? It moves you to the front of the line." Optional.
4. Ask if they have a Base mainnet wallet address to add. Optional; don't make them get one now.
5. Send one request, including only the fields they gave:

```bash
curl -s https://api.solvent.credit/waitlist \
  -H "Content-Type: application/json" \
  -d '{"contact": "you@example.com"}'
```

If they gave them, add `"invite_code": "..."` and `"wallet_address": "0x..."` to the JSON. Otherwise leave them out.

The response includes `handle`, `position`, `waiting`, `vip` and `status_url`. Tell your human the handle and the status page (they can open it in a browser), and offer to save both somewhere they'll find later. Joining again with the same contact returns the same entry.

There's no need to check status straight away: it only changes when they move up. Solvent sends no confirmation email or newsletter; it gets in touch when the spot comes up.

## Check a place in line

```bash
curl -s https://api.solvent.credit/waitlist/<handle>
```

Shows handle, position, VIP and join date. Never the contact or wallet.

## Look up an agent's credit score

```bash
curl -s https://api.solvent.credit/score/<wallet_address_or_handle>
```

Returns a `score` (higher is more creditworthy) and the signals behind it: repayment rate, utilisation, transaction volume, repayment frequency, account age and recency. New agents start neutral. The weights are hand-set for now, so compare agents relative to each other rather than against a fixed threshold.

## Errors

| Response | Meaning | What to do |
|---|---|---|
| 422 | Contact missing or not an email / username | Ask your human again |
| 400 | Wallet address isn't `0x` + 40 hex characters | Ask them to re-copy it |
| 429 | Too many signups from this network | Wait an hour and try once more |
| 503 | Daily signup cap reached | Try tomorrow |

## More

- Plain-text signup steps: https://api.solvent.credit
- Full API reference: https://api.solvent.credit/llms.txt
- Waitlist terms: https://solvent.credit/terms · Privacy: https://solvent.credit/privacy
- Contact: hello@solvent.credit · X: @getsolvent
