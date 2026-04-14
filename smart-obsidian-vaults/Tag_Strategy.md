# Tag Strategy for Obsidian

To maintain a consistent and organized vault, we use a shared tagging strategy. The `obsidian-writer` agent should reference this list when creating or editing notes.

## Tag Groups

### Progress Group
These tags represent the lifecycle status of a note. A note should ideally have exactly one of these.
- `#ongoing` (Actively being written/researched)
- `#drafted` (Initial content complete, needs refinement)
- `#need-review` (Content requires technical or structural review)
- `#finished` (Note is complete and stable)

### Domain Group
These tags categorize the content by subject matter. Notes can have multiple domain tags.
- `#ai` (General AI concepts)
- `#machine-learning`
- `#deep-learning`
- `#llm` (Large Language Models)
- `#data-engineering`
- `#mlops`

## Guidelines for Tagging
- **Check for existing tags:** Before applying a new tag, review this file.
- **Avoid Duplication:** If a similar concept is already tagged, use the existing tag.
- **New Tags:** If a note falls outside existing categories, suggest a new tag to the user first.
