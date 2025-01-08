# Make

Creating a `make`-like program in Go requires implementing features such as reading a configuration file
(like a `Makefile`), parsing dependencies, and executing commands. Below is an example structure with files divided
into logical paths. This implementation will focus on basic functionality for reading tasks, resolving dependencies,
and running commands.

## Features

- **Command-Line Interface**: Implements a command-line interface using `cobra`.
- **Makefile Parsing**: Parses simple Makefile formats to extract tasks and dependencies.
- **Task Execution**: Executes tasks and commands defined in the Makefile.
- **Variable Substitution**: Supports substituting variables within commands.
- **Dependency Resolution**: Handles task dependencies to ensure proper execution order.
- **Cross-Platform Support**: Provides compatibility for both Windows and Unix-like systems.
- **Logging**: Includes basic logging for better debugging and task tracking.
- **Stack Implementation**: Utilizes a stack to manage conditional logic.
- **Error Handling**: Gracefully handles errors to ensure robust execution.
- **Modular Structure**: Organizes code into logical and reusable modules.

Each feature includes a rudimentary implementation to demonstrate the fundamentals of creating a `make`-like program. The structure is designed to be expandable and adaptable to accommodate additional requirements or complexities.

Basic support for conditional logic (`ifeq`, `ifneq`, `ifdef`, `ifndef`) is provided. More advanced features can be integrated as needed.

### Global Variables in Makefiles
The following global variables are supported:
- **`OS`**: Operating system name
- **`PWD`**: Current working directory
- **`CURDIR`**: Current working directory
- **`HOME`**: Home directory
- **`SHELL`**: Shell program name
- **`PATH`**: System path
- **`USER`**: Current user
- **`USERNAME`**: Current user name
- **`MAKE`**: Make command

Additional variables can be defined and used as required.

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
    ├── logger.go
    └── stack.go
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
	"github.com/username/go-make/vars"
	"os"

	"github.com/username/go-make/cmd"
)

