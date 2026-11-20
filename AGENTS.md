# weirdnet-text agents

The collective `AGENTS.md` in `WeirdBrains/weirdnet-agents` is mandatory and wins on conflict.

- No toolkit dependencies (no GPUI, no platform crates): only editing rules that can be tested headless. Widgets stay in the apps.
- Offsets are UTF-8 byte offsets on grapheme boundaries; keep the UTF-16 helpers exact for input methods.
- Build outside the source checkout, with `CARGO_TARGET_DIR` on a scratch disk; clean targets afterwards.
