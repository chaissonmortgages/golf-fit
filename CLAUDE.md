# Swing Fit: notes for Claude Code

Personal golf workout app, installed on Mack's phone as a PWA from GitHub Pages. Not a product.

## Structure
- `index.html`: the whole app (HTML, CSS, vanilla JS). No frameworks, no build step, no dependencies.
- `sw.js`: offline cache, network first with `cache: 'no-store'`.
- `.github/workflows/deploy.yml`: deploys to Pages on push to `main` and replaces `__BUILD__` in `index.html` and `sw.js` with a build id. Leave the `__BUILD__` placeholders in the source.
- `manifest.json`, icons: home screen install.

## Data (localStorage, keys prefixed `sf_`)
- `profile`: questionnaire answers `{name, level, days, env, equip, count, limits, goal, rounds, hcp, time}`
- `plans`: `[{id, pid, env, equip, days, time, start, sessions:[{date, week, tpl, done}]}]`
- `logs`: `[{id, date, start, dur, pid, planId, title, ex:[{id, name, tg, sets:[{reps, lbs, secs, pr}]}]}]`
- `active`: workout in progress, restored if the app is closed mid-workout
- `rounds`: golf round dates, `badges`: `{badgeId: dateEarned}`, `archive`: ended plans
Never change these shapes in a way that breaks existing data on the phone. If you must, migrate on load.

## Code map
- Exercises: `X(id, name, {...})` library. `poses` are two stick figure poses from `POSE`, animated by `figureSVG`.
- Programs: `PROGRAMS[pid].tpl` is a list of workout days, each a list of slots, each slot a preference list of exercise ids. `pickExercises` takes the first one that fits the equipment and sore spots. Goblet squat and a deadlift lead every Strength day: keep it that way.
- Progression: `target()`. Weight tips: `suggestFor()`. Personal bests: `logSet()`.
- Badges: `BADGES` array, each with `p(stats) => [current, needed]`. Earned dates are stored, never taken away.
- Round days: `shiftForRounds()` moves Strength and Power sessions off a round day and the day before.

## Style rules
- Mobile first, big tap targets, one handed use. Dark theme, green accent.
- Never use em dashes in UI text or comments.
- No `alert`/`confirm`: use `ask()` sheets.
