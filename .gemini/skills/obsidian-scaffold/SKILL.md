---
name: obsidian-scaffold
description: Scaffolds folders, subfolders, and markdown files in Obsidian based on a bulleted list of topics/subtopics. Use when you need to create a structured hierarchy of notes from a set of topics.
---

# Obsidian Scaffold

This skill allows you to quickly create a folder hierarchy and index notes in your Obsidian vault from a bulleted list of topics and subtopics.

## Structure

The skill follows a specific folder/file structure:
- Every subtopic is placed in its own folder.
- An `index.md` file is created inside each subtopic folder.
- The `index.md` file contains a `# Subtopic Name` heading as its content.

Example:
If you provide:
- Programming
  - JavaScript
  - Python

It will create:
- `Programming/JavaScript/index.md`
- `Programming/Python/index.md`

## Usage

Provide a bulleted list of topics and subtopics. The indentation determines the hierarchy.

1. Prepare your bulleted list.
2. The skill uses the `scripts/scaffold.cjs` script to parse the list and call the `obsidian` CLI.

### Trigger Phrases

- "scaffold my obsidian vault with these topics"
- "create a topic structure in obsidian"
- "build out folders and notes for these subtopics"

## Under the Hood

The skill uses the `obsidian` CLI's `create` command to perform the operations. It assumes the `obsidian` CLI is available in the environment path.

A detailed reference for the `obsidian` CLI is available in `references/obsidian-cli.md`. Agents should refer to this file instead of running `obsidian --help` to save time and context.
