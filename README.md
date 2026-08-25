# HOMEWORX-Notices

The notices feed every H@MEWORX install polls.

`homeworx.json` is the feed index. Each entry points at a notice body in
`notices/`, and carries that body's SHA-256 so the fetching install can
verify it received what was published.

This repository is content, not code — it holds announcements shown inside
H@MEWORX under **About → Notices**. The software itself lives in
[HOMEWORX-Shell](https://github.com/AlderpenGhub/HOMEWORX-Shell).

## Naming

Notices are named **date first**:

    notices/2026-08-24-first-public-release.html

Chronological in any file listing, the date is readable without opening
anything, and there is no bookkeeping. (Sequence numbers need you to know
the last one used; version numbers only work when a notice corresponds to a
release, and most do not.)

If a second notice lands on the same date, suffix it: `-2`.

Editing an existing notice keeps its id and filename — it is still the same
notice. Only its `partial_sha256` changes.

## Publishing a notice

1. Write the body as `notices/YYYY-MM-DD-short-topic.html`
2. Compute its SHA-256 and save it as `notices/<id>.sha256`
3. Add an entry to the `notices` array in `homeworx.json`, with the same
   value in `partial_sha256`

The hash is not optional: the shell verifies the fetched body against it and
will not render a notice whose content does not match.

The body is sanitized by the shell before rendering — only a small tag
allowlist survives (see `_PARTIAL_ALLOWED_TAGS` in the shell's
`database.py`).

## This repository must stay public

Every install fetches this feed without credentials. If it is private, the
notices feature silently degrades for everyone.

## License and disclaimer

Released under the MIT License — see [LICENSE.txt](LICENSE.txt).

[DISCLAIMER.txt](DISCLAIMER.txt) covers no warranty, no support, assumption
of risk and liability, and limitation of liability.

---

Copyright (c) 2026 Alderpen Media, Inc.
