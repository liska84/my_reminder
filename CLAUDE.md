# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-page grocery list web app hosted on GitHub Pages at https://liska84.github.io/my_reminder/. No build step, no backend, no dependencies — just one `index.html` file with inline CSS and JS.

## Development

Open `index.html` directly in a browser for local testing. No server required.

To deploy: push to `main` — GitHub Pages auto-deploys from the root of the `main` branch.

## Architecture

Everything lives in `index.html`:
- **Storage**: localStorage (`grocery-items` key) — array of `{name: string, checked: boolean}`
- **Sharing**: Items encoded into URL query param `?list=item1|item2|...`, shared via QR code (api.qrserver.com) or mailto link
- **URL loading**: On page load, `?list=` param overwrites localStorage and is stripped from the URL

## Security Constraints

- Content-Security-Policy restricts scripts to inline only, images to `api.qrserver.com` only
- All user input is escaped via `textContent` assignment (not innerHTML with raw strings)
- Item names capped at 100 chars, list capped at 200 items
- Array index access is bounds-checked
- URL param decoding is wrapped in try-catch
- localStorage parsing validates structure before use

## macOS Dock App

`GroceryList.app/` is a minimal macOS app bundle that opens the GitHub Pages URL in the default browser. It's a shell script wrapper, not a compiled binary.
