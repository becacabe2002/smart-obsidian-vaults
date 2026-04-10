# Obsidian CLI Reference

## Usage
`obsidian <command> [options]`

## Options
- `vault=<name>`: Target a specific vault by name.

## Notes
- `file` resolves by name (like wikilinks), `path` is exact (`folder/note.md`).
- Most commands default to the active file when `file`/`path` is omitted.
- Quote values with spaces: `name="My Note"`.
- Use `\n` for newline, `\t` for tab in content values.

## Commands

### create
Create a new file.
- `name=<name>`: File name.
- `path=<path>`: File path.
- `content=<text>`: Initial content.
- `template=<name>`: Template to use.
- `overwrite`: Overwrite if file exists.
- `open`: Open file after creating.
- `newtab`: Open in new tab.

### append
Append content to a file.
- `file=<name>`: File name.
- `path=<path>`: File path.
- `content=<text>`: Content to append (required).
- `inline`: Append without newline.

### prepend
Prepend content to a file. (Note: listed under `daily:prepend` but standard `prepend` might exist or be implied by `daily`). 
*Self-correction: Looking at the help output, there is no top-level `prepend`, only `daily:prepend`.*

### move
Move or rename a file.
- `file=<name>`: File name.
- `path=<path>`: File path.
- `to=<path>`: Destination folder or path (required).

### delete
Delete a file.
- `file=<name>`: File name.
- `path=<path>`: File path.
- `permanent`: Skip trash, delete permanently.

### open
Open a file.
- `file=<name>`: File name.
- `path=<path>`: File path.
- `newtab`: Open in new tab.

### daily
Open daily note.
- `paneType=tab|split|window`: Pane type to open in.

### search
Search the vault (Note: command not fully listed in previous help snippet but common).

### links
List outgoing links from a file.
- `file=<name>`: File name.
- `path=<path>`: File path.
- `total`: Return link count.

### backlinks
List backlinks to a file.
- `file=<name>`: Target file name.
- `path=<path>`: Target file path.

### files
List files in the vault.
- `folder=<path>`: Filter by folder.
- `ext=<extension>`: Filter by extension.

### folders
List folders in the vault.
- `folder=<path>`: Filter by parent folder.

*(Full list of commands available in the CLI help output)*
