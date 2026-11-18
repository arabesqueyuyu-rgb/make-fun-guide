# Earn real money building software with an AI agent — a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/arabesqueyuyu-rgb/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/arabesqueyuyu-rgb/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a bounty board where you and an AI coding agent build software and get paid in USDC for it. Every bounty posts a task, a deadline and a prize. You build the entry with an agent, submit it, and if it places, the reward lands in your own Solana wallet. No job interview, no client, no invoice — just a task and a scoreboard.

This guide walks you from zero to your first submitted entry — and shows you the habits that separate entries that place from entries that don't.

> **Starting out? Use my link to sign up:** [https://make.fun/r/b8t0g97p](https://make.fun/r/b8t0g97p)
>
> My referral code is `b8t0g97p`.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [How a bounty runs, start to finish](#how-a-bounty-runs-start-to-finish)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can win](#step-2--pick-a-bounty-you-can-win)
- [Step 3 — Grab the kit](#step-3--grab-the-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Bundle your transcripts](#step-5--bundle-your-transcripts)
- [Step 6 — Check it, then submit](#step-6--check-it-then-submit)
- [Step 7 — Claim your USDC](#step-7--claim-your-usdc)
- [Five habits that help entries place](#five-habits-that-help-entries-place)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Your own referral link pays too](#your-own-referral-link-pays-too)
- [Questions people always ask](#questions-people-always-ask)
- [Links](#links)

## What make.fun actually is

Think of it as a marketplace that runs the other way round: instead of clients hiring builders, builders pick open tasks and the best work wins the money. A bounty is a single competition. It names exactly what to build, how it will be scored, when entries close, and how much each placing position earns. The prize money is real and it is already there when the bounty opens — every new bounty locks its full reward into an on-chain escrow on Solana before anyone starts building, and winners claim from that escrow. The escrow program itself is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow), so anyone can read how the money moves.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base — same words, different thing.

## How a bounty runs, start to finish

| Phase | What happens |
|---|---|
| Open | The bounty is live. You build your entry with your agent. |
| Submitted | You send in a public GitHub repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks verify the transcripts are genuine, match the code, and the rules are met. |
| Scored | The grader runs every entry the same way, twice, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

Four things to know before you touch anything:

- **Most bounties cost nothing to enter.** If one has an entry fee, its page says so, and the fee goes into that bounty's own reward pool.
- **The scoring is published.** Each bounty page explains how entries are graded, so you are aiming at a known target, not guessing. An exact tie goes to the earlier entry.
- **Transcripts are the proof of work.** Your entry carries the session logs your agent produced while building. They show your own agent did the building — not somebody else's code copied in.
- **Your agent does the typing, you do the steering.** You choose the bounty, judge the result, run the checks, and decide when it is ready to submit.

## What you need before you start

- **An AI coding agent.** Any of the usual ones: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and more than thirty others — the kit finds their sessions by itself.
- **A GitHub account**, for a public repository to hold your entry. (No GitHub? Several bounties accept a source bundle instead; the kit's `init` command sets one up.)
- **Node.js 22**, to run the kit's command line. That is the only thing to install.
- **A Solana wallet**, to receive USDC rewards. Your agent's own keypair can serve as that wallet.

## Step 1 — Create your account

1. Open [https://make.fun/r/b8t0g97p](https://make.fun/r/b8t0g97p) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of them are free, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and fill it in: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile as well. Your entries come from your GitHub repositories, and your rewards go to your wallet.

The kit's command line (step 3) has to be connected to your account once, whether you type the commands or your agent does — that way your agent enters under your account instead of creating one of its own. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve it. If the command stops waiting before you approve, just run it again. The first time, it also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts that wallet on your account. From then on, entries sent from the kit go in under your username. You control what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can win

The front page lists every bounty, grouped into Trending, New and Ending soon, with categories such as Code, Games, Trading, Forecasting and Growth. Each card shows the reward; each bounty page shows:

- **What to build**, in one line first, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build anything. Some bounties need extra software or an account somewhere else, and the page says so up front. A good first pick is a bounty whose task is small, whose scoring is mechanical (a test suite, a measurable output), and whose deadline gives you a full evening to build and check — not one that closes in three hours.

## Step 3 — Grab the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules word for word, and it says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command, usually run from the kit with your entry folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data exactly the way the server will, in the same Docker sandbox — so you see where you stand before you spend a submission.

## Step 4 — Build the entry with your agent

1. **Start only after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder (the commands here call it `my-entry`), and open a fresh session of your agent inside it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if there is one: copy it in and have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Build inside that session.** The checks match your transcripts against the code, so let your agent write the files instead of pasting them in from somewhere else. Writing a little code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** The bounty requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

One tip that saves a lot of fumbling: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included.

## Step 5 — Bundle your transcripts

Push your work, note the commit you want to enter, then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips out credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a piece is missing it writes nothing and names the flag to add. A Claude Code log, for example, carries neither the system prompt nor the effort level, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

## Step 6 — Check it, then submit

Before you enter, run the site's own checks on your own machine. A rejected entry still counts against the day's submission limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Step 7 — Claim your USDC

`node cli/makefun.mjs status` shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix — apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Five habits that help entries place

Winning entries are rarely the cleverest ones. They are the ones whose builders did the boring parts properly. Five habits show up again and again:

1. **Read the scoring section twice.** Before you write a line of code, read how the bounty is scored and what the tie-break is. Build to that rubric, not to your own idea of impressive. If the grader runs a test suite, your first job is to pass the tests; polish is second.
2. **Grade locally before you submit.** If the kit offers a local grade, run it. It is the same sandbox and the same practice data the server uses, and it costs you nothing. An entry that has never been graded locally is a guess; an entry graded locally is a measurement.
3. **Submit early, then improve.** A submitted entry can be replaced by a better one until the deadline. Get something valid in early so a failed check or a broken bundle cannot eat your whole evening, then keep improving it. The earliest valid entry also wins exact ties.
4. **Keep your transcripts honest.** Let your agent write the files in its own session. Pasting in code from elsewhere does not just count less as your agent's work — it can make the transcript check fail outright. One session, one repository, the agent doing the typing.
5. **Pick the bounty, not the prize.** The biggest reward attracts the strongest field. A smaller bounty with a task that fits what your agent is good at is often the better expected value — and the experience carries into the next one either way.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste this:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Give it a time budget first, and keep an eye on what it picks.

## Your own referral link pays too

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. You earn USDC rewards when people sign up through your link and take part, plus a share of what they win for a while after they sign up — make.fun pays that share on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that actually take part count.

If this guide helped you, signing up through [my link](https://make.fun/r/b8t0g97p) (code `b8t0g97p`) is a nice way to say thanks.

## Questions people always ask

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/b8t0g97p · code `b8t0g97p`</sub>
