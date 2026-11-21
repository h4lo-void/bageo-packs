# Contributing

You can add a region, add a language, or fix a line. Every change is a pull request; checks run by themselves and say what to fix. Also in `CONTRIBUTING.zh-TW.md` (繁體中文).

## Add or change a region

1. Copy `templates/region.json` to `regions/<code>.json`. The code is lower-case letters (and dashes), at most 24 characters, and it must be the same as the file name (`tw` in `tw.json`). To change a region, just edit its file on GitHub.
2. Fill in the fields below. Write both `en` (English) and `zh` (Traditional Chinese). If you can write only one, write the other as well as you can and say so in `notes`; a maintainer will tidy it.
3. Keep `"status": "draft"` unless you are from there (see "Draft and local_reviewed" below). Open a pull request.

Lengths are counted in characters. The first number is for English, the second for Chinese.

| Field | What it is | Limit |
|---|---|---|
| `schema` | Always `1` | |
| `code` | Region code, same as the file name | 24 |
| `countries` | Countries of this region, two-letter lower-case ISO codes. A country belongs to one region only | 30 countries |
| `name` | `en`, `native` (how locals write it), `zh` | 40 each |
| `lang` | The main language, a code from the [official Gemini Live list](https://firebase.google.com/docs/ai-logic/live-api/limits-and-specs), such as `en-US`, `ja-JP`, `th-TH`. Chinese is `cmn` only | |
| `layer` | Optional. Which language folder to share with. Left out, it is the first part of `lang` (`en-US` uses `languages/en`) | |
| `stt` | Optional. Listening language, only when it differs from `lang` (for example `hi-IN` for a region that speaks English) | |
| `other_langs` | Optional. Other languages heard there | 4 codes |
| `chinese_dialects` | `true` only for regions made of Taiwan, Hong Kong, Macao, mainland China, Singapore, Malaysia | |
| `hello` | How a person says hello, in the local language: `hello` and `hello_again`. Needed when the language is not one of Bageo's nine interface languages, or a country in a non-English region is not in Bageo's own country list. Never contains `{owner}` | 30 and 60 |
| `delivery` | Where parcels are left | 80 / 36 |
| `delivery_key` | Optional. A short word for the place, `en` and `zh` | 12 |
| `readback` | How phone numbers, times and days are read aloud | 80 / 36 |
| `fraud` | The scams that are common there. English must contain "scam", Chinese "詐騙" | 110 / 50 |
| `habits` | Local words and habits that really differ from the next region | 420 / 190, together with the language folder's |
| `stall_local` | Everyday snags to get stuck on when stalling a scam caller | 150 / 70, together with the language folder's |
| `talk_style` | `persona` (the owner) and `assistant`, each with cells `"1"` to `"5"`, from casual (1) to crisp business (5) | 200 / 90 per cell |
| `vocab` | Optional. Words by situation, for example `"bank": ["card reader"]`. Situation names are `[a-z_]`, 2 to 16 characters | 8 situations, 6 words each, 24 characters per word |
| `status` | `draft` or `local_reviewed` | |
| `reviewed_on` | Date as `YYYY-MM-DD`, required for `local_reviewed`, not in the future | |
| `notes` | Optional working notes, dropped when the pack is built | 1000 |

Two totals also apply to the region after it is merged with its language folder. Parcels, readback, scams and habits plus the longest talk-style cell: at most 430 (English) and 410 (Chinese). Scams plus stall details: at most 220 and 470.

Each talk-style cell says three things: how to address people, how long the sentences are, and how warm the tone is. Cell 3 always says that after the caller finishes a point, the answer is one full sentence, not a word or two. Give at most three example words per cell, in the local language, and end with "varied". `{owner}` is the owner's name and is allowed only in talk-style cells.

## Add or change a language folder

Copy `templates/language-call.json` to `languages/<code>/call.json`. The folder name is the language code (`es`, `th`, `cmn`) and `layer` inside must be the same. Fill in only what every region of that language shares, so a region file never repeats it.

How the two merge: a region's `delivery`, `readback`, `fraud`, `hello` and `stt` replace the language folder's. `habits` and `stall_local` are the language folder's text followed by the region's. Talk-style cells are replaced one by one. Vocabulary is joined, the region's words first.

The language folder's own limits are smaller: `habits` 200 / 90 and each talk-style cell 120 / 55. Its `name` has `en` and `zh` (40 each). Its other fields use the same limits as a region.

## Writing rules

- Give a direction, not a script. Describe the situation and the feel, then let the AI use its own words. Do not write word-for-word lines or a fixed order of steps.
- Do not repeat the fixed rules. Bageo already forbids giving codes or personal details, agreeing to transfers, promising for the owner, and telling the caller to wait. Leave them out.
- Name only languages Gemini Live speaks (see the official list). Do not name dialects or accents that are not on it, and do not tell the AI to answer in one language only.
- Use the form locals use for money, shops, dates and numbers, but no real web addresses, phone numbers, e-mail, names of real people or six or more digits in a row. Write a number as a pattern such as 06 xx xx xx xx.
- Keep it short. Only put in what really differs there; leave out what is true everywhere.

## Translate Bageo's text

Bageo's notifications, web console and desktop program can be translated into any language on the Gemini Live list (the phone APK ships its multi-language resources built into `bageo-call`). Each language has a folder, `languages/<code>/`.

1. The English original is in `source/en`. Do not change it. `source/meta` says where each line shows up and who reads it, so you can pick the right tone.
2. Put your translation in your language's folder: `notify.json` (notification messages), `console.json` (web console), `desktop.json` (desktop program) and `names.json` (the language's own name; copy `templates/language-names.json`). Use the same keys as the English files.
3. Keep every placeholder, such as `{n}`, `{name}`, `{}` and `%1$s`. You may move it to where your language needs it, but do not add, drop or rename one.
4. Use the fixed words in `source/glossary.json` every time. "Bageo" is never translated.
5. No web addresses, e-mail, phone numbers or six or more digits in a row, unless the English line has them too.
6. In `_review.json`, each line has a `status`: `ai_draft` (written by AI, nobody has read it), `ai_checked` (translated back and the meaning held), `needs_fix` (the meaning is off) and `local_reviewed` (a person from there read it).
7. If you are from there and you read a line, fix it or approve it, set it to `local_reviewed` and write today's date in `on` (`YYYY-MM-DD`). A file counts as its lowest line, so it is `local_reviewed` only when every line is.
8. Before you open the pull request, run the check (see "Check on your computer"). It must report no issues.

