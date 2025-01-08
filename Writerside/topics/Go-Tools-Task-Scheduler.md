# Task Scheduler

To create a task scheduler program in Go, follow these steps:

## Step 1: Initialize the Go Module

First, create a new directory for your project and initialize the Go module.

```sh
mkdir task_scheduler
cd task_scheduler
go mod init github.com/username/task_scheduler
```

## Step 2: Install Dependencies

You will need the following library:
- `github.com/robfig/cron/v3` for parsing crontab expressions


## Step 3: Create the `scheduler.go` File

Create a `lib/scheduler.go` file to handle the task scheduling functionality.

```go
// scheduler.go
package lib

import (
	"fmt"
	"log"
	"time"

	"github.com/robfig/cron/v3"
)

// Task represents a scheduled task.
type Task struct {
    Name       string
    Interval   time.Duration
    CronExpr   string
    Delay      time.Duration
    Condition  func() bool
    Action     func()
    LastStatus string
}

// Scheduler manages and runs tasks.
type Scheduler struct {
    tasks []Task
    cron  *cron.Cron
}

// NewScheduler creates a new Scheduler.
func NewScheduler() *Scheduler {
    return &Scheduler{
        cron: cron.New(),
    }
}

// AddTask adds a new task to the scheduler.
func (s *Scheduler) AddTask(task Task) {
    s.tasks = append(s.tasks, task)
    if task.CronExpr != "" {
        s.cron.AddFunc(task.CronExpr, func() {
            s.executeTask(task)
        })
    } else if task.Interval > 0 {
        go func(t Task) {
            ticker := time.NewTicker(t.Interval)
            for {
                select {
                case <-ticker.C:
                    s.executeTask(t)
                }
            }
        }(task)
    } else if task.Delay > 0 {
        go func(t Task) {
            time.Sleep(t.Delay)
            s.executeTask(t)
        }(task)
    }
}

// Start runs the scheduler and executes tasks at their specified intervals.
func (s *Scheduler) Start() {
    s.cron.Start()
    for _, task := range s.tasks {
        if task.CronExpr == "" && task.Interval == 0 && task.Delay == 0 {
            go s.executeTask(task)
        }
    }
}

// Stop stops the scheduler.
func (s *Scheduler) Stop() {
    s.cron.Stop()
    fmt.Println("Scheduler stopped")
}

// executeTask executes a task and logs its status.
func (s *Scheduler) executeTask(task Task) {
    if task.Condition != nil && !task.Condition() {
        log.Printf("Task %s skipped due to condition", task.Name)
        return
    }
    log.Printf("Task %s started", task.Name)
    task.Action()
    task.LastStatus = "completed"
    log.Printf("Task %s completed", task.Name)
}

```

## Step 4: Create the `main.go` File

Create a `main.go` file to use the task scheduling functionality.

```go
// main.go
package main

import (
	"fmt"
	"time"

	"github.com/username/taskscheduler/lib"
)

func main() {
	scheduler := lib.NewScheduler()

	// Example task: Print a message every 2 seconds
	scheduler.AddTask(lib.Task{
		Name:     "PrintMessage",
		Interval: 2 * time.Second,
		Action: func() {
			fmt.Println("Task executed: PrintMessage")
		},
	})

	// Example task: Print a different message every 5 seconds
	scheduler.AddTask(lib.Task{
		Name:     "PrintAnotherMessage",
		Interval: 5 * time.Second,
		Action: func() {
			fmt.Println("Task executed: PrintAnotherMessage")
		},
	})

	// Example task: Print a message after a 10-second delay
	scheduler.AddTask(lib.Task{
		Name:  "DelayedMessage",
		Delay: 10 * time.Second,
		Action: func() {
			fmt.Println("Task executed: DelayedMessage")
		},
	})

	// Example task: Print a message based on a cron expression
	scheduler.AddTask(lib.Task{
		Name:     "CronMessage",
		CronExpr: "*/1 * * * *", // Every minute
		Action: func() {
			fmt.Println("Task executed: CronMessage")
		},
	})

	// Example task: Print a message if a condition is met
	scheduler.AddTask(lib.Task{
		Name: "ConditionalMessage",
		Condition: func() bool {
			return time.Now().Second()%2 == 0
		},
		Action: func() {
			fmt.Println("Task executed: ConditionalMessage")
		},
	})

	// Start the scheduler
	scheduler.Start()

	// Keep the main function running
	select {}
}

```

## Step 5: Run the Program

Run the program using the `go run` command.

```sh
go run main.go
```

This will start the task scheduler and execute the tasks at their specified intervals.