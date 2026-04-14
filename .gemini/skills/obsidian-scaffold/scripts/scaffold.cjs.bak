#!/usr/bin/env node

const { execSync } = require('child_process');
const fs = require('fs');

/**
 * Parses a bulleted list into a structured object.
 * Supports nesting with spaces or tabs.
 */
function parseBulletedList(content) {
  const lines = content.split('\n');
  const result = [];
  const stack = [{ level: -1, children: result }];

  for (const line of lines) {
    if (!line.trim()) continue;

    const match = line.match(/^(\s*)([-*+]|\d+\.)\s*(.*)$/);
    if (!match) continue;

    const indent = match[1].length;
    const text = match[3].trim();

    let level = indent;
    // Basic indentation level calculation (4 spaces per level)
    // Adjust if needed for specific indent styles
    level = Math.floor(indent / 2); // Assuming 2 spaces or tabs

    const node = { text, children: [] };

    while (stack.length > 1 && stack[stack.length - 1].level >= level) {
      stack.pop();
    }

    stack[stack.length - 1].children.push(node);
    stack.push({ level, children: node.children });
  }

  return result;
}

/**
 * Recursively creates folders and files based on the parsed structure.
 */
function scaffold(nodes, parentPath = '') {
  for (const node of nodes) {
    const currentPath = parentPath ? `${parentPath}/${node.text}` : node.text;
    
    // If it has children, it's a topic/subtopic
    if (node.children.length > 0) {
      scaffold(node.children, currentPath);
    } else {
      // It's a leaf node, create Topic/Subtopic/index.md
      const indexPath = `${currentPath}/index.md`;
      const title = node.text;
      const content = `# ${title}`;
      
      try {
        console.log(`Creating: ${indexPath}`);
        // Use obsidian CLI to create the file
        // Ensure content is properly quoted for shell execution
        const escapedContent = content.replace(/"/g, '\\"').replace(/\n/g, '\\n');
        execSync(`obsidian create path="${indexPath}" content="${escapedContent}"`, { stdio: 'inherit' });
      } catch (error) {
        console.error(`Error creating ${indexPath}:`, error.message);
      }
    }
  }
}

// Read from stdin or file
let inputContent = '';
if (process.argv[2]) {
  inputContent = fs.readFileSync(process.argv[2], 'utf8');
} else {
  inputContent = fs.readFileSync(0, 'utf8'); // stdin
}

if (!inputContent) {
  console.error('Error: No input provided.');
  process.exit(1);
}

const structure = parseBulletedList(inputContent);
scaffold(structure);
