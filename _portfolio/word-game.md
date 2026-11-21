---
title: Word cards
summary: Simple phonics flashcards for early readers. Just the word, big and clear, with no ads, accounts or app to install.
img: /assets/img/portfolio/word-game.png
link: https://forkthis.co.uk/word-game/
order: 6
date: 2026-11-21
tags: [Kids, JavaScript, Fun]
---

Most reading apps for small children are cluttered with adverts, rewards and upsells. This
is the opposite: one page that shows one word at a time, big enough to read from across
the table. Tap the card for the next word.

## What it does

- **Phonics word sets.** Three-letter words grouped by short vowel (*cat*, *bed*, *pig*,
  *dog*, *bug*), plus *sh*, *ch* and *th* words and four-letter blends like *frog* and *jump*.
  Every word was checked to be suitable for a four-year-old.
- **Vowel colouring.** An optional switch colours the vowels, to help find the middle sound.
- **Say it aloud.** A speaker button reads the word using the browser's built-in speech, so
  a child can check their answer. It only speaks when asked, so they get to try first.
- **No repeats.** Words are shuffled and each one appears once before the deck reshuffles.

## How it works

A single HTML file with no dependencies beyond a web font
([Andika](https://software.sil.org/andika/), designed for beginning readers, with the
single-storey *a* and *g* that children learn to write). Speech uses the Web Speech API,
so it works offline and nothing leaves the device. It's published to GitHub Pages by a
small Actions workflow whenever the page changes.
