# weirdnet-text

Toolkit-independent editing rules for text fields, so the behaviour can be tested without a UI
and shared by every Weirdnet app's text inputs (Morph's address bar, Bragi's prompt).

`TextField` holds the text, the selection (and which end of it moves) and any text an input
method has marked while composing. It handles typing and pasting at the caret, Backspace and
Delete by whole grapheme clusters, Left/Right/Home/End with and without Shift, select-all,
inline completions (`append_selected`: the suggestion is selected, so typing replaces it,
Backspace removes it and Right accepts it), input-method composition (`replace_and_mark`) and
UTF-8 ↔ UTF-16 offset conversion for platform input APIs. One-line fields turn line breaks into
spaces; `TextField::multiline()` keeps them (normalising `\r\n` and `\r` to `\n`).

```rust
use weirdnet_text::TextField;

let mut field = TextField::new();
for ch in "git".chars() {
    field.replace(None, &ch.to_string());
}
field.append_selected("hub.com"); // inline completion, selected
field.right();                    // Right accepts it
assert_eq!((field.text(), field.cursor()), ("github.com", 10));

field.select_left();
field.backspace();
assert_eq!(field.text(), "github.co");
```

The widget that draws a field and feeds it keys and input-method events stays in each app's
toolkit layer (GPUI in Morph and Bragi); only these rules are shared.

## Status

0.1.0, extracted unchanged from Morph's `morph-ui` text module. License: BSD-3-Clause.
