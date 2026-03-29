# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal knowledge base managed as an **Obsidian vault**. It contains technical cheatsheets and platform-specific notes in Markdown format. There is no build system, test suite, or linting — it is a collection of static markdown files.

## Structure

- `Cheatsheet/` — Language and tool quick-reference guides (JS, Git, Docker, CSS, React, etc.)
- `Platform/` — OS and platform-specific notes (Arch Linux, macOS, Apple, GitHub, etc.)
- `.obsidian/` — Obsidian vault configuration (plugins, appearance, hotkeys)

## Conventions

- Obsidian-flavored Markdown: internal links use `[[File Name]]` syntax
- Code blocks use [Prism-supported language identifiers](https://prismjs.com/#supported-languages)
- Tab size is 3 spaces (configured in `.obsidian/app.json`)
- Version control is automated via the `obsidian-git` community plugin; automated commits use the message format `vault backup: YYYY-MM-DD HH:MM:SS`

## Installed Obsidian Plugins

Community: `obsidian-git`, `obsidian-languagetool-plugin`, `table-editor-obsidian`
