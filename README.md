# Trek — Mini Version Control

Trek is a small Git-inspired version-control CLI written in Python. It stores file objects, commits, and branch references in a `.trek` directory in the current working directory.

**Repository:** [github.com/tayyba678/trek---mini_version_control](https://github.com/tayyba678/trek---mini_version_control)

## Requirements

- Python 3.10 or later
- `colorama`

## Install and run

Clone this repository, then install the dependency:

```bash
git clone https://github.com/tayyba678/trek---mini_version_control.git
cd trek---mini_version_control
python -m pip install -r requirements.txt
```

Start the CLI with:

```bash
python main.py
```

These commands work in PowerShell, Command Prompt, and Unix-like terminals. Trek operates on the directory from which it is started. To track another project, change to that project's directory and launch Trek's `main.py` from there.

## Quick start

At the `trek>` prompt, initialize a repository, stage files, and commit:

```text
trek> init
trek> add file1.py file2.py
trek> commit Add initial files
trek> status
trek> graph
```

`add` accepts one or more file paths. File paths are interpreted relative to the directory where Trek was started.

## Commands

| Command | Description |
| --- | --- |
| `init` | Create a `.trek` repository in the current directory. |
| `add <file> [file ...]` | Stage existing files. |
| `commit <message>` | Save the staged files in a commit. |
| `branch` | List branches. |
| `branch <name>` | Create a branch at the current commit and switch to it. If it already exists, switch to it. |
| `checkout <branch>` | Switch to an existing branch and restore files from its commit. |
| `merge <commit-hash>` | Attempt a simple merge with the specified commit hash. |
| `reset <commit-hash>` | Move the current HEAD to a commit and restore files from it. |
| `undo` / `redo` | Use the in-memory undo/redo stacks, if entries are available. |
| `graph` | Display the commit history reachable from the current HEAD. |
| `status` | Display the current HEAD hash. |
| `exit` | Leave the CLI. |

### Branch example

```text
trek> branch feature
trek> add file2.py
trek> commit Add feature file
trek> checkout master
```

`merge` currently takes a commit hash, not a branch name. Branch reference files are stored under `.trek/refs/heads/`.

## Project layout

```text
.
├── main.py
├── requirements.txt
├── README.md
└── trek/
    ├── branch.py
    ├── commit.py
    ├── config.py
    ├── dag.py
    ├── merge.py
    ├── remote.py
    ├── repository.py
    ├── reset.py
    ├── staging.py
    └── utils.py
```

## Notes and limitations

- Trek is an educational prototype, not a replacement for Git.
- Merge conflict handling is basic and may require manually editing conflict markers.
- `undo` and `redo` use in-memory stacks, so their history does not persist after exiting the program.
- `remote.py` is not connected to a CLI command; remote push is not available through the prompt.
- File paths containing spaces are not supported by the current command parser.
