# Gender Neutral Language Recognizer

Finds predefined gender-specific words and phrases in a `.txt` file and suggests gender-neutral alternatives.
Built for the Automata and Language Theory machine problem. Recognition uses **regular expressions**.

## How to run

No installation needed.

1. Open `index.html` in any modern browser (Chrome, Edge, Firefox).
2. Click **Choose a file** and select a `.txt` file (try `sample.txt`).
3. Read the results table (term, occurrences, suggested alternative). Matches are highlighted in the text below it.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole application (HTML, CSS, JavaScript) |
| `sample.txt` | Sample document containing many listed terms |
| `tests/repeated.txt` | Same term repeated with different capitalization |
| `tests/no_terms.txt` | No listed terms; contains "the", "them", "whole" to check `he` is not matched |
| `tests/empty.txt` | Empty file |
| `tests/unsupported.pdf` | Unsupported format |

## The regular expression

The pattern is built from the term list in `buildRecognizer()`:

```
(?<![A-Za-z0-9_])(chairman|policeman|fireman|...|he\s+or\s+she|...)(?![A-Za-z0-9_])   flags: g, i
```

- `i` flag: ignores capitalization (`Chairman`, `CHAIRMAN`).
- `(?<![A-Za-z0-9_])` and `(?![A-Za-z0-9_])`: the match must not touch another letter, digit or underscore, so whole words only. This is why `he` inside `the` is never matched.
- `\s+` in place of spaces: phrases like `he or she` still match across extra spaces or line breaks.
- Terms are sorted longest-first and regex special characters (such as the `-` in `man-made`) are escaped.
- `g` flag: every occurrence is found and counted.

## Messages

- Unsupported extension: "Unsupported file format. Please choose a .txt file."
- Empty or whitespace-only file: "The file is empty. Please choose a file that contains text."
- Readable text with no matches: "No predefined gender-specific terms were detected."

Suggestions are for review only; nothing is replaced automatically.
