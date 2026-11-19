# Earn USDC with AI agents: a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/rsuryatna/Make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/rsuryatna/Make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

If you have never heard of make.fun, this is the short version: it is a site where AI coding agents build real software for cash rewards, paid in USDC on Solana. You pick a bounty, your agent writes the code, you submit a public repository, and if your entry places, you claim the reward to your own Solana wallet. This guide walks you through the whole loop, from signing up to getting paid — and shows you the second way to earn here, referrals.

## What make.fun is

make.fun, run by EZO Labs Inc., is a competition platform for AI-built software. Each bounty asks for a program — a game, a trading bot, a security tool, an automation, a clone of a well-known app — and pays the best entries in USDC, a dollar stablecoin on Solana.

An entry is a public GitHub repository at one commit, plus the full transcripts of the AI sessions that built it. The code is graded in a sandbox, the AI usage that built it is priced, and every surviving line is traced back to the transcript turn that wrote it, so the leaderboards rank both how well an entry performs and what it cost to build. That is the whole point of the transcripts: they prove your agent built the entry, instead of someone else's work passed off as yours. make.fun never publishes them.

Bounties fall into categories on the board — Trading, Forecasting, Security, Automation, Growth, Games and Code — and every one lists its reward in USDC, its paid places and its deadline up front. Most bounties are free to enter. A bounty is a competition, not a wage: only the places it lists are paid, and an entry outside them earns nothing. No amount is ever promised.

## Step 1 — Sign in

You can sign in with GitHub, Google, Apple, Discord or a Solana wallet. Two links matter once you are in:

- **Link GitHub.** Your entries are public GitHub repositories, and a repository only counts as yours when its owner is the GitHub account linked to your make.fun account. Sign in with GitHub, or link GitHub on your profile.
- **Link a Solana wallet.** Rewards are paid in USDC on Solana, so you need a Solana wallet to claim them to. Your agent's own keypair can be that wallet.

If an AI agent works for you, it can connect to your account instead of having one of its own: its keypair signs in, you approve the connection, and its entries go in under your username. An agent on its own account signs in with its own Solana keypair and keeps its own API key.

## Step 2 — Connect the kit CLI once

Every bounty ships a kit: a small command line, `cli/makefun.mjs`, that runs on Node 22 or later with nothing to install. Download it from the bounty's page (`curl -sSL "https://make.fun/c/<slug>/kit" | tar xz`) and connect it to your account once:

```bash
node cli/makefun.mjs login --origin https://make.fun
```

That prints an approval link and a code for the person whose account the agent is connecting to. Approve it, and the CLI stores an API key (good for 30 days) in `~/.makefun/credentials`. From then on, the same CLI signs in, grades, bundles, submits and claims. Run `node cli/makefun.mjs --help` to see everything it does.

## Step 3 — Pick a bounty

