# Self-hosted fonts

| Folder                   | Face                  | Role                       | Package                                      |
| ------------------------ | --------------------- | -------------------------- | -------------------------------------------- |
| `source-sans-3/`         | Source Sans 3         | text + headings            | `@fontsource-variable/source-sans-3`         |
| `source-code-pro/`       | Source Code Pro       | mono (keys, notation)      | `@fontsource-variable/source-code-pro`       |
| `noto-sans-thai-looped/` | Noto Sans Thai Looped | Thai glyphs, `th` pages    | `@fontsource-variable/noto-sans-thai-looped` |
| `noto-sans-jp/`          | Noto Sans JP          | Japanese glyphs, `ja` pages| `@fontsource-variable/noto-sans-jp`          |
| `noto-sans-sc/`          | Noto Sans SC          | Chinese glyphs, `zh` pages | `@fontsource-variable/noto-sans-sc`          |

Everything in this folder but this README is **generated and git-ignored**:
`npm install` (via `prepare`) and `npm run build` run `scripts/fonts.mjs`, which
copies the needed woff2 files out of the pinned packages in `package.json` and,
for the two CJK families, rewrites their sliced `index.css` (plain family names,
`format('woff2')`). Bumping a font is bumping its package version.

Where each face is declared and used:

- `src/lib/styles/fonts.css` — hand-written `@font-face` for Source Sans 3,
  Source Code Pro and the Thai face (subset order is load-bearing there;
  `fonts.spec.ts` guards it).
- `src/lib/chrome/LocaleFonts.svelte` — links `/fonts/noto-sans-{jp,sc}/index.css`
  only on pages whose locale needs them.
- `src/lib/styles/props.css` — the `--font-sans` / `--font-display` /
  `--font-mono` stacks and their `:lang(ja|zh|th)` extensions. Source Sans 3
  stays first in every stack: the Latin of Noto Sans CJK *is* Source Sans, so
  digits and Latin words render identically in all five languages.
- `src/app.html` — preloads the Latin file of Source Sans 3.

All faces: SIL Open Font License 1.1 (`LICENSE` in each folder).
