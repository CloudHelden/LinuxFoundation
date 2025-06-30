# Mermaid Diagram Guide for Linux 101

## Overview
This guide helps instructors and students create visual diagrams using Mermaid syntax. All diagrams render automatically in GitHub, GitLab, and many Markdown viewers.

## Quick Reference

### 1. Process Flow Diagrams

```mermaid
graph LR
    A[User Input] --> B{Valid?}
    B -->|Yes| C[Process]
    B -->|No| D[Error]
    C --> E[Output]
    D --> A
```

**Use for**: Command flows, decision trees, troubleshooting guides

### 2. System Architecture

```mermaid
graph TB
    subgraph "Application Layer"
        A1[Web Server]
        A2[App Server]
        A3[Cache]
    end
    
    subgraph "Data Layer"
        D1[(Database)]
        D2[File Storage]
    end
    
    A1 --> A2
    A2 --> A3
    A2 --> D1
    A3 --> D1
    A1 --> D2
```

**Use for**: System components, network topology, service relationships

### 3. Sequence Diagrams

```mermaid
sequenceDiagram
    participant U as User
    participant S as Shell
    participant K as Kernel
    participant H as Hardware
    
    U->>S: Type command
    S->>K: System call
    K->>H: Hardware request
    H-->>K: Response
    K-->>S: Result
    S-->>U: Output
```

**Use for**: System calls, network protocols, process communication

### 4. State Diagrams

```mermaid
stateDiagram-v2
    [*] --> Running
    Running --> Sleeping: wait()
    Running --> Stopped: SIGSTOP
    Sleeping --> Running: wake up
    Stopped --> Running: SIGCONT
    Running --> Zombie: exit()
    Zombie --> [*]: parent wait()
```

**Use for**: Process states, service lifecycle, file states

### 5. Git Workflows

```mermaid
gitGraph
    commit
    branch feature
    checkout feature
    commit
    commit
    checkout main
    merge feature
    commit
```

**Use for**: Version control, branching strategies, deployment flows

### 6. Entity Relationships

```mermaid
erDiagram
    USER ||--o{ PROCESS : owns
    PROCESS ||--o{ FILE : accesses
    USER ||--o{ GROUP : belongs_to
    GROUP ||--o{ FILE : owns
    
    USER {
        int uid
        string username
        string home_dir
    }
    PROCESS {
        int pid
        int uid
        string command
    }
    FILE {
        string path
        int permissions
        int uid
        int gid
    }
    GROUP {
        int gid
        string groupname
    }
```

**Use for**: Permission models, database schemas, system relationships

### 7. Gantt Charts (for Course Planning)

```mermaid
gantt
    title Linux 101 Course Timeline
    dateFormat  YYYY-MM-DD
    section Month 1
    Foundations     :2024-01-01, 14d
    File System     :14d
    section Month 2  
    Administration  :28d
    section Month 3
    Automation      :21d
    Final Project   :7d
```

**Use for**: Course timeline, project planning, lab schedules

### 8. Pie Charts (for Resource Usage)

```mermaid
pie title Disk Usage
    "System" : 15
    "Applications" : 25
    "User Data" : 45
    "Free Space" : 15
```

**Use for**: Resource distribution, time allocation, survey results

## Best Practices

### 1. Keep It Simple
```mermaid
graph LR
    A[Input] --> B[Process] --> C[Output]
```

### 2. Use Clear Labels
```mermaid
graph TD
    A[User runs: ls -la] --> B{Files exist?}
    B -->|Yes| C[Display file list]
    B -->|No| D[Show empty directory]
```

### 3. Color Coding for Emphasis
```mermaid
graph TD
    A[Normal Process] --> B[Warning Process]
    B --> C[Critical Process]
    
    style B fill:#ff9,stroke:#333,stroke-width:2px
    style C fill:#f99,stroke:#333,stroke-width:4px
```

### 4. Group Related Items
```mermaid
graph TB
    subgraph "User Commands"
        A[ls]
        B[cd]
        C[pwd]
    end
    
    subgraph "Admin Commands"
        D[sudo]
        E[chmod]
        F[chown]
    end
    
    A --> G[File System]
    D --> G
```

## Common Diagrams for Linux Teaching

### Permission Flow
```mermaid
graph TD
    A[User requests file access] --> B{User owns file?}
    B -->|Yes| C{Check user permissions}
    B -->|No| D{User in file's group?}
    D -->|Yes| E{Check group permissions}
    D -->|No| F{Check other permissions}
    
    C -->|Read| G[Allow read]
    C -->|Write| H[Allow write]
    C -->|Execute| I[Allow execute]
    C -->|None| J[Deny access]
    
    E -->|Has permission| K[Allow action]
    E -->|No permission| J
    
    F -->|Has permission| K
    F -->|No permission| J
```

### Boot Process
```mermaid
graph TD
    A[BIOS/UEFI] --> B[Bootloader GRUB]
    B --> C[Kernel Loading]
    C --> D[initramfs]
    D --> E[Init System systemd]
    E --> F[System Services]
    F --> G[Login Prompt]
    G --> H[User Session]
```

### Network Packet Flow
```mermaid
sequenceDiagram
    participant App
    participant Socket
    participant TCP/IP
    participant NIC
    participant Network
    
    App->>Socket: send() data
    Socket->>TCP/IP: Create packet
    TCP/IP->>NIC: Transmit
    NIC->>Network: Physical transmission
    Network-->>NIC: Response
    NIC-->>TCP/IP: Receive packet
    TCP/IP-->>Socket: Process data
    Socket-->>App: recv() data
```

## Integration Tips

### 1. In Markdown Files
Place diagram code in triple backticks with `mermaid` identifier:
````markdown
```mermaid
graph LR
    A --> B
```
````

### 2. For Presentations
- Export as SVG/PNG for slides
- Use live rendering tools
- Keep diagrams on single slides

### 3. Student Exercises
Have students create diagrams for:
- Their understanding of concepts
- Troubleshooting workflows  
- System designs
- Command relationships

## Tools and Resources

### Rendering Tools
- **GitHub/GitLab**: Native support
- **VS Code**: Mermaid extension
- **Online**: https://mermaid.live/
- **CLI**: `mmdc` (mermaid CLI)

### Learning Resources
- [Official Docs](https://mermaid-js.github.io/mermaid/)
- [Live Editor](https://mermaid.live/edit)
- [Examples Gallery](https://mermaid-js.github.io/mermaid/#/examples)

## Exercise: Create Your Own

Try creating a diagram for:
1. How `sudo` works
2. File permission check flow
3. Your daily Linux workflow
4. Network troubleshooting steps

Remember: Diagrams should clarify, not complicate!