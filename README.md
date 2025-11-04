# wk - Git Worktree Manager

A bash-based tool for managing git worktrees with one-word US state names. Automatically rotates through state names alphabetically and handles branch creation/fetching from remote.

## Installation

1. **Make the script executable:**
   ```bash
   chmod +x wk
   ```

2. **Add to your shell profile** (`.bashrc`, `.zshrc`, or equivalent):
   ```bash
   # Add to the end of your shell profile file
   source /path/to/this/repo/wk
   ```

   Replace `/path/to/this/repo` with the actual path to this directory.

3. **Reload your shell:**
   ```bash
   source ~/.bashrc  # or ~/.zshrc, etc.
   ```

## Usage

Navigate to any git repository and run:

```bash
wk
```

This will show an interactive menu with three options:

### 1. Create New Worktree
- Prompts for a branch name
- Automatically assigns the next available state name (alphabetically)
- If the branch exists on `origin`, fetches it
- If not, creates a new local branch
- Automatically changes directory to the new worktree

Example:
```bash
$ wk
=== Git Worktree Manager ===
1) Create new worktree
2) Remove worktree
3) List worktrees

Select option (1-3): 1
Enter branch name to check out: feature/new-ui
Branch 'feature/new-ui' found on remote. Creating worktree from remote branch...
Worktree created at: /path/to/repo/.worktrees/alabama
Worktree state: Alabama
```

### 2. Remove Worktree
- Lists all existing worktrees with their branches
- Prompts you to select which one to remove
- Removes only the worktree (preserves the branch)

```bash
$ wk
=== Git Worktree Manager ===
1) Create new worktree
2) Remove worktree
3) List worktrees

Select option (1-3): 2
Existing worktrees:
1) alabama (branch: feature/new-ui)
2) alaska (branch: bugfix/header)

Select worktree to remove (number): 1
Worktree removed: alabama
```

### 3. List Worktrees
- Shows all active worktrees
- Displays the branch and commit for each
- Shows the next state name that will be used

```bash
$ wk
=== Git Worktree Manager ===
1) Create new worktree
2) Remove worktree
3) List worktrees

Select option (1-3): 3
Existing worktrees:
  alabama              branch: feature/new-ui       commit: a1b2c3d
  alaska               branch: bugfix/header        commit: e4f5g6h

Next state to use: Arizona
```

## Supported State Names

The tool rotates through these 27 one-word US states (alphabetically):

Alabama, Alaska, Arizona, Arkansas, Colorado, Connecticut, Delaware, Florida, Georgia, Hawaii, Idaho, Illinois, Indiana, Iowa, Kansas, Kentucky, Louisiana, Maine, Maryland, Massachusetts, Michigan, Minnesota, Mississippi, Missouri, Montana, Nebraska, Nevada

## How It Works

- **State Tracking**: The next state index is stored in `.worktrees/.wk-state`
- **Worktree Location**: All worktrees are created in `.worktrees/<state-name>/`
- **Branch Handling**:
  - If a remote branch exists with the given name, it's checked out and tracked
  - If not, a new local branch is created
- **Directory Change**: After creating a worktree, you're automatically `cd`'d into it

## Requirements

- Git (with worktree support)
- Bash 4.0+
- A git repository to work in

## Error Handling

- If a state name is already in use, you'll get an error and can try again
- If all 27 state names are exhausted, an error is shown (no wraparound)
- Git repository validation is performed before any operation

## Shell Integration

The script is designed to be sourced, so:
- You can call `wk` from anywhere in your repository
- Directory changes persist in your current shell
- Can be used with aliases or functions for further customization
