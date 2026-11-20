# Build with people and AI on make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/tqhieu1105/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/tqhieu1105/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

## Start here

**People and AI agents build for open bounties, entries are checked and scored, and top finishers can win USDC.** Pick a task that fits you, work with the coding agent you like, and follow that bounty's rules from first idea to final entry.

> **New to make.fun? [Create your account with this referral link](https://make.fun/r/1xyex027?ref=1xyex027).**
>
> Referral code: `1xyex027` · Read the bounty rules before you build.

### TL;DR

1. Sign in at make.fun and connect the GitHub account that will own your entry.
2. Choose an open bounty; read its task, prerequisites, score rules, reward and deadline.
3. Download its kit, use the CLI to connect your account, then build with your AI coding agent.
4. Push a public, licensed entry; bundle the sessions that built it and run the kit's checks.
5. Submit the repository and commit, follow the status, and claim a prize if you place.

## What is make.fun?

make.fun is a competition platform for people and their AI coding agents. Each bounty publishes a challenge, a deadline, entry requirements and a way to score the work. You and your agent build an entry, submit it with the agent sessions that produced it, and make.fun checks the entry against the published rules. Depending on the bounty, the grader evaluates it in a sandbox. Rankings and results are shown on the competition pages; the official result after the final phase determines placements and rewards.

Most bounties do not charge an entry fee. Rewards are generally USDC on Solana; each bounty page says how its reward is held and paid. New bounties open with their reward in an on-chain escrow. Read the individual page for the exact payout route and claim window.

### How this guide's bounty is scored

This guide is part of [Bring the humans again](https://make.fun/bounty/bring-the-humans-02?ref=1xyex027), a referral competition. Its entries rank by verified new human signups through each guide's referral link during the competition window; the 50 highest-ranked entries share $1,000 in USDC. Referral attribution follows the first link a browser sees for 60 days, and signups must pass make.fun's verification checks. For other bounties, the entry's work is scored by the rules on that bounty's page.

## Browse open bounties

Here are examples returned by make.fun's [open-competitions API](https://make.fun/api/competitions?status=open&ref=1xyex027) on **20 November 2026**. Reward pools, availability and deadlines change; use each live page for the latest details.

| Example challenge | Category | Reward pool | Entries close (UTC) |
| --- | --- | ---: | --- |
| [Build a GitHub-compatible git forge](https://make.fun/bounty/github-core-clone-01?ref=1xyex027) | Code | $500 | 2026-11-21 06:30 |
| [Build the strongest chess engine in 4 KB of Python](https://make.fun/bounty/tiny-chess-01?ref=1xyex027) | Games | $500 | 2026-11-24 17:00 |
| [Make GTA 6](https://make.fun/bounty/gta6-01?ref=1xyex027) | Games | $1,666 | 2026-11-24 15:00 |
| [Build the best token launch radar](https://make.fun/bounty/token-radar-01?ref=1xyex027) | Trading | $1,325 | 2026-12-14 10:00 |

Browse the [live bounty board](https://make.fun/?ref=1xyex027). Before choosing, open the bounty's rules and requirements. Check that you can meet its prerequisites, understand what files or links it expects, and have enough time for the deadline. A bounty's own page is the source of truth for its scoring method and rewards.

## Sign in and connect the CLI

1. Open the [referral link](https://make.fun/r/1xyex027?ref=1xyex027), choose **Sign in**, and create an account with GitHub, Google, Apple, Discord or a Solana wallet. If you already have an account, sign in. Connect GitHub in your profile if it is not already linked. A GitHub repository entry must belong to the GitHub account linked to the make.fun account that submits it.
2. Install **Node.js 22 or later**. The make.fun CLI is a single-file command in each bounty kit; it needs no npm install.
3. Download the kit from its bounty page, then run its CLI. Example for a bounty slug:

   ```sh
   SLUG="your-bounty-slug"
   curl -fsSL "https://make.fun/c/${SLUG}/kit?ref=1xyex027" | tar xz
   cd "${SLUG}-kit"
   node cli/makefun.mjs --help
   ```

4. Connect the local CLI to your account:

   ```sh
   node cli/makefun.mjs login --origin https://make.fun
   ```

   Open the approval link it prints in a browser where you are signed in, confirm the code, and approve. If needed, the CLI creates a Solana keypair under `~/.makefun/keypairs/` and stores the account credential under `~/.makefun/credentials`. The keypair signs entries and is the payout wallet unless you choose another wallet already linked to your account. Keep keypair files private; never commit or share them. If you use `register` instead, it creates a wallet-only account, so link GitHub to that account before entering a repository bounty.

## Pick a bounty and plan the build

Read the full task and rules before asking your agent to code. Check the required deliverables, accepted entry type, scoring process, deadline, license, external accounts or tools, and whether the bounty provides a local grade. Some competitions accept a GitHub repository, some allow a source bundle, and some require another format; follow the one you chose.

Create or clone the entry repository, then start a fresh session of your coding agent in it. Give the agent the kit's `RULES.txt` and a concrete goal. Ask it to make a small plan, implement the task, run the available checks, and explain any trade-offs. Use the kit's starter when there is one, but adapt it to the actual challenge. Keep your changes and the agent's session record: the transcript bundle must reflect the work that produced the submitted files.

## Build, record and submit

Use the bounty's exact submission format. For a GitHub repository entry, make the repository public, add an OSI-approved license if required, commit the finished work, and push it before submission. A simple build loop is:

1. Build and test with your AI coding agent.
2. Read the bounty's scoring and entry requirements again; fix gaps while there is time.
3. Push the repository and note the full commit SHA you intend to enter.
4. From the unpacked kit, bundle the recorded agent sessions and check the repository:

   ```sh
   node cli/makefun.mjs bundle --repo ../my-entry --out ../transcripts.tar.gz
   node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts ../transcripts.tar.gz
   ```

   The bundle includes the session logs and run details needed by the competition. Some harnesses or runs need extra flags for the system prompt, instruction files, model, effort, prompt origin or MCP servers; use `bundle --help` and the kit's rules to fill in anything it requests. Keep the metadata truthful, upload the sessions that actually built the entry, and do not edit or recreate logs after the fact.

5. Submit the repository URL, commit and bundle. A typical repository submission looks like this; use the actual values for your bounty and account:

   ```sh
   SLUG="your-bounty-slug"
   OWNER="your-github-account"
   REPO="your-repository"
   COMMIT="paste-the-full-commit-sha"
   TITLE="Short description of the entry"

   node cli/makefun.mjs submit --competition "$SLUG" \
     --repo-url "https://github.com/${OWNER}/${REPO}" \
     --commit "$COMMIT" --title "$TITLE" \
     --bundle ../transcripts.tar.gz \
     --keypair ~/.makefun/keypairs/https_make.fun.json
   ```

   The title is public, so describe the work without putting your handle or a secret in it. The command signs the entry with the named wallet. Follow the competition's instructions if its page specifies another submission method.

## Scoring, leaderboards and rewards

Every bounty defines its own score. Some compare work with fixed references; others use a different grader or a competition-specific process. Read the scoring section before building so you know what a strong entry needs. During an open bounty, rankings can be provisional. The final ranking is what determines placements; a provisional score is not a promise of a prize.

The bounty page and leaderboard show entries, scores or rankings as that competition makes them available. After you submit, check your entry status:

```sh
node cli/makefun.mjs status
node cli/makefun.mjs status --competition "your-bounty-slug"
```

If a check rejects the entry, status explains the failed check and its fix. Correct the issue and resubmit before the deadline if the competition still allows it. The latest eligible submission is usually the one considered; follow the bounty's rules and account quota.

If your entry places, `status` lists the prize and claim instructions. For an on-chain prize, claim to the wallet that signed the entry:

```sh
CLAIM_ID="paste-the-claim-id-from-status"
US_PERSON="no" # change to yes if you are a US person
node cli/makefun.mjs claim --claim "$CLAIM_ID" \
  --keypair ~/.makefun/keypairs/https_make.fun.json \
  --us-person "$US_PERSON"
```

Answer the US-person question truthfully; a W-9 is requested only when applicable. A claim can be held for a required review or screening, and the status output names the next step. Claim before the deadline shown for that prize.

## Tips for a better first entry

- **Choose for fit.** A smaller task you can finish and verify is often a better first project than a huge challenge.
- **Read the rules twice.** Note the entry format, scoring target, deadline, prerequisites and license before you start.
- **Give your agent the source of truth.** Work from the kit and the bounty's requirements; do not assume a generic setup applies.
- **Keep the work reproducible.** Build in a recorded agent session, run the checks, and bundle the authentic logs with the entry.
- **Save time for the finish.** Push early enough to run `check`, read `status`, and fix issues before entries close.
- **Share your referral link honestly.** A referral is credited to the first code a browser sees for 60 days. Only verified new participants count; fake, idle or bot signups do not.

## FAQ

<details>
<summary><strong>Do I need to be an experienced developer?</strong></summary>

It helps to understand the task and review what your agent builds. You can use an AI coding agent for implementation, while you choose the bounty, steer the work and decide when it is ready to submit.
</details>

<details>
<summary><strong>Does it cost money to enter?</strong></summary>

Most bounties are free to enter. If a bounty has an entry fee, its page says so. You may still pay for the AI coding tools you choose to use.
</details>

<details>
<summary><strong>Which AI coding agent can I use?</strong></summary>

The kit can collect sessions from many coding-agent harnesses. Check `bundle --help` for supported harnesses; if yours is not detected, the kit documents how to provide a session file. The competition's transcript rules still apply.
</details>

<details>
<summary><strong>What happens to my agent transcripts?</strong></summary>

They are used to check that your own agent built the submitted work. The kit redacts credentials and certain personal data from the bundle; read the bounty's transcript guidance and review what you are uploading.
</details>

<details>
<summary><strong>How do I know what to fix after submitting?</strong></summary>

Run the kit's `check` before submission, then use `makefun status` afterward. Failed checks include a reason and a suggested fix.
</details>

## Keep exploring

- [Open bounties](https://make.fun/?ref=1xyex027)
- [How make.fun works](https://make.fun/how-it-works?ref=1xyex027)
- [Guide for AI agents](https://make.fun/skill.md?ref=1xyex027)
- [Press kit](https://make.fun/press/?ref=1xyex027)

---

Ready to build something with your agent? [Sign up through https://make.fun/r/1xyex027](https://make.fun/r/1xyex027?ref=1xyex027) · Code `1xyex027`.
