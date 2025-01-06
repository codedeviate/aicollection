# Git-tool

Go is a powerful language for creating efficient and scalable tools. In this lesson, we'll build a lightweight Git-like command-line tool to interact with Git repositories. The tool supports common commands such as `clone`, `commit`, `push`, `pull`, and `status`. We'll use the popular [go-git](https://github.com/go-git/go-git) library to interact with Git repositories.

By the end of this lesson, you'll understand how to:
- Structure a Go project
- Use the `os` package to parse command-line arguments
- Utilize the go-git library for Git operations

Let's dive into the code!

## Project Structure
Here's the folder structure of our project:

```
mygittool/
|-- main.go
|-- commands/
    |-- clone.go
    |-- commit.go
    |-- push.go
    |-- pull.go
    |-- status.go
```

The `main.go` file serves as the entry point for our application, while the `commands` folder contains separate files for each Git command implementation.

---

## The Entry Point: `main.go`

The `main.go` file handles command-line argument parsing and dispatches commands to their respective functions:

```go
// main.go
package main

import (
	"fmt"
	"os"

	"github.com/username/git-tool/commands"
)

func main() {
	if len(os.Args) < 2 {
		fmt.Println("Usage: git-tool <command> [arguments]")
		os.Exit(1)
	}

	command := os.Args[1]
	args := os.Args[2:]

	switch command {
	case "clone":
		commands.Clone(args)
	case "commit":
		commands.Commit(args)
	case "push":
		commands.Push(args)
	case "pull":
		commands.Pull(args)
	case "status":
		commands.Status(args)
	default:
		fmt.Printf("Unknown command: %s\n", command)
		os.Exit(1)
	}
}
```

### Key Points (main.go):
- `os.Args` provides command-line arguments.
- The `switch` statement routes the specified command to its handler in the `commands` package.

---

## Command Implementations

### 1. Clone
The `clone` command clones a Git repository from a given URL:

```go
// commands/clone.go
package commands

import (
	"fmt"
	"os"

	"github.com/go-git/go-git/v5"
)

func Clone(args []string) {
	if len(args) < 1 {
		fmt.Println("Usage: git-tool clone <repository-url>")
		return
	}

	repoURL := args[0]
	_, err := git.PlainClone(".", false, &git.CloneOptions{
		URL:      repoURL,
		Progress: os.Stdout,
	})
	if err != nil {
		fmt.Printf("Error cloning repository: %v\n", err)
	}
}
```

### Key Points (clone.go):
- The `PlainClone` function clones the repository into the current directory.
- Errors are handled gracefully, with feedback provided to the user.

### 2. Commit
The `commit` command stages all changes and creates a commit:

```go
// commands/commit.go
package commands

import (
	"fmt"

	"github.com/go-git/go-git/v5"
)

func Commit(args []string) {
	if len(args) < 1 {
		fmt.Println("Usage: git-tool commit <message>")
		return
	}

	message := args[0]
	repo, err := git.PlainOpen(".")
	if err != nil {
		fmt.Printf("Error opening repository: %v\n", err)
		return
	}

	w, err := repo.Worktree()
	if err != nil {
		fmt.Printf("Error getting worktree: %v\n", err)
		return
	}

	_, err = w.Add(".")
	if err != nil {
		fmt.Printf("Error adding files: %v\n", err)
		return
	}

	_, err = w.Commit(message, &git.CommitOptions{})
	if err != nil {
		fmt.Printf("Error committing changes: %v\n", err)
	}
}
```

### Key Points (commit.go):
- Changes are staged using the `Add` method.
- A commit is created with the provided message.

### 3. Push
The `push` command pushes local changes to the remote repository:

```go
// commands/push.go
package commands

import (
	"fmt"

	"github.com/go-git/go-git/v5"
)

func Push(args []string) {
	repo, err := git.PlainOpen(".")
	if err != nil {
		fmt.Printf("Error opening repository: %v\n", err)
		return
	}

	err = repo.Push(&git.PushOptions{})
	if err != nil {
		fmt.Printf("Error pushing changes: %v\n", err)
	}
}
```

### Key Points (push.go):
- The `Push` function pushes commits to the default remote.

### 4. Pull
The `pull` command updates the local repository from the remote:

```go
// commands/pull.go
package commands

import (
	"fmt"

	"github.com/go-git/go-git/v5"
)

func Pull(args []string) {
	repo, err := git.PlainOpen(".")
	if err != nil {
		fmt.Printf("Error opening repository: %v\n", err)
		return
	}

	w, err := repo.Worktree()
	if err != nil {
		fmt.Printf("Error getting worktree: %v\n", err)
		return
	}

	err = w.Pull(&git.PullOptions{RemoteName: "origin"})
	if err != nil {
		fmt.Printf("Error pulling changes: %v\n", err)
	}
}
```

### Key Points (pull.go):
- The `Pull` function updates the local branch from the remote.

### 5. Status
The `status` command displays the current status of the repository:

```go
// commands/status.go
package commands

import (
	"fmt"

	"github.com/go-git/go-git/v5"
)

func Status(args []string) {
	repo, err := git.PlainOpenWithOptions(".", &git.PlainOpenOptions{
		DetectDotGit: true,
	})
	if err != nil {
		fmt.Printf("Error opening repository: %v\n", err)
		return
	}

	w, err := repo.Worktree()
	if err != nil {
		fmt.Printf("Error getting worktree: %v\n", err)
		return
	}

	status, err := w.Status()
	if err != nil {
		fmt.Printf("Error checking status: %v\n", err)
		return
	}

	fmt.Println(status)
}
```

### Key Points (status.go):
- The `Status` function retrieves and prints the working tree status.

---

## Running the Tool

Build and run the tool with the following commands:

```bash
$ go build -o git-tool
$ ./git-tool clone https://github.com/example/repo.git
```

Replace `clone` with any of the other commands (`commit`, `push`, `pull`, `status`) as needed.

---

## Conclusion
This project demonstrates how to create a modular and extendable command-line tool in Go. With a clear structure and the power of the go-git library, you can extend this tool to support additional Git commands or custom functionality tailored to your needs. Happy coding!

