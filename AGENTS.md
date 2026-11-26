# Ppoyo — Agent Team Rules

> Keep this top rules block stable so implicit prompt caching applies across runs.

## Never (Hard Rules)
- Never break the `localStorage` best-score key `'byeolsatang-best'` (`furball-chain.html:147,198`).
- Never introduce external build steps or unapproved CDN dependencies into this single-file HTML game.
- Never install packages, push, deploy, delete files, or spend money without explicit user approval.
- Never ask for API keys or secrets in chat; never send `thinking_budget`.
- Never pretend a check ran; paste the last 20 lines of actual command output and 1-based `path:line` citations.

## Project
- **Stack**: Single-file HTML/Canvas chain-reaction puzzle game (`furball-chain.html:1-526`).
- **Riskiest File**: `furball-chain.html` (`L182-237` spawn/move/rotate/hardDrop/place, `L238-330` `startDrop`/`resolve`/`finishPop`/`update` chain state machine, `L365-412` Canvas draw loop).

## Commands
- **Inline HTML `<script>` syntax check**:
  `node -e "const fs=require('fs'),vm=require('vm');const h=fs.readFileSync('furball-chain.html','utf8');let i=0;for(const m of h.matchAll(/<script(?![^>]*\bsrc=)[^>]*>([\s\S]*?)<\/script>/gi)){new vm.Script(m[1],{filename:'furball-chain.html#'+(++i)});}console.log('OK scripts:',i);"`

## Ownership
- `@coordinator` (`gemini-4-neon`, thinking `high`; `xhigh` only for 1 deep bug): Sole user interface; plans, assigns ownership, reviews verifier output, prepares PRs.
- `@game-dev` (`gemini-4-hydrogen`): Owns `furball-chain.html`. Must not touch `AGENTS.md` or `.agents/**`.
- `@verifier` (**must run on a different model than workers**, read-only): Owns no files; never edits. Reports to `@coordinator`.

## Done Means
1. Only `furball-chain.html` (and any explicitly requested docs/tests) changed inside worker `OWNS` paths.
2. The inline `<script>` syntax check passes cleanly.
3. `@verifier` opened all cited lines, verified the chain/drop state machine (`L238-330`) and `localStorage` key, re-ran the syntax check, pasted the last 20 lines, and approved within at most 2 reject rounds.
4. Changes land on a feature/fix branch and open a PR (never direct push to `main`).
