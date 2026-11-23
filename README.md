# news-image-20261123 — World News in One Image

[![make.fun bounty](https://img.shields.io/badge/make.fun-news--image--20261123-blue)](https://make.fun/bounty/news-image-20261123)

A single 1024x1024 newspaper front page summing up 23 November 2026:
COP31 collapses with no deal, two tankers hit in the Strait of Hormuz,
Democrats win 258 House seats, Mexico captures El Chapo Isidro, and WHO
pleads for peace in Ebola-hit DR Congo.

## How it works

`main.py` is Python 3.13 standard library only (no external packages, no
network). It draws the front page with a hand-built 5x7 bitmap font and a
hand-written PNG encoder (zlib + struct), then writes `entry.png`.

## Run

```sh
python3 main.py
# writes entry.png next to main.py, or to $MAKEFUN_OUTPUT_DIR if set:
MAKEFUN_OUTPUT_DIR=/tmp/out python3 main.py
```

## Test

```sh
MAKEFUN_OUTPUT_DIR=/tmp/out1 python3 main.py
MAKEFUN_OUTPUT_DIR=/tmp/out2 python3 main.py
sha256sum /tmp/out1/entry.png /tmp/out2/entry.png  # must be identical
```

The image is deterministic: two runs produce byte-identical output
(16,253 bytes, 1024x1024, well under the 1 MiB limit).

## Verified 23 Nov 2026

- Two runs into separate output dirs: sha256
  `827ca1bd3e2472da3642ab3227f9dddd84acca80d40bbe1c90c5606450c60f91`
  on both — byte-identical.
- PNG signature valid, dimensions 1024x1024, 16,253 bytes (limit 1,048,576).
- Pixel check: every headline and fact line sits inside its expected band
  (masthead 132–891, lead headline 280–902, all facts within their rows),
  lead headline is red, zero ink in the gaps between rows, no text clipped
  at the right edge.
- Design choice: fact lines are printed in black, not grey — at ~300px the
  grey 3-scale text lost contrast; the spec demands high contrast.

## Facts

Every number and claim on the image comes from the prose spec, verified
against primary sources (Reuters, AP, NBC, Al Jazeera, AFP) on 23 Nov 2026.
No extra numbers were added.
