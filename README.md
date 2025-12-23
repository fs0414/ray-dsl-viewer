# Ray DSL Viewer

Preview Markdown and Mermaid diagrams instantly from your clipboard or files.

## Features

- **Markdown Preview**: Render Markdown content with full formatting support
- **Mermaid Diagram Support**: Visualize flowcharts, sequence diagrams, ER diagrams, and more
- **Auto Detection**: Automatically detects content type (Markdown or Mermaid)
- **Clipboard Integration**: Paste content directly from your clipboard with `Cmd+Shift+V`
- **Dark Theme**: Mermaid diagrams are rendered with a beautiful dark theme

## Supported Mermaid Diagrams

- Flowchart / Graph
- Sequence Diagram
- Class Diagram
- State Diagram
- ER Diagram
- User Journey
- Gantt Chart
- Pie Chart
- Mindmap
- Timeline
- Git Graph
- C4 Diagrams
- Requirement Diagram

## Usage

1. Open the extension in Raycast
2. Select content type (Markdown or Mermaid) - auto-detected when pasting
3. Enter or paste your content
4. Press Enter to preview

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Enter` | Preview content |
| `Cmd+Shift+V` | Paste from clipboard |
| `Cmd+T` | Switch to detected content type |

## Examples

### Markdown with Embedded Mermaid

```markdown
# My Document

Here's a flowchart:

\`\`\`mermaid
graph TD
    A[Start] --> B[Process]
    B --> C[End]
\`\`\`
```

### Pure Mermaid

```
graph TD
    A[Start] --> B{Decision}
    B -->|Yes| C[Action 1]
    B -->|No| D[Action 2]
```

## Installation

```bash
# Clone the repository
git clone https://github.com/fujitanisora0414/ray-dsl-viewer.git

# Install dependencies
npm install

# Start development
npm run dev
```

## License

MIT
