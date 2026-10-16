# Relativity & Rocket Physics graphs

Notes for a future Claude. Tim's global rules in `~/.claude/CLAUDE.md` still apply.

## What it is
- A single-page physics toy. It has four interactive Chart.js graphs: time dilation, length contraction, the relativistic rocket equation (six propellants) and relativistic vs Newtonian kinetic energy.
- Users: Tim and anyone he shows it to. There are no accounts, no backend and no stored data.
- Live: https://timothyhadfield.github.io/relativity-graphs/ (repo `TimothyHadfield/relativity-graphs`, public).
- The README says it's "best on a laptop": right-click-hold shows exact values and double-click zooms. Neither works on a phone.

## File map
- `index.html`: everything. CSS, the head script (shared custom tooltip, crosshair plugin, right-click-hold and double-click zoom handlers, reset on double-click outside), and the body script (physics functions and the four charts).
- `README.md`: GitHub showcase page with the screenshots in `docs/screenshots/`.
- `progress.md`: handoff/status file.
- Chart.js 4.4.0 loads from cdnjs in `<head>`. It must stay blocking (no `defer`) because the inline head script calls `Chart.register` right away.

## Physics (checked against textbook formulas on 2026-10-16)
- Time dilation and length contraction: `sqrt(1 - β²)` = 1/γ.
- Rocket: Ackeret relativistic rocket, mass ratio `((1+β)/(1-β))^(c/(2·v_ex))`, fuel = payload·(ratio − 1), payload 1000 kg. For chemical, nuclear and ion fuel this overflows to `Infinity` at moderate β. That's expected: those points simply aren't drawn or clickable.
- KE: `(γ−1)mc²`, computed as `β²γ²/(γ+1)·mc²` to avoid cancellation at low β. Newtonian ½mv².
- Constants: c = 299792458 m/s. Hiroshima bomb 6.3e13 J. Sun's output 3.8e26 J/s. Sun 1.989e30 kg. Observable universe (ordinary matter) about 1.5e53 kg.

## Run locally
- `python -m http.server 8106` in this folder, then open http://localhost:8106/ (start the server with the background option).

## Test
- There is no test suite, and none should be added without Tim asking. Verify with `node ~/.claude/tools/phone-view.mjs http://localhost:8106/ --desktop --eval "<js>"`. The chart objects (`timeChart`, `spaceChart`, `rocketChart`, `keChart`) and the functions (`fuelMass`, `relKE`, `gamma`, `timeDilation`) are globals, so `--eval` can call them directly.
- Check at phone width too (`--full`). The page has **no meta viewport**, so iPhone renders it as a zoomed-out 980px desktop page. The README phone screenshot shows that look.

## Deploy
- GitHub Pages from `main`, root folder. Push to `main` and Pages rebuilds. Check it with `python ~/.claude/hooks/live-check.py "<main checkout>"`.

## Traps
- The tooltip config is in two places. Each chart's `options.plugins.tooltip.callbacks` is dead (tooltips are disabled), and the live text comes from `chart.$customTooltipConfig`. Change both or neither.
- Every click on the rocket chart zooms to the nearest fuel line, so a double-click there also fires that fuel zoom first. `window.__suppressRocketClick` only blocks clicks that come after the double-click.
- `.gitignore` used to ignore `CLAUDE.md`. That line was removed on 2026-10-16 so this file is committed.
