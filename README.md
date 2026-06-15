# Situation Match

Static single-page exercise for the Cafe Empathy activity. The app is built as a standalone HTML file with inline CSS and JavaScript, local MTS fonts, and media/data embedded directly in `index.html`.

## Purpose

The exercise helps children practice empathy: noticing emotional cues, matching situations with emotions, and identifying who did what after listening to short audio scenes.

All age modes share the same context block:

- Breadcrumbs: `Главная / Болталка / Кафе «Эмпатия»`
- Title: `Кафе «Эмпатия»`
- Description about empathy as a superpower and the task goal.

## Main Files

- `index.html` - production page used by GitHub Pages.
- `fonts/` - local MTS Wide and MTS Compact font files.
- `situation-match.html` - older/alternate version kept in the repository.
- `json.json` - source-like data file, currently untracked in this working tree.
- `letter_password.html` - unrelated/untracked file in this working tree.

## Age Modes

### 3-5

Image matching task:

- User selects one top image card.
- Then user selects one emotion option below.
- Options are unique; selecting an option already used moves it from the previous card.
- Nothing is selected automatically.
- If the user taps a lower option before selecting a top card, top cards play a short hint animation.

### 6-9

Flip-card matching task:

- User taps a card to select it.
- Tapping the selected card flips it to show the situation text.
- Then user chooses an emotion option below.
- Nothing is selected automatically after a match or after carousel scroll.
- If the user taps an option before selecting a card, top cards play a short hint animation.

### 10-12

Audio-based matching task:

- A modal explains that audio must be listened to first.
- The task is revealed after the first listen ends or after `Пропустить аудио`.
- Audio can be listened to at most two times total per task.
- Pausing and resuming does not count as a new listen.
- After the second full listen, the play button is disabled.

### 13-17

Audio-based matching task:

- A modal explains that audio must be listened to first.
- The task is revealed after the listen ends or after `Пропустить аудио`.
- Audio can be listened to only once.

## Checking Answers

After the user fills every item in the current task:

- `Проверить` becomes enabled.
- Correct cards receive `correct` styling.
- Wrong cards receive `wrong` styling.
- Result text shows `Верно X из Y`.
- The button changes to `Далее` or `Завершить`.

## Scroll Hint

The app has a floating `Листай вниз` cue for screens where more content is below the visible area. It should:

- appear only on the active screen;
- sit above the fixed footer and mobile browser UI;
- hide near the bottom of the scroll area;
- scroll the exercise down when tapped.

Mobile Safari and Chrome have dynamic browser toolbars, so the cue needs to use `visualViewport` or fixed viewport-aware positioning rather than relying only on the app container height.

## Development

No build step is required. Open `index.html` directly or serve the folder locally:

```bash
python3 -m http.server 4173
```

Then open:

```text
http://localhost:4173/index.html
```

For syntax checks, extract and check the inline script:

```bash
node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const m=html.match(/<script>([\s\S]*)<\/script>/); fs.writeFileSync('/tmp/situation-match-index-script.js', m ? m[1] : '');"
node --check /tmp/situation-match-index-script.js
git diff --check
```

## Deployment

Changes are committed to `master` and pushed to:

```text
https://github.com/vasilievanton/situation-match.git
```

The live page is served through GitHub Pages at `vasilievanton.github.io`.

## Git Notes

There are untracked files in the current working tree that are not part of recent changes:

- `json.json`
- `letter_password.html`
- screenshot PNG files with Russian names

Do not stage or remove them unless explicitly requested.
