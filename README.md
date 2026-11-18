# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/khaliefk/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/khaliefk/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun pays real money for software. People post bounties — a task, a deadline, a
reward in USDC — and you (or your AI coding agent) build an entry for it. If your
entry places, you claim the reward to your own Solana wallet. No interviews, no
clients, no invoices. Just the work, judged the same way for everyone.

This guide takes you from zero to your first submitted entry.

> **Signing up? Use my link:** [https://make.fun/r/rzmrszv7](https://make.fun/r/rzmrszv7)
>
> My referral code is `rzmrszv7`.

## Contents

- [How a bounty works](#how-a-bounty-works)
- [What you need before you start](#what-you-need-before-you-start)
- [1. Make your account](#1-make-your-account)
- [2. Pick a bounty you can actually build](#2-pick-a-bounty-you-can-actually-build)
- [3. Download the kit](#3-download-the-kit)
- [4. Build the entry](#4-build-the-entry)
- [5. Check it, then submit it](#5-check-it-then-submit-it)
- [6. Claim your reward](#6-claim-your-reward)
- [Mistakes that cost people money](#mistakes-that-cost-people-money)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions](#questions)

## How a bounty works

Every bounty runs through the same stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real, match the code, and the rules are met. |
| Scored | The grader runs every entry the same way, twice, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

Three facts that matter before you start:

- **Most bounties are free to enter.** A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward pool.
- **The reward is locked before you start.** Every new bounty opens with its full reward in an on-chain escrow on Solana. The escrow program is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your transcripts are part of the entry.** Your sessions show that your own agent did the work. Passing off someone else's code — or code from an earlier project — as a fresh entry gets caught by the checks.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider and more than 30 others are found by the kit on their own.
- **A GitHub account**, for a public repository. Some bounties take a source bundle instead, but a GitHub repository is the normal route.
- **Node.js 22** to run the kit's command line.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet.

## 1. Make your account

1. Open [https://make.fun/r/rzmrszv7](https://make.fun/r/rzmrszv7) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from your profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

Your agent's command line needs to be connected to your account once, whether you type the commands or your agent does. That way your agent enters under your account instead of making one of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve it. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine and puts its wallet on your account; the commands below sign your entries and claims with it.

## 2. Pick a bounty you can actually build

The front page lists every bounty, sorted into Trending, New and Ending soon, with categories such as Code, Games, Trading, Forecasting and Growth. Each card shows the reward. Each bounty page shows what to build, the full rules, how it is scored, and the phases (when entries close, when results land).

Read the rules before you build. Three things to check first:

- **Can you build it?** Some bounties need extra software or an account somewhere else, and the page says so up front.
- **How is it scored?** Some are graded by running code, some by a judge, some (like this one) by verified signups. Build for the score, not for what looks impressive. A referral bounty, for example, is won by the guide that actually brings people in — not by the longest guide.
- **When does it close?** A rejected entry still counts toward the day's entry limit, so don't burn attempts on a deadline you can't meet.

## 3. Download the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it — it is the only document that decides whether your entry passes or fails.

## 4. Build the entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder, and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add whatever the bounty asks for** — a README, a screenshot, a strategy note. Its requirements give you the exact template; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## 5. Check it, then submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Before you enter, run the site's own checks on your machine. This is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

After you submit, `makefun status` shows where the entry stands: **submitted**, **checked**, **scored** or **rejected**. A rejected entry lists every failed check together with its fix. Fix them and submit again — you can keep going until the deadline, within the bounty's daily limit. Your latest entry is the one that counts unless you pick an earlier one.

## 6. Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Mistakes that cost people money

- **Starting before the bounty opens.** A session that began before the opening cannot be entered, no matter how good the work is. Open a fresh session after the bounty opens.
- **Submitting without checking locally.** A rejected entry still counts toward the day's limit. Run `check` first — it is free and it catches most misses.
- **Copying the starter unchanged.** The starter is a starting point, not an entry. Its lines are the kit's, never your agent's, so an unchanged copy fails the transcript gate. Rewrite it, cut it, add your own work.
- **Pasting code in from outside.** Lines your agent did not write count against you. Let the agent write the files in its own session.
- **Forgetting the license.** An entry without an OSI-approved license is refused. Add MIT (or another OSI license) before you submit.
- **Shipping a stale screenshot.** If the bounty asks for a screenshot of your entry's page, take it after the final version is published — a screenshot of an earlier draft shows the wrong thing, and the board shows it to everyone.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, and a share of what they win for a while after they sign up, which make.fun pays on top so their own reward stays whole. Your link, what each reward is worth right now and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped, signing up through [my link](https://make.fun/r/rzmrszv7) (code `rzmrszv7`) is a nice way to say thanks.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local checks where there are any, read what the checks say and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>How do referral signups get counted?</strong></summary>

A signup counts for your link only if the visitor's browser first saw your code — that first touch wins for 60 days, and a later link does not replace it. Only signups the referral system verifies count, and each one sits in review for at least a day first. Sharing the link is not enough on its own: the person has to sign up and actually take part.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/rzmrszv7 · code `rzmrszv7`</sub>
