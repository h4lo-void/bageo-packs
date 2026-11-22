# Prompt texts

The words Bageo tells the AI during a call are built into Bageo. A file here rewords some of them without a new Bageo: after the next release of this repository, a Bageo whose owner presses *Check for updates* in the console downloads the changes and uses them from the next call.

Also in [README.zh-TW.md](README.zh-TW.md) (繁體中文).

## Change a text

1. Find the text in `bageo-call`, in `crates/agent/data/prompts/<language>.json`, and note its key. The languages are `zh-TW`, `en`, `ja`, `ko`, `es`, `fr`, `de` and `pt`. Simplified Chinese follows `zh-TW`.
2. Create or edit `prompts/<language>.json` here with only the texts you change:

   ```json
   {
     "format": 1,
     "lang": "en",
     "texts": {
       "ack_line": "The new wording of this text."
     }
   }
   ```

   A text is one string, or a list of lines.
3. Open a pull request. The check tells you in plain words what is wrong, if anything.
4. After it is merged, a maintainer pushes a release tag (`vYYYYMMDDNN`).

To go back to the built-in words, delete the text from the file and release again.

## Rules the check applies

- The key must be one Bageo has, in that language.
- Keep every `{placeholder}` of the built-in text, and add none.
- Keep the same spaces and line breaks at the start and the end.
- At most twice the length of the built-in text, or 400 characters more.
- No control, direction or invisible characters.
- Locked texts cannot be changed here. They are the rules Bageo always keeps, such as not giving out personal data and admitting to being an AI when seriously asked; only a new Bageo changes them. They are listed under `"locked"` in the built-in file.

Say the situation, the direction and the limits; do not script lines for the AI to recite. Write for every caller: no real names, phone numbers or addresses.
