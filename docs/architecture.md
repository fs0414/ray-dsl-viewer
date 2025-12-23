# DSL Viewer Architecture

## Overview

DSL Viewer is a Raycast extension that provides instant preview for Markdown and Mermaid diagrams.

## Component Architecture

```mermaid
graph TB
    subgraph Raycast Extension
        Command[Command<br/>Main Entry Point]
        Form[Form Component<br/>Input UI]
        PreviewDetail[PreviewDetail<br/>Preview UI]
    end

    subgraph Core Functions
        detectContentType[detectContentType<br/>Auto Detection]
        mermaidToImageUrl[mermaidToImageUrl<br/>URL Generator]
    end

    subgraph External Services
        MermaidInk[mermaid.ink API<br/>SVG/PNG Rendering]
    end

    Command --> Form
    Form -->|Submit| PreviewDetail
    Form -->|onChange| detectContentType
    PreviewDetail -->|Mermaid| mermaidToImageUrl
    mermaidToImageUrl -->|Base64 Encoded| MermaidInk
    MermaidInk -->|Image| PreviewDetail
```

## User Flow

```mermaid
flowchart LR
    A[Open Extension] --> B{Input Content}
    B --> C[Auto Detect Type]
    C --> D{Type Match?}
    D -->|Yes| E[Preview]
    D -->|No| F[Show Warning]
    F --> G{Switch Type?}
    G -->|Yes| E
    G -->|No| E
    E --> H[View Result]
    H --> I{Action}
    I -->|Back| B
    I -->|Copy| J[Clipboard]
```

## Data Flow

```mermaid
sequenceDiagram
    participant U as User
    participant F as Form
    participant D as Detector
    participant P as Preview
    participant M as mermaid.ink

    U->>F: Input Content
    F->>D: detectContentType()
    D-->>F: markdown | mermaid
    U->>F: Submit
    F->>P: Push PreviewDetail

    alt Mermaid
        P->>M: Base64 encoded request
        M-->>P: PNG Image
    else Markdown
        P->>P: Render directly
    end

    P-->>U: Display Result
```

## Module Structure

```mermaid
graph LR
    subgraph dsl-viewer.tsx
        A[Types] --> B[Constants]
        B --> C[Utility Functions]
        C --> D[Components]
        D --> E[Export Command]
    end

    A --- A1[ContentType]
    B --- B1[MERMAID_KEYWORDS]
    C --- C1[detectContentType]
    C --- C2[mermaidToImageUrl]
    D --- D1[PreviewDetail]
    D --- D2[Command]
```

## Key Features

| Feature | Description |
|---------|-------------|
| Auto Detection | Automatically detects Markdown vs Mermaid from content |
| Dark Theme | Custom dark theme optimized for Raycast |
| Clipboard Integration | Paste from clipboard with `Cmd+Shift+V` |
| Type Mismatch Warning | Warns when selected type doesn't match detected type |

## Tech Stack

- **Runtime**: Raycast Extension (React)
- **Language**: TypeScript
- **Mermaid Rendering**: mermaid.ink (External API)
- **State Management**: React useState/useEffect