func main() {
	vars.Init()
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
	"log"
	"os"
	"strings"

	"github.com/username/go-make/executor"
	"github.com/username/go-make/vars"

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
		taskName := ""
		for _, arg := range args {
			if strings.Contains(arg, "=") {
				parts := strings.Split(arg, "=")
				vars.VarList[parts[0]] = vars.EvalVar(parts[1])
			} else if len(taskName) == 0 {
				taskName = arg
			} else {
				log.Fatal("Too many arguments")
				os.Exit(1)
			}
		}
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

### `make_file/parser.go`
```go
package make_file

import (
	"bufio"
	"fmt"
	"github.com/username/go-make/utils"
	"log"
	"os"
	"regexp"
	"strings"

	"github.com/username/go-make/vars"
)

type Task struct {
	Name         string
	Dependencies []string
	Command      []string
}

func ParseLogic(line string) bool {
	// Remove leading stuff until the first parenthesis
	pos := strings.Index(line, "(")
	if pos == -1 {
		return false
	}
	stmt := strings.Trim(line[:pos], " ")
	rawLogic := line[pos+1:]
	logic := ""

	idx := 0
	pCount := 0
	for idx < len(rawLogic) {
		if rawLogic[idx] == '(' {
			pCount++
		} else if rawLogic[idx] == ')' {
			pCount--
			if pCount < 0 {
				logic = strings.Trim(rawLogic[:idx], " ")
				break
			}
		}
		idx++
	}

	re := regexp.MustCompile(`\$\([a-zA-Z0-9_-]+\)`)

	for re.MatchString(logic) {
		logic = re.ReplaceAllStringFunc(logic, func(match string) string {
			// Replace the match with some value, for example, the key itself without $()
			key := match[2 : len(match)-1]
			value, ok := vars.VarList[key]
			if !ok {
				log.Fatalf("Variable %s not found", key)
			}
			return fmt.Sprintf("%s", value) // Example replacement
		})
	}

	// Evaluate the logic
	left := strings.Trim(strings.Split(logic, ",")[0], " ")
	right := strings.Trim(strings.Split(logic, ",")[1], " ")
	if stmt == "ifeq" {
		return left == right
	} else if stmt == "ifneq" {
		return left != right
	} else if stmt == "ifdef" {
		_, ok := vars.VarList[left]
		return ok
	} else if stmt == "ifndef" {
		_, ok := vars.VarList[left]
		return !ok
	}
	return false
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

	logicStack := utils.Stack{}

	for scanner.Scan() {
		line := scanner.Text()
		trimmedLine := strings.TrimSpace(line)

		if strings.HasPrefix(trimmedLine, "ifeq") {
			logicStack.Push(ParseLogic(trimmedLine))
		} else if strings.HasPrefix(trimmedLine, "ifneq") {
			logicStack.Push(ParseLogic(trimmedLine))
		} else if strings.HasPrefix(trimmedLine, "ifdef") {
			logicStack.Push(ParseLogic(trimmedLine))
		} else if strings.HasPrefix(trimmedLine, "ifndef") {
			logicStack.Push(ParseLogic(trimmedLine))
		} else if strings.HasPrefix(trimmedLine, "else") {
			logicStack.InvertCurrent()
		} else if strings.HasPrefix(trimmedLine, "endif") {
			if logicStack.IsEmpty() {
				log.Fatalf("Unexpected endif in line: %s", line)
			}
			logicStack.Pop()
		}
		if !logicStack.IsEmpty() {
			if value, ok := logicStack.Peek(); ok && !value {
				continue
			}
		}
		if !strings.HasPrefix(line, "\t") {
			if strings.Contains(line, "=") {
				parts := strings.SplitN(line, "=", 2)
				vars.VarList[parts[0]] = vars.EvalVar(parts[1])
				continue
			}
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

### `make_file/task.go`
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
	"runtime"
	"strings"

	"github.com/username/go-make/make_file"
	"github.com/username/go-make/vars"
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
				command = vars.EvalVar(command)
				fmt.Println(command)
				var cmd *exec.Cmd
				if runtime.GOOS == "windows" {
					cmd = exec.Command("cmd", "/C", strings.TrimPrefix(command, "@"))
				} else {
					cmd = exec.Command("sh", "-c", strings.TrimPrefix(command, "@"))
				}
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

### `utils/stack.go`
```go
package utils

// Stack represents a dynamic stack of bool values
type Stack []bool

// Push appends a value to the stack
func (s *Stack) Push(value bool) {
	*s = append(*s, value)
}

// Pop removes and returns the last value from the stack
func (s *Stack) Pop() (bool, bool) {
	if len(*s) == 0 {
		// Handle empty stack
		return false, false
	}
	last := (*s)[len(*s)-1]
	*s = (*s)[:len(*s)-1]
	return last, true
}

// Peek returns the last value from the stack without removing it
func (s *Stack) Peek() (bool, bool) {
	if len(*s) == 0 {
		// Handle empty stack
		return false, false
	}
	return (*s)[len(*s)-1], true
}

// IsEmpty returns true if the stack is empty
func (s *Stack) IsEmpty() bool {
	return len(*s) == 0
}

// InvertCurrent inverts the last value in the stack
func (s *Stack) InvertCurrent() {
	if len(*s) == 0 {
		// Handle empty stack
		return
	}
	(*s)[len(*s)-1] = !(*s)[len(*s)-1]
}

```

---

## Example `Makefile`
```Make
# Makefile

# Variables
BINARY_NAME=gomake
EXT=
RM=rm -f
ifeq ($(OS),Windows_NT)
    EXT=.exe
	RM=del /Q
endif
BINARY=$(BINARY_NAME)$(EXT)
STR=$(HELLO)

# Setup dependencies
setup:
	go mod init github.com/username/go-make
	go get github.com/spf13/cobra@latest

build:
	go build -o $(BINARY)

test: build
	./$(BINARY) echo HELLO=$(STR)

echo:
	@echo Hello, $(STR)!

complete: clean setup build
	make test HELLO=world

clean:
	$(RM) $(BINARY)
	$(RM) go.mod
	$(RM) go.sum

```

## Usage
1. Run `go build` to compile the program.
2. Use `./gomake <target>` to execute tasks defined in the `Makefile`.

This structure ensures the program is modular, extensible, and adheres to Go best practices.