# Off the Clock

*What I listen to, watch and read when I'm not working, with my Spotify wired in live.*

**Live:** https://suhxnitiwari.github.io/off-the-clock/

## What it is

A personal taste page in three parts:

- **Listen:** my live Spotify listening, drawn as a music universe of my top artists, Listening DNA by genre, a listening clock, On Repeat, and what I'm playing right now.
- **Watch:** the shows I rewatch on repeat, rom-coms, the Desi edit, comedy, and 26 TED talks sorted by topic that play in a pop-up.
- **Read:** the books behind the business, the ones I'll never shut up about, and the ones that changed how I live.

It ends on "So apparently, I have a type." and a closing line for anyone who scrolled that far: "Still here? You must like me."

## How it's built

- **Live data without exposing keys.** The music section reads from my main site, [suhanitiwari.com](https://suhanitiwari.com), which keeps my Spotify login private on its server and lets only this site read its `/spotify` and `/music` answers. Each section fills in as soon as its own data arrives, and fresh responses are cached per tab in `sessionStorage`.
- **A packed bubble universe.** My top 20 artists are laid out with a small physics simulation: #1 sits at the center, #2 to #5 start from four directions, #6 to #10 in the gaps, and the rest spread out on the golden angle. Then 400 steps of decaying gravity pull everything inward while pairwise collision passes push overlaps apart, with the smaller bubble moving more. A seeded random number generator keeps the "organic" layout identical on every visit, and bubble sizes are deliberately nonlinear so the top five can be ranked by size alone.
- **Semantic zoom and real input handling.** The universe pans and zooms with mouse, trackpad pinch and touch. What each bubble shows depends on its size on screen, label text is sized in screen pixels so it stays readable at any zoom, the scroll wheel only zooms once you've clicked in (so it never hijacks page scroll), double-click flies to an artist, and bubbles are keyboard-selectable.
- **A real-time player.** The now-playing pin is modeled on Spotify's own screen: the progress bar advances in real time from the moment the server asked Spotify, and when the song ends it asks again.
- **An honest listening clock.** A 12-hour dial with an AM/PM switch and one wedge per hour, built from Spotify's last 50 plays. It states how far back those plays actually reach so it never claims more than it has, and arrow keys walk it an hour at a time.
- **Listening DNA** is an interactive donut of genre share whose palette was checked with a colorblind validator in ring order against the page background.
- **Music extras computed in the browser** from one API call ([`js/music-lab.js`](js/music-lab.js)): albums I can't leave, the oldest songs I still play, and a word cloud of my song titles with a family-friendly filter.
- **Shelves that behave like a streaming app** ([`js/shelves.js`](js/shelves.js)): click-and-drag scrolling that snaps to the nearest cover, a guard so a drag never opens a card, arrow keys, "See all," and topic filters. Talks open in a `<dialog>` with a privacy-enhanced YouTube embed that's removed on close so audio stops.
- **A custom cursor that survives the top layer** ([`js/sparkle.js`](js/sparkle.js)): a gold sparkle drawn in its own layer because macOS swaps cursor images for a plain arrow at speed. That layer is a popover, so a `MutationObserver` re-raises it above any modal that opens. Glitter sheds faster the faster you move, and it all switches off for touch screens and reduced motion.

## Design choices

- The song-title word cloud gives every word its own font picked for its meaning: "love" in a romantic script, "run" in a racing face, "drop" in a dripping-paint font, "time" like a digital clock, "down" set slightly below the line. Words without a match borrow from their mood (love, angry, sad, move, dream), and no font is used twice.
- The music universe borrows the Apple Watch app grid, so a personal ranking reads at a glance as size.
- Clicking a bubble fills an artist card with genres, hometown and a short bio, and occasional one-time "snoop" remarks reward exploring.
- Diagrams play themselves when they're on screen ([`js/autoplay.js`](js/autoplay.js)), pause for 10 seconds when you interact, and stay still for reduced motion or a background tab.
- The copy has a voice: the "View more" button collapses with "Okayyy Suhani, I've seen enough of your 'taste'."

## Tech stack

HTML, CSS, vanilla JavaScript, SVG, Spotify Web API (through my site's server), iTunes Search API previews, YouTube embeds, GitHub Pages.

This page used to live at suhanitiwari.com/home/favorites, and that address now sends you here.

© 2026 Suhani Tiwari. All rights reserved.

Built by [Suhani Tiwari](https://suhanitiwari.com).
