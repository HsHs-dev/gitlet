# Gitlet

Gitlet is a version-control system implemented after a subset of Git's features. It is implemented in the Java programming language.

![gitlet-logo](gitlet-logo.png)

Gitlet is project 2 in [UCB-CS61B: Data Structures and Algorithms](https://github.com/HsHs-dev/UCB-CS61B) course, which aims to implement such a complex system with considerable amount of DSA such as git, to give a sense of how DSA can be used together, and how it can impact our design choices in a real-world system.

## Features

Gitlet supports a subset of the git version control commands, allowing users to track changes, manage different lines of development, and review the history of their projects.

- **Repository Management**: Initialize a new repository.
- **File Tracking**: Add files to a staging area for the next commit.
- **Committing**: Save snapshots of the project's state.
- **History Viewing**: View the log of commits for the current branch or the entire repository.
- **Branching**: Create, delete, and switch between branches.
- **File Restoration**: Checkout files from previous commits or different branches.
- **Merging**: Merging two branches together.

## Supported Commands

| Command | Description |
| :--- | :--- |
| `init` | Creates a new Gitlet version-control system in the current directory. |
| `add [file name]` | Adds a copy of the file as it currently exists to the staging area. |
| `commit [message]` | Saves a snapshot of the tracked files and the current staging area. |
| `rm [file name]` | Unstages the file if it is currently staged for addition. If the file is tracked in the current commit, stages it for removal and removes the file from the working directory. |
| `log` | Displays the commit history starting from the current head commit and moving backwards. |
| `global-log` | Displays information about all commits ever made, in any order. |
| `find [commit message]` | Prints out the IDs of all commits that have the given commit message. |
| `status` | Displays what branches currently exist, and marks the current branch. Also shows what files have been staged for addition or removal. |
| `checkout -- [file name]` | Restores the file in the working directory to its state in the head commit. |
| `checkout [commit id] -- [file name]` | Restores the file in the working directory to its state in the commit with the given ID. |
| `checkout [branch name]` | Checks out all files tracked by the given branch, deleting tracked files not present in that branch and moving the head pointer. |
| `branch [branch name]` | Creates a new branch with the given name, pointing it at the current head commit. |
| `rm-branch [branch name]` | Deletes the branch with the given name. |
| `reset [commit id]` | Checks out all the files tracked by the given commit and moves the current branch's head to that commit. |
| `merge [branch name]` | Merges files from the given branch into the current branch. |

## Design

Gitlet's state is stored within a `.gitlet` directory in the root of the project.

- **Commits**: Each commit is a `Commit` object, serialized and stored in the `.gitlet/commits` directory. A commit contains its metadata (message, timestamp, parent hash) and a map of filenames to their content hashes (blobs).
- **Blobs**: The contents of committed files are stored as "blobs" in the `.gitlet/blobs` directory. Each blob is named by its SHA-1 hash of its content, which allows for efficient storage by avoiding content duplication.
- **Staging Area**: Files staged for addition or removal are tracked in a `Staging` object, which is serialized to the `.gitlet/staged` file.
- **Branches and HEAD**: Branches are pointers to commit hashes. Each branch is a file in `.gitlet/branches` whose content is the hash of the commit it points to. The `HEAD` file contains the name of the currently active branch.

## Building

The project uses a `Makefile` for building and testing.

### Compilation

To compile the Java source code, run the following command from the root of the directory:

```bash
make
```

## Usage

after compilation, copy all the class files in the gitlet directory to a folder in the directory you want to use gitlet in

```bash
cp gitlet/*.class <destination_dir/gitlet>
```

then run a command from [Supported Commands](#supported-commands) list as follows:

```bash
java gitlet.Main <command>
```