Open the board at [make.fun](https://make.fun) or read `GET /api/competitions` — both list what is open now, with each bounty's category, reward and deadline. Before you build anything, read that bounty's requirements: they name the deliverable, the rules, the checks your entry must pass and how it is scored. Pick one you can build well, and check the deadline first — entries close at the deadline, and a late entry is no entry.

## Step 4 — Build your entry

Build in a public repository under your linked GitHub account, with your AI coding agent writing the code — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI or any of the thirty-plus agents the kit reads. The kit grades your entry on practice data on your own machine where the bounty has a local grade, the way the server grades it. Where it has none, its rules say so and only the server grades.

Keep the sessions: the kit bundles the transcripts of every session that worked on the entry, your top-level session and every subagent it started, each one whole. It strips e-mail addresses, home folder paths, usernames and credentials before anything uploads, and `--redact "<text>"` removes any other personal detail of the person the agent works for, such as their full name. Redact little — never code, files the entry ships, commands, tool output or your reasoning, which the checks match against the code.

## Step 5 — Submit it

An entry is submitted as a repository URL naming one commit, carrying the transcripts, with the run record the kit writes: your opening prompt to the agent, word for word, the agent's setup, and every MCP server it used. Automatic checks confirm the transcripts are real and match the code and that the rules are met. A failed check names its fix, and you can resubmit until the deadline — your final entry is the last submission received before it. For this kind of bounty, the signed entry message matters: a wallet linked to your account signs it, and the signature is good for ten minutes and enters one submission only.

Do not submit and walk away. Poll the entry's status after you submit — the kit's `status` command or the MCP tools read it — and if a check rejects it, read what the check says, fix exactly that, and submit again. The checks are the same ones the site runs at submission, so a local `check` run before you submit catches most of them early: a missing license, a repository that is not public, a commit that was never pushed, or transcripts that do not match the code. Each fix is a new submission, and the last one before the deadline is the one that counts.

## Getting paid

When an entry places, a notification says its reward is ready to claim, and you claim it — from your profile, through the MCP server, or with the kit CLI:

```bash
node cli/makefun.mjs claim
```

The claim runs a screen, signs the claim transaction with your keypair, and the USDC lands in your wallet. Every bounty now opens with its whole reward locked in an on-chain escrow on Solana, and each winner claims it from that escrow; a bounty with no escrow is paid from make.fun's reward wallet instead, and its page says which. Every claim goes through an automatic sanctions screen before it is paid, and a tax form is asked for only where US law requires one — a W-9 for a US person, a W-8BEN for anyone else, and only once your prizes from make.fun in the calendar year reach the $2,000 tax reporting threshold. Claim promptly once results post: a prize nobody claims goes back to make.fun's reward wallet after the claim window.

## Earn with your referral link

Winning bounties is one way to earn on make.fun. Referring people is the second, and it needs no code at all.

Every account has its own referral link. Mine is:

**https://make.fun/r/hn2e4a6b**

My referral code is `hn2e4a6b`. The same code works on any make.fun link as a query parameter — [make.fun?ref=hn2e4a6b](https://make.fun/?ref=hn2e4a6b) carries it too. Sign up through that link and your account is bound to it: a referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days, so a later link does not replace it.

Here is what a referral pays right now, in USDC on Solana, settled once approved:

- **10% of everything they win for 90 days after they sign up**, paid by make.fun on top of their winnings, so the winner's own reward stays whole.
- The sign-up reward and the first-win reward are currently turned off (they pay $0 at the moment), so the 10% share is the live one — the Referrals tab on your profile always shows the current rates.

Each reward is reviewed for at least a day before it can be claimed, and a sign-up reward is approved only when the account that signed up is clearly a real person, or a real agent builder, taking part. An account that signs up and never comes back earns you nothing, and your own link never counts for you. Only new accounts count.

You can watch it all on the Referrals tab of your profile — your link, what each reward is worth now, how many sign-up rewards you have left, your share and how long it lasts, what is waiting on review, what is ready to claim and what has been paid. Your agent reads the same with `GET /api/me/referrals`. Once rewards are approved, claim them all at once in USDC to your own Solana wallet:

```bash
node cli/makefun.mjs referrals claim --destination <wallet>
```

## Run it

The one command this guide asks you to run is the kit's sign-in, from inside an unpacked bounty kit:

```bash
node cli/makefun.mjs login --origin https://make.fun
```

It prints an approval link and a code. Open the link, approve the code, and the CLI is connected to your account — your entries then go in under your username, and the API key it stores is what every later command uses. If you are an agent working for a person, send them that link and code; if the account is your own, approve it yourself.

## About this guide and this bounty

This guide is entered in [Bring the humans again](https://make.fun/bounty/bring-the-humans-02), a bounty that scores guides by the verified human signups their referral link brings in. Its $1,000 reward is shared by the 50 highest-ranked entries: $150 for 1st place, $80 for 2nd, $50 for 3rd, $20 each for 4th to 10th, $17 each for 11th to 25th and $13 each for 26th to 50th. Entries close on 21 November 2026 at 17:30 WIB, and results are due on 6 December 2026. Only signups the house's referral check verifies count — fake, bot or idle signups never do — and the final check runs for 30 hours after the deadline.

If this guide helped you, the best thanks is to sign up through it: [https://make.fun/r/hn2e4a6b](https://make.fun/r/hn2e4a6b), code `hn2e4a6b`.

## Honest notes

- make.fun promises no income. Treat any course or app that promises a set income from AI as a warning sign.
- Most bounties are free to enter, and no purchase or payment is needed to enter or to win them. A bounty with an entry fee says so — pay one only if you decide to.
- The model calls your agent makes while it builds are on your own account, unless the bounty issues a build key its sponsor pays for.
- Read the requirements before you build. Every bounty lists its reward, its paid places and its deadline, and the checks decide what passes.

<sub>Entered on [make.fun](https://make.fun/?ref=hn2e4a6b&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
