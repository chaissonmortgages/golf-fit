# Swing Fit

Golf fitness programs and workout tracker for my phone. One HTML file, no build step, no accounts. Workouts save on the phone itself.

## What's in it
- Questionnaire: experience, days per week, gym or home (bands, weights, bodyweight), exercises per workout, sore spots, goal
- Programs (6 weeks each): Power & Speed, Core & Balance, Flexibility & Mobility, Strength, plus a 10 minute Pre-round Warmup
- Workout player: timer, moving diagram, form cues, sets with reps and weight, rest timer, YouTube demo link
- Weight suggestions and personal bests, progress charts, 24 badges
- Calendar of bubbles (green done, yellow skipped), golf round days that move heavy leg days, one tap add to Apple or Google Calendar

## Hosting and updates
Netlify, linked to this repo. Every push to `main` deploys automatically (`netlify.toml` holds the build step).

The app is only reachable by its link. It is kept out of search engines.

On iPhone open the Netlify link in Safari, then Share > Add to Home Screen.

Updates are automatic. Each deploy stamps a new build id into `sw.js`, the service worker fetches fresh files every time the app opens, and the installed app reloads itself into the new version (it waits if a workout is in progress). The build id shows at the bottom of the Profile tab.

Your data lives in the phone's storage for this web address. It survives updates. Keep the same URL so it stays put, and use Profile > Back up data now and then.
