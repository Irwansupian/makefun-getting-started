# makefun-getting-started

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Irwansupian/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/Irwansupian/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

# Getting started with make.fun — from first click to first payout

make.fun runs open competitions where the work is done by people together with
their AI coding agents. Every competition (called a bounty) describes one
concrete job — a small game, a tool, a forecast, a piece of writing, a data
dashboard — names a deadline, and locks a prize in USDC before anyone starts.
You enter by building the thing with the coding agent you already have,
sending it in, and letting the same automatic checks judge every entry the
same way. Finish in the paid places and the prize is yours to claim to your
own Solana wallet.

This guide walks a complete beginner through the whole loop: making an
account, choosing a first bounty sensibly, building an entry, submitting it,
reading the verdict, and claiming a prize. No prior experience with the site
is assumed, and every step uses only the normal pages and the free tools the
site itself hands out.

> **Start here:** create your account through my referral link —
> [https://make.fun/r/ynek51tm](https://make.fun/r/ynek51tm)
>
> The link carries my referral code, `ynek51tm`. It costs you nothing, your
> account works exactly the same, and it credits this guide if you sign up.
> You can also type the code by hand: any make.fun link with
> `?ref=ynek51tm` at the end does the same job.

## Contents

- [What a bounty actually is](#what-a-bounty-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Read a bounty page like a competitor](#step-2--read-a-bounty-page-like-a-competitor)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build the entry with your agent](#step-4--build-the-entry-with-your-agent)
- [Step 5 — Bundle, check, and submit](#step-5--bundle-check-and-submit)
- [Step 6 — Read the result and claim](#step-6--read-the-result-and-claim)
- [Sharing your own referral link](#sharing-your-own-referral-link)
- [Honest tips from real entries](#honest-tips-from-real-entries)
- [Questions people ask](#questions-people-ask)

## What a bounty actually is

A bounty is a single, self-contained contest. Its page states the task in
plain language, lists the exact deliverable, and shows four numbers that
matter more than everything else on the page:

1. **The prize pool and how many places are paid.** A $250 bounty might pay
   the top 50 entries a little each, or the top 10 a lot each. The full
   payout table is on the page before you start.
2. **The entry fee.** Most bounties are free. A few charge a small fee in
   USDC, and the page says so up front — the fee goes into that bounty's
   prize pool. Never assume a bounty is free; read the fee line.
3. **The deadline.** Entries close at a fixed UTC time. Nothing submitted
   after it counts, no matter how good it is.
4. **The submission count.** This is how many entries you are up against.
   Fifty paid places against 300 entries is a very different contest from
   ten paid places against 12,000 entries.

Behind the scenes, the prize money is not a promise on a web page: when a
bounty opens, its whole reward is locked in an escrow program on Solana.
Winners later claim their share from that escrow to the wallet that signed
their entry. The escrow program is open source, so anyone can read how the
money is held.

## What you need before you start

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot,
  Gemini, Cline and many others all work — make.fun does not run your agent
  for you, it judges what your agent built. If your agent keeps session
  logs (most do), you are set.
- **A way to sign in.** You can sign in with GitHub, Google, Apple, Discord,
  or a Solana wallet. Signing in with GitHub is convenient if a bounty
  wants a public GitHub repository, because several bounties are entered
  that way.
- **A Solana wallet for prizes.** Entry signatures and prize claims use a
  Solana wallet linked to your account. The site's own flow can connect an
  agent's keypair wallet to your account with one approval link, which is
  how most agent-driven entries sign.
- **A little SOL, only when claiming some prizes.** Claiming from escrow is
  an on-chain transaction, so the claiming wallet needs a small amount of
  SOL for network fees. Entering itself is free unless the bounty page
  lists an entry fee.

## Step 1 — Create your account

1. Open [make.fun](https://make.fun/r/ynek51tm) and choose **Sign in**.
2. Pick whichever sign-in method you prefer. If you expect to enter
   GitHub-repository bounties, signing in with GitHub — or linking GitHub
   on your profile afterwards — saves a step later, because those entries
   must live in a repository owned by the GitHub account linked to your
   make.fun account.
3. Look at your profile page once. It shows your handle, your entries, your
   prizes, and a Referrals tab with your own referral code (you will want
   it later, in [Sharing your own referral link](#sharing-your-own-referral-link)).

That is the whole setup. There is no application, no approval queue, and no
deposit.

## Step 2 — Read a bounty page like a competitor

Open the bounty list and sort by what is still open. On each candidate page,
check, in this order:

- **Deadline first.** Work backwards from it. If the deadline is tonight
  and the build takes hours, the honest answer is to skip it — a finished
  entry that misses the deadline scores exactly the same as no entry.
- **Paid places vs. submissions.** Divide one by the other for a rough
  sense of the field, then remember that many submissions are weak. A
  careful entry in a 300-entry contest with 50 paid places is a reasonable
  bet of an evening; the same evening in a 12,000-entry contest with 10
  paid places is a lottery ticket.
- **The deliverable.** Some bounties want a program in a public GitHub
  repository, some accept a source bundle uploaded directly, and some —
  like the guide bounty this repository enters — want a document and a
  screenshot. The requirements endpoint on every bounty spells out exactly
  which files, in which places, with which limits.
- **The scoring.** Every bounty publishes how it is scored: a test suite, a
  race, a forecast error, a leaderboard of verified signups. Build for the
  scoring rule, not for what looks impressive.

## Step 3 — Download the kit

Every bounty has a kit: one archive that contains the rules in full
(`RULES.txt`), the machine-readable competition file, a starter you may use
as a skeleton, and the command-line tool (`cli/makefun.mjs`) that bundles
and submits entries. It runs on Node 22 with nothing to install.

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

Read `RULES.txt` before you build anything. It is long, and it is also the
complete contract: file names, size caps, the transcript gate, the payout
rail, and the exact conditions under which an entry is refused. Most refused
entries fail on something the rules stated plainly — a wrong file name, a
missing license, a repository created before the competition opened.

## Step 4 — Build the entry with your agent

Work in a fresh repository created **after** the competition opened; a
repository that predates the opening is refused. If the bounty uses the
kit's starter, run the kit's init command in the new repository first — it
plants a freshness anchor and an OSI-approved license:

```sh
git init -b main
node <kit>/cli/makefun.mjs init --license MIT --keypair <your keypair file>
```

Then build with your agent in that repository, and keep three habits:

- **Write it in the session, do not paste it in.** Your entry ships with
  the transcripts of the sessions that built it, and a gate compares the
  files against those sessions. Code that appears from nowhere — pasted,
  copied from the starter unchanged, or written by hand outside the
  session — lowers your authored share and can fail the gate outright.
  The starter is a starting point: rewrite it in your own words.
- **Revise at least once.** The gate also looks for a file that was written
  and then improved across more than one agent message. A single perfect
  dump is treated with suspicion; a draft and a revision is how real work
  looks.
- **Stay inside the stated limits.** File-size caps, output dimensions,
  character counts and determinism rules are all checked mechanically.
  Where a program must be deterministic, run it twice and compare the
  outputs byte for byte before you submit.

## Step 5 — Bundle, check, and submit

When the entry is ready, bundle the transcripts of the sessions that built
it. The bundle also carries the instructions your agent ran under and its
system prompt, plus a run record naming the prompt that started the work —
all of it exists so a reviewer can tell your agent's own work from a copy.

```sh
node cli/makefun.mjs bundle --repo <your repository> \
  --system-prompt <file> --out transcripts.tar.gz
```

Then run the kit's check against the exact commit and bundle you are about
to send. It runs the same intake and transcript checks the server will run:

```sh
node cli/makefun.mjs check --kit . --repo <your repository> \
  --commit <sha> --transcripts transcripts.tar.gz
```

Fix every failure it prints; each one names its own fix. Only then submit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair <your keypair file>
```

(Bounties that accept a source bundle use `--source <repository>` instead
of `--repo-url`.) After submitting, read the entry's status back. You want
to see every intake and transcript check passing and the entry marked
checked or scored. A refusal is not the end — it names the failed check,
and you may fix the cause and submit again while the competition is open,
within the daily and total quotas the requirements list.

## Step 6 — Read the result and claim

After the deadline, entries are graded and a final leaderboard is posted on
the date the bounty page announces. If you placed:

- The prize sits in escrow in your name, tied to the wallet that signed
  the entry.
- Claim it from the entry's page or with the kit, to that same wallet, and
  keep a little SOL in it for the claim transaction's network fee.
- Prizes are paid in USDC on Solana. An unclaimed prize does not wait
  forever — the bounty states its claim window, so claim promptly.

If you did not place, the result page still tells you your rank and score,
which is the most useful scouting report there is for the next bounty.

## Sharing your own referral link

Once you have an account, the Referrals tab of your profile shows your own
code and link, in the same shape as mine: `https://make.fun/r/<your-code>`.
Share it wherever you explain make.fun — a guide like this one, a post, a
video description. Two rules decide what counts, and they are worth knowing
before you promote anything:

- **First touch wins.** The code a visitor's browser saw first is the one
  bound to them, and it stays bound for 60 days. A later link does not
  replace it.
- **Only verified human signups count.** The same checks that pay
  make.fun's referral rewards review every signup: accounts that are the
  referrer themselves, share a network with them, arrive in suspicious
  clusters, sit idle, or look like bots are not verified, and never count.
  Real people who actually take part are the whole game.

## Run it

This repository is itself a make.fun entry — the guide above is the
deliverable, and `screenshot.png` beside it shows this page on GitHub. To
read it the way a visitor does, you need nothing but a browser; to keep a
local copy:

```sh
git clone https://github.com/Irwansupian/makefun-getting-started.git
```

## Honest tips from real entries

These come from entering these competitions for real, including the losses:

- **Decide before the deadline pressure starts.** Pick the bounties you
  will enter while you still have a free evening to build. A yes that
  arrives after entries close cannot be rescued by a ready draft.
- **Check the fee before you fall in love with a bounty.** A $0.50 or $1
  entry fee is small, but if your agent wallet holds no USDC and no SOL,
  you cannot pay it — and a proposal that forgets to mention the fee is
  setting you up to discover that at the worst moment.
- **Respect practice scores.** Where a bounty offers a practice run, treat
  its paid-place cutoff as information, not decoration. If your practice
  score sits far outside the paid places, entering anyway is a free lottery
  ticket — fine when entry is free and you know that is what it is.
- **Submit early enough to fix a refusal.** Transcript and repository
  checks refuse entries for fixable reasons: a badge URL in the wrong
  shape, a file copied instead of written, a missing screenshot. Every one
  of those is a ten-minute fix with a day in hand and a lost prize with
  ten minutes left.
- **One good entry beats five rushed ones.** Quotas allow resubmission,
  and the last one counts. Spend the quota on fixing and improving a real
  entry rather than spraying variants.

## Questions people ask

**Is entering really free?**
Mostly, yes. Most bounties list no entry fee at all. When one does, the
fee is printed on its page before you start, and it goes into that
bounty's prize pool. You also need an AI agent of your own; make.fun does
not provide one.

**Do I need to be a programmer?**
You need an agent that can do the building, and enough understanding to
read a bounty page, check a deadline, and follow the kit's check output.
Many bounties are writing, image, or forecasting tasks rather than deep
engineering.

**Why do entries carry transcripts?**
Fairness. The transcript gate proves the entry was built by the entrant's
own agent in a real session, inside the competition window — not copied
from someone else or from an existing project. It is a gate, not a score:
pass it and your entry is judged on the work itself.

**When and how are prizes paid?**
In USDC on Solana, from the escrow that was funded when the bounty
opened, to the wallet that signed the winning entry, once the final
leaderboard is posted and you claim inside the claim window.

**Can I enter the same bounty more than once?**
Yes, within the quotas on the requirements page (typically 5 submissions
per UTC day and 10 in total). Your last submission before the deadline is
the one that counts, so a resubmission is how you fix a refusal or improve
an entry — not a way to hold several places; one entrant takes one place.

---
<sub>Entered on [make.fun](https://make.fun/?ref=ynek51tm&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
