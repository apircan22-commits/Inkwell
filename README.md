# Inkwell

A mobile-first web app for searching and printing any Magic: The Gathering card on a thermal receipt printer.

## What it does

- **Search** any card, token, or emblem via the Scryfall API
- **Filter** by type — creature, instant, sorcery, token, emblem, etc.
- **Preview** cards with full art, oracle text, and set info
- **Print** with Floyd-Steinberg dithering tuned for thermal paper
- **Double-faced cards** print each face as a separate job (thermal printers cut off the last page otherwise)
- **Print queue** to batch multiple cards and print them one by one
- **Copies** stepper (1–10) per card

## Setup

No build step. No server. Open `mtg-printer.html` on your phone and connect a Bluetooth thermal printer.

Supports 2″, 3″, and 4″ paper widths. Cards print at real physical MTG card width (63mm) and center on wider paper.

## Usage

1. Open in a mobile browser
2. Pick your paper size
3. Search for a card
4. Tap to preview → hit Print
5. Or add to queue and print all at once

## Tech notes

- Single HTML file, vanilla JS, no dependencies
- Scryfall API with rate limiting (50ms between requests)
- Dithering: Floyd-Steinberg at 504px wide (63mm × 8 dots/mm), gamma 0.82, threshold 120
- Print pipeline uses `@page { margin: 0 0 50mm 0 }` and `page-break-after: always` to feed paper past the cutter
- `image-rendering: pixelated` prevents browser anti-aliasing on dithered output
- Dark/light theme and paper size persist in localStorage
