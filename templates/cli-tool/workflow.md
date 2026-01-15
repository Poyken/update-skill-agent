# CLI Tool Development Workflow

## 🎯 Purpose

Step-by-step workflow for building CLI tools with AI assistance.

---

## Phase 1: Design

### Step 1.1: Command Structure

```
Prompt:
"Design CLI command structure for [tool name]:

Purpose: [what the tool does]

Commands needed:
- [command 1]: [description]
- [command 2]: [description]

For each command, define:
- Subcommands (if any)
- Options/flags
- Arguments
- Example usage

Follow Unix CLI conventions."
```

### Step 1.2: User Experience

```
Prompt:
"Design the UX for this CLI:

[paste command structure]

Consider:
- Help text format
- Error messages
- Progress indicators
- Color coding
- Interactive prompts vs flags

Provide examples for each."
```

---

## Phase 2: Setup

### Step 2.1: Project Setup

```
Prompt:
"Set up a Node.js CLI project:

Requirements:
- TypeScript
- Commander.js (or yargs)
- Chalk for colors
- Ora for spinners

Provide:
1. Package.json setup
2. TypeScript config
3. Build config
4. npm link setup for development"
```

### Step 2.2: Base Structure

```
Prompt:
"Create the base CLI structure:

Commands: [list commands]

Setup:
- Entry point with Commander
- Command registration
- Global options (--verbose, --help)
- Error handling wrapper"
```

---

## Phase 3: Implementation

### Command Template

```
Prompt:
"Implement CLI command: [command name]

function [commandName]([args]) {
  // ...
}

Features:
- [feature 1]
- [feature 2]

Include:
- Argument parsing
- Validation
- Progress indicator
- Error handling
- Success/failure output"
```

### Interactive Prompts

```
Prompt:
"Add interactive prompts to [command]:

Questions:
1. [question 1] - type: [text/select/confirm]
2. [question 2] - type: [text/select/confirm]

Use Inquirer.js.
Include validation.
Allow skip with --yes flag."
```

---

## Phase 4: Polish

### Help & Documentation

```
Prompt:
"Generate help text for CLI:

[paste command structure]

Include:
- Command descriptions
- Option details
- Usage examples
- Version info"
```

### Error Handling

```
Prompt:
"Improve error handling for CLI:

Common errors:
- Missing arguments
- Invalid options
- File not found
- Network errors

Provide user-friendly messages with suggestions."
```

---

## Quick Reference

| Phase  | Focus                       |
| ------ | --------------------------- |
| Design | Commands → Options → UX     |
| Setup  | Project → Structure → Entry |
| Build  | Commands → Prompts → Logic  |
| Polish | Help → Errors → Testing     |
