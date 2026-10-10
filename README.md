## Vũ Duy Khang

I'm a first-year Information Security student at PTIT Ho Chi Minh City, on the
blockchain track. Most of my time goes into smart contract security.

I've been around crypto since 2022. That's where the interest started: I wanted
to know why so many token contracts turn out to be traps.

### Smart contract security

[smart-contract-security-lab](https://github.com/Vuduykhang2306/smart-contract-security-lab)
is one audit done start to finish. The target is a tax token with nine
findings. The repo has a runnable Foundry PoC for each one, the full report,
the patched contract, and a retest suite that runs every exploit again against
the patch. 27 tests, CI on every push. The report is
[here](https://github.com/Vuduykhang2306/smart-contract-security-lab/blob/main/reports/2026-09_MemeTax_audit-report.md).
If you only have time for two findings, read M-01 and M-02.

I missed the ninth finding in my manual pass. It only came up when I wrote an
invariant saying every ETH the contract owes has to be covered by its balance.
Writing that down made me check what moves ETH without updating the books, and
the fee swap pays out the whole balance, dividend pool included.

I also did a
[public review of a launchpad token template](https://github.com/Vuduykhang2306/smart-contract-security-lab/tree/main/reviews/2026-09_FatTokenV5)
on Ethereum mainnet, using a dead token as the example. 8 findings, 7 PoCs that
run on a mainnet fork, and the contract address is in the report so anyone can
check it. The most useful result: every dangerous feature in that template is
switched on or off in the constructor, and no function can switch it back on.
A buyer can read five values on-chain and know for good what the deployer can
do to them.

I kept the scope small on purpose. I picked a near-dead contract and only wrote
up what the deployer can do to holders. None of it helps anyone take someone
else's funds.

The four invariants run under Foundry and again under
[Echidna](https://github.com/Vuduykhang2306/smart-contract-security-lab/tree/main/test/echidna).
Both pass, and neither found anything the other missed. What I got out of it
was a control: the same properties run against the unpatched contract, where
they have to fail. CI checks all four results by name. A passing fuzz run looks
the same whether the code is correct or the harness never reached the bug, so
the control is how I know which one it is.

### Built on top of that

[token-powers](https://github.com/Vuduykhang2306/token-powers)
([live](https://vuduykhang2306.github.io/token-powers/)): paste an ERC-20 from
mainnet and the page shows what its deployer can still do to the people holding
it. It came out of the review above. "Read five values and you know your
exposure" doesn't help much if you don't know which five, so the page reads
them for you.

The page keeps two things apart. An owner power is something a privileged
address can do later, like raising the tax or freezing a wallet. Renouncing
ownership removes it. A baked-in mechanism runs by itself on every transfer.
Renouncing ownership makes that one permanent, because the setter that could
have turned it off can't be called anymore either. So `owner() = 0xdead` is
good news for the first kind and bad news for the second.

It also simulates a sell. Flags only tell you which powers exist. To see
whether selling works right now, the page sends an `eth_call` with a state
override: give the wallet a fake balance, try the transfer, check whether it
reverts. It's the same trick as `deal()` in my Foundry fork PoCs, done through
the RPC.

The whole thing is read-only. It never asks for a signature and never builds a
transaction.

### Writing

I write up the parts I got wrong first at
[vuduykhang2306.github.io](https://vuduykhang2306.github.io):

- [Whose money is this?](https://vuduykhang2306.github.io/2026/10/09/whose-money-is-this.html)
  I read the same function twice and still missed H-04. A one-line invariant
  found it.
- [A green fuzzing run doesn't prove much](https://vuduykhang2306.github.io/2026/10/09/a-green-fuzzing-run.html)
  Foundry and Echidna agreed with each other, and why I added a negative
  control anyway.
- [The first drafts of three findings](https://vuduykhang2306.github.io/2026/10/09/first-drafts-of-three-findings.html)
  M-01, M-02 and L-01 each started out wrong, in three different ways.
- [Renounced doesn't mean safe](https://vuduykhang2306.github.io/2026/10/09/renounced-is-not-a-verdict.html)
  Owner powers and baked-in mechanisms, from the FatTokenV5 review.

### Other projects

- [nodex.io.vn](https://nodex.io.vn): an e-commerce platform I built and run
  myself, with paying customers. Next.js, a REST API for customers who want to
  automate, and a Linux VPS behind Cloudflare. It means I have a live system of
  my own to keep safe, which I think matters if you audit other people's code.
- [aquaoracle-app](https://github.com/Vuduykhang2306/aquaoracle-app) and
  [Esp32_AquaOracle_Programm](https://github.com/Vuduykhang2306/Esp32_AquaOracle_Programm):
  water-quality monitoring for aquaculture ponds. An ESP32 sensor node,
  Supabase, a PatchTST forecasting model and a Flutter app. It made the national
  final of the Vietnam Youth Innovation Contest 2026.
- CTF, mostly cryptography. I'm
  [13th in Vietnam on CyberTalents](https://cybertalents.com/members/vuduykhang/profile)
  and captain of C0mt4m367 and meobeo.

  You can check the ranking on that profile, or on
  [cybertalents.com/worldrank](https://cybertalents.com/worldrank) with the
  country set to Vietnam. Screenshot from 15 September 2026:

  ![CyberTalents Vietnam leaderboard, row 13](assets/cybertalents-vietnam-rank-2026-09-15.png)

### About my older repos

Some of them used to have Supabase and Gemini keys in the source, and the ESP32
firmware had a Wi-Fi password in it. I found these when I went through my own
account, removed them from the git history, and moved every project to config
files that aren't committed. The keys had already stopped working by then, but
that was luck. I didn't have a process for it at the time.

### Contact

vuduykhang23062008@gmail.com. Ho Chi Minh City, or remote.

I'm looking for internships in smart contract security, Solidity development or
Web3 frontend. I'm interested in all three for the same reason: I like knowing
what a contract actually does before I trust it.
