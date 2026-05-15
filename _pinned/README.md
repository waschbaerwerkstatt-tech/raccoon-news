# Pinned archive entries

Files in `_pinned/archive/` are permanent fixtures that must always be present
in `archive/`, regardless of what the external feed publisher writes.

The `.github/workflows/restore-pinned.yml` workflow runs after every push to
`main` and:

1. Copies any missing/outdated file from `_pinned/archive/` back into
   `archive/`.
2. Inserts each line in `_pinned/index-entries.html` at the top of
   `archive/index.html`'s `<ol class="archive-list">`, if its `href` isn't
   already present.
3. Commits the restored state with the marker `[pinned-restore]`, which the
   workflow itself ignores to avoid an infinite loop.

## To pin a new file

1. Place the file in `_pinned/archive/<name>.html`.
2. Add a `<li>…</li>` line for it to `_pinned/index-entries.html`.
3. Commit. The workflow will sync `archive/` on the next push.

## To unpin (delete permanently)

Remove the file from `_pinned/archive/` and the line from
`_pinned/index-entries.html`. The workflow will not re-create it; the next
publisher push will then drop it from `archive/` for good.
