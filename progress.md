# progress.md: Relativity & Rocket Physics graphs

## START HERE
Last updated 2026-10-16. Read `CLAUDE.md` (file map, physics, traps), then this file.

## Goal right now
Nothing is in progress. The app is finished and live at https://timothyhadfield.github.io/relativity-graphs/.

## Status
| Area | State |
|---|---|
| Four graphs | Live and working |
| Physics | Checked against textbook formulas 2026-10-16 |
| Tests | None (single HTML file). Verify with phone-view `--eval` |
| Sweep 2026-10-16 | Fixed the observable-universe label threshold and the KE "NaN×" at 0c. Added meta description and CLAUDE.md |

## Authorized next steps
None.

## Standing instructions
- None recorded from Tim for this project yet. The global ones apply.

## Traps
- There's no meta viewport. The phone look is a zoomed-out desktop page, and the README screenshot shows that look. Don't add one without Tim's OK.
- Right-click-hold and double-click don't exist on a phone.

## Decisions
- 2026-10-16: Rocket tooltip threshold for "more than the mass of the observable universe" is now 1.5e53 kg (it was 1e30 kg, about half a Sun). The "~N suns" branch is live again.
- 2026-10-16: KE ratio shows 1.00× at v = 0 (the limit) instead of NaN×. KE uses the cancellation-free form of γ−1.

## NOT verified
- On a real iPhone. Checked only in WebKit with phone-view.

## Rejected / parked
- (none)
