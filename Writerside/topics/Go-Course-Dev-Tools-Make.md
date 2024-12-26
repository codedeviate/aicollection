# Make

Creating a `make`-like program in Go requires implementing features such as reading a configuration file (like a `Makefile`), parsing dependencies, and executing commands. Below is an example structure with files divided into logical paths. This implementation will focus on basic functionality for reading tasks, resolving dependencies, and running commands.

## Directory Structure

```Plain Text
go-make/
├── main.go
├── cmd/
│   └── root.go
├── makefile/
│   ├── parser.go
│   └── task.go
├── executor/
│   └── runner.go
└── utils/
    └── logger.go
```

## Setup and Dependencies

```
mkdir go-make
cd go-make
go mod init github.com/username/go-make
go get github.com/spf13/cobra
mkdir cmd makefile executor utils
```

## Code Implementation

### `main.go`
```go
package main

import (
	"fmt"
	"os"

	"github.com/username/go-make/cmd"
)

func main() {
	if err := cmd.Execute(); err != nil {
		fmt.Println(err)
		os.Exit(1)
	}
}

```

---

### `cmd/root.go`
```go
package cmd

import (
	"fmt"
	"os"

	"github.com/username/go-make/executor"

	"github.com/spf13/cobra"
	"github.com/username/go-make/make_file"
)

var rootCmd = &cobra.Command{
	Use:   "gomake",
	Short: "GoMake is a lightweight alternative to GNU Make",
	Long:  `GoMake parses a simple Makefile and executes the tasks defined in it.`,
	Run: func(cmd *cobra.Command, args []string) {
		if len(args) < 1 {
			fmt.Println("Please specify a target task")
			os.Exit(1)
		}
		taskName := args[0]
		makeFileName, _ := cmd.Flags().GetString("file")
		if len(makeFileName) == 0 {
			makeFileName = "Makefile"
		}
		tasks, err := make_file.ParseMakefile(makeFileName)
		if err != nil {
			fmt.Printf("Error parsing Makefile: %v\n", err)
			os.Exit(1)
		}

		if err := executor.RunTask(taskName, tasks); err != nil {
			fmt.Printf("Error executing task: %v\n", err)
			os.Exit(1)
		}
	},
}

func Execute() error {
	rootCmd.Flags().StringP("file", "f", "Makefile", "Specify the Makefile to use")
	return rootCmd.Execute()
}

```

---

### `makefile/parser.go`
```go
package make_file

import (
	"bufio"
	"log"
	"os"
	"strings"
)

type Task struct {
	Name         string
	Dependencies []string
	Command      []string
}

// ParseMakefile reads and parses a Makefile.
func ParseMakefile(filename string) (map[string]*Task, error) {
	file, err := os.Open(filename)
	if err != nil {
		return nil, err
	}
	defer file.Close()

	tasks := make(map[string]*Task)
	scanner := bufio.NewScanner(file)
	var currentTask *Task

	for scanner.Scan() {
		line := scanner.Text()
		trimmedLine := strings.TrimSpace(line)
		if !strings.HasPrefix(line, "\t") {
			parts := strings.Split(trimmedLine, ":")
			taskName := strings.TrimSuffix(parts[0], ":")
			currentTask = &Task{Name: taskName}
			tasks[taskName] = currentTask
			if len(parts) > 1 && parts[1] != "" {
				currentTask.Dependencies = strings.Fields(parts[1])
			}
		} else if currentTask != nil && strings.HasPrefix(line, "\t") {
			currentTask.Command = append(currentTask.Command, strings.TrimSpace(line))
		} else if currentTask != nil {
			currentTask.Dependencies = append(currentTask.Dependencies, strings.Fields(line)...)
		} else {
			log.Fatalf("Unknown action in line: %s", line)
		}
	}

	if err := scanner.Err(); err != nil {
		return nil, err
	}
	return tasks, nil
}

```

---

### `makefile/task.go`
```go
package make_file

import "fmt"

// ResolveDependencies resolves all dependencies for a task recursively.
func ResolveDependencies(taskName string, tasks map[string]*Task, resolved map[string]bool) ([]string, error) {
	if resolved[taskName] {
		return nil, nil
	}

	task, exists := tasks[taskName]
	if !exists {
		return nil, fmt.Errorf("task '%s' not found", taskName)
	}

	var dependencies []string
	for _, dep := range task.Dependencies {
		subDeps, err := ResolveDependencies(dep, tasks, resolved)
		if err != nil {
			return nil, err
		}
		dependencies = append(dependencies, subDeps...)
	}
	resolved[taskName] = true
	dependencies = append(dependencies, taskName)
	return dependencies, nil
}

```

---

### `executor/runner.go`
```go
package executor

import (
	"fmt"
	"os"
	"os/exec"
	"strings"

	"github.com/username/go-make/make_file"
)

func RunTask(taskName string, tasks map[string]*make_file.Task) error {
	resolved := make(map[string]bool)
	executionOrder, err := make_file.ResolveDependencies(taskName, tasks, resolved)
	if err != nil {
		return err
	}

	for _, task := range executionOrder {
		if len(tasks[task].Command) > 0 {
			for _, command := range tasks[task].Command {
				cmd := exec.Command("sh", "-c", strings.TrimPrefix(command, "@"))
				cmd.Stderr = os.Stderr
				cmd.Stdout = os.Stdout
				if err := cmd.Run(); err != nil {
					return fmt.Errorf("task '%s' failed: %s", task, err.Error())
				}
			}
		}
	}

	return nil
}

```

---

### `utils/logger.go`
```go
package utils

import (
	"log"
	"os"
)

var logger = log.New(os.Stdout, "[GoMake] ", log.LstdFlags)

// Info logs an informational message.
func Info(msg string) {
	logger.Println(msg)
}

// Error logs an error message.
func Error(msg string) {
	logger.Println(msg)
}

```

---

## Example `Makefile`
```Make
setup:
	go mod init github.com/username/go-make
	go get github.com/spf13/cobra@latest

build:
	go build -o gomake

test: build
	./gomake echo

echo:
	@echo "Hello, World!"

clean:
	rm -f gomake
	rm -f go.mod
	rm -f go.sum

```

## Usage
1. Run `go build` to compile the program.
2. Use `./gomake <target>` to execute tasks defined in the `Makefile`.

This structure ensures the program is modular, extensible, and adheres to Go best practices.