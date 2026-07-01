# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the personal academic website for Kristian S. Blickle (economist, Federal Reserve Bank of New York), served via GitHub Pages at the custom domain `kristianblickle.net` (see `CNAME`). There is no build system, package manager, or test suite — the entire site is a single static HTML file plus image assets.

## Architecture

- `index.html` — the entire site. All markup, CSS (in a `<style>` block), and JS (in a `<script>` block) live in this one file. There are no other `.html`, `.css`, or `.js` files.
- The site is a client-side "SPA": all pages (`About`, `Research`, `Teaching`, `Syndicated Loans`, `Policy & Press`, `Contact`) are `<div class="page" id="page-...">` blocks that all exist in the DOM at once. Navigation via `showPage(name)` toggles the `.active` class to show/hide the matching `#page-<name>` div and highlight the matching `#nav-<name>` button — there is no routing/history API, no page reload.
- Research entries are hand-written `<li class="paper-item">` blocks (see the `Research` page) each with a title/link, coauthors, an abstract (`toggleAbstract()` expands/collapses it), links, and an optional key-figure image. Clicking a figure opens a shared lightbox (`openLightbox()` / `closeLightbox()`) that displays the image full-size with a caption.
- Images referenced by the Research page (`*.png`, `blickle_forest.jpg`) live at the repo root alongside `index.html` and are referenced with plain relative paths.
- Email addresses are Cloudflare-obfuscated (`__cf_email__` / `/cdn-cgi/l/email-protection#...`) — this decoding is normally injected by Cloudflare's edge when the domain is proxied through it; it will not auto-decode when viewing the raw file or from an unproxied host.

## Working in this repo

- There's no local dev server, bundler, or linter — edit `index.html` directly and open it in a browser to preview.
- To add a new paper/publication, working paper, or policy post: copy an existing `<li class="paper-item">` (Research) or `<li class="policy-item">` (Policy & Press) block and adjust the content, keeping `id` attributes (e.g. `abs-wp7`, `abs-pub12`) unique since `toggleAbstract()` looks elements up by id.
- Deployment is implicit: commits pushed to `main` are published directly by GitHub Pages, so changes to `index.html` go live as soon as they land on `main`.
