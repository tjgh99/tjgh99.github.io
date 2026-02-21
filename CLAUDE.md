# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website for **No Sweat Soles**, a student-run shoe deodorizer business based in Minnesota. No build tools, frameworks, or package managers — just HTML, CSS, and vanilla JS.

## Previewing the Site

Open `index.html` directly in a browser. No server or build step is required.

## Architecture

`index.html` is a single-page app (SPA) without any routing library. All five sections (Home, About, Products, Preorder Status, Contact) exist in the DOM at once. JavaScript in `index.html` hides inactive sections by toggling the `.active` CSS class, which uses `opacity`/`height`/`overflow` to show/hide content with a transition. Only one section is visible at a time.

`style.css` handles all styling, including the `.active` / `:not(.active)` section visibility logic.

## Payments

All "Preorder Now" buttons in `index.html` link to a Stripe-hosted payment page. Do not replace this with a custom card form.

## Important: `preorder.html`

This file is an **unused draft** — it is not linked from `index.html`'s navigation. It contains a raw HTML form that collects credit card numbers, expiration dates, and CVCs, which is a PCI DSS violation. The form currently only fires a demo `alert()` and submits nothing. Do not wire this form up to any backend or payment processor; use the Stripe link approach in `index.html` instead.

## Known HTML Issues

- Both "Preorder Now" buttons in `index.html` share `id="stripe-link"`, which is invalid (IDs must be unique). Use classes instead if JS targeting is needed.
- `favicon.html` is not a real page — it is just a code snippet. The actual favicon reference (`nosweatsoles-favicon.png`) is declared inside `index.html` and `preorder.html`, but the image file is not present in the repo.
