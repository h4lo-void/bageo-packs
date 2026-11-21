# bageo-packs

The public library of local data for [Bageo](https://github.com/h4lo-void/bageo-call): regional phone manners, multi-language translations, regional scam patterns, voice pack prompts and mascot artwork. Bageo itself ships only its core nine languages and built-in basics; everything beyond the core lives here so installers stay small and anyone can improve local content.

Every file starts as an AI draft (`draft` / `ai_checked`) until people who live there review and mark it `local_reviewed`. If you live in a region or speak a language, your review is the most valuable contribution.

Also in `README.zh-TW.md` (繁體中文).

## What is inside

- `regions/<code>.json`: one file per region (74 regions). Countries, primary language, parcel rules, number/time readback, common scams, local words, five talk styles for owner and assistant, and local details for stalling a scam caller.
- `languages/<code>/`: one folder per extra language (70 languages + shared call layers). `call.json`, `names.json`, `notify.json`, `app.json`, `desktop.json`, `console.json`, and `_review.json`.
- `art/<region>.json`: SVG mascot drawings for the 64 non-built-in regions, downloaded on demand by the console once a region is reviewed.
- `scams/`: isolated country phone-scam intelligence (`country_scams.json` and `countries/<iso>.json` for 112 countries) plus extra-language scam keywords and own-matter phrases (`keywords.json`).
- `voices/`: regional voice pack lines (`lines.json`) and release voice-pack manifest (`bageo-voices-index.json`).
- `source/`: English source strings, notes and `glossary.json`. Do not edit source text here (update in `bageo-call` first).
- `templates/`: templates for adding or editing a region or language.

## Help in three steps

1. Open the file for your region or language on GitHub (for example `regions/tw.json` or `languages/it/app.json`), click edit, and fix what is wrong. To add a region, copy `templates/region.json`.
2. Open a Pull Request. Automated checks run cleanly and report any schema or translation rules in plain words.
3. Tick the checklist boxes in the Pull Request form (CC0 license and local reviewer confirmation). Maintainers review before merging.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## How Bageo uses it

Bageo bundles the core built-in baseline and fetches updates or on-demand extras (`lang-<code>.json.gz`, `art-<region>.json`, voices) from GitHub Releases here only when configured or requested in the console. Downloaded data is re-checked locally with the same validation rules before use.

Maintainers publish a release by pushing a tag named `vYYYYMMDDNN` (for example `v2026112101`), which validates all sources and builds all packs and indexes as release assets.

## License

Data, artwork and translations: [CC0-1.0](LICENSE) (Public domain).

Workflows and scripts (`.github/` and `tools/`): Apache-2.0, see [LICENSE-scripts](LICENSE-scripts).