## Draft and local_reviewed

New content starts as `draft`: not yet read by someone from there. Bageo shows that it is a draft.

Set `status` to `local_reviewed` and `reviewed_on` to today's date only when you live in that region (or speak the language as your first language), have read every field of the file, and it matches how people really talk there. Tick the matching box in the pull request. If you change text in a reviewed file and you are not from there, set it back to `draft`.

When a region and its language folder are merged, the lower of the two statuses is used. The checker only checks that a date is present; whether the review is real is something a maintainer judges when reading the pull request.

## Check on your computer

You do not have to. Every pull request is checked automatically. To check before sending, you need Rust and git:

```
git clone https://github.com/h4lo-void/bageo-call
cd bageo-call
git checkout <the commit written in tools/bageo-call.ref>
cargo run -p bageo-packs --release -- check <path to this folder>
```

A good result is one line: `ok: N region(s), M language layer(s)`. Otherwise each line gives the file, the field, a rule code and what is wrong, and the last line counts the issues. Rule codes: R01 format or unknown field, R02 code, R03 country, R04 language, R05 missing field, R06 length, R07 placeholder, R08 web address, phone number or six digits, R09 forbidden phrase, R10 unsupported language or accent, R11 Chinese dialect flag, R12 status or date, R13 index, R14 line break, hidden or bracket characters, R15 release index.

## What a pull request runs

The `Check` workflow runs on every pull request and every push. It gets this repository and the checker from `h4lo-void/bageo-call` (the commit named in `tools/bageo-call.ref`) and runs the command above on the whole folder. It must pass before a maintainer merges. A maintainer also reads every change, because no check can tell whether text looks fine but teaches the wrong thing.

## License agreement

By opening a pull request you agree, in the box of the pull request form, that your data and translations are released under CC0-1.0 and any scripts under Apache-2.0. There is no other agreement to sign.

## For maintainers

When the checker's rules change in `bageo-call`, put the new commit into `tools/bageo-call.ref` in its own pull request. To release, push a tag like `v2026112101`; the Release workflow does the rest.
