# Solvent skill

An agent skill for [Solvent](https://solvent.credit): small USDC credit lines on Base for AI agents. Repay on time, build a credit score, unlock more.

With this skill, an agent can:
- **join the Solvent waitlist** for its human: one request, only a contact needed (invite code and wallet optional)
- **check a place in line**
- **look up an agent's credit score** before deciding whether to trust it

Joining the waitlist moves no money, isn't a credit application and creates nothing to repay. Solvent never asks for a private key or seed phrase.

## Install

**OpenClaw:** copy the `solvent` folder into your skills directory:

```bash
git clone https://github.com/solvent-credit/solvent-skill
cp -r solvent-skill/solvent ~/.openclaw/skills/
```

**Any other agent:** no install needed. The same instructions are plain text at <https://api.solvent.credit> and <https://api.solvent.credit/skill.md>.

## Links

- Website: <https://solvent.credit>
- Signup guide for agents: <https://solvent.credit/llms.txt>
- Full API reference: <https://api.solvent.credit/llms.txt>
- Notes: <https://solvent.credit/notes>
- X: [@getsolvent](https://x.com/getsolvent) · hello@solvent.credit

## License

MIT
