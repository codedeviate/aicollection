# Text Diff

Below is a basic Go program to perform a diff operation (finding differences between two texts).
The program is divided into logical parts, with explanations and documentation.
We will use Go's standard library and implement a simple line-by-line diff that shows what lines are added or removed
from one text compared to the other.

> Please note that this diff is not compatible with the `diff` command-line tool and is a basic implementation for
> educational purposes. The output is not in the standard unified diff format and therefore not compatible with patching
> tools.

```go
package main

import (
	"bufio"
	"fmt"
	"os"
)

// DiffResult represents the results of a diff operation.
type DiffResult struct {
	Added   []string // Lines that are in new text but not in old text
	Removed []string // Lines that are in old text but not in new text
}

// ReadFile reads the file content and returns it as a slice of strings (lines).
func ReadFile(filePath string) ([]string, error) {
	file, err := os.Open(filePath)
	if err != nil {
		return nil, err
	}
	defer file.Close()

	var lines []string
	scanner := bufio.NewScanner(file)
	for scanner.Scan() {
		lines = append(lines, scanner.Text())
	}

	if err := scanner.Err(); err != nil {
		return nil, err
	}

	return lines, nil
}

// Diff compares two slices of strings (representing two versions of text).
// It returns a DiffResult containing lines added and removed.
func Diff(oldLines, newLines []string) DiffResult {
	var diff DiffResult

	oldSet := make(map[string]struct{})
	newSet := make(map[string]struct{})

	// Fill the maps with old and new lines
	for _, line := range oldLines {
		oldSet[line] = struct{}{}
	}
	for _, line := range newLines {
		newSet[line] = struct{}{}
	}

	// Find removed lines (present in old but not in new)
	for _, line := range oldLines {
		if _, exists := newSet[line]; !exists {
			diff.Removed = append(diff.Removed, line)
		}
	}

	// Find added lines (present in new but not in old)
	for _, line := range newLines {
		if _, exists := oldSet[line]; !exists {
			diff.Added = append(diff.Added, line)
		}
	}

	return diff
}

// PrintDiff prints the diff result to the console.
func PrintDiff(diff DiffResult) {
	fmt.Println("Removed lines:")
	for _, line := range diff.Removed {
		fmt.Printf("- %s\n", line)
	}

	fmt.Println("\nAdded lines:")
	for _, line := range diff.Added {
		fmt.Printf("+ %s\n", line)
	}
}

// main function to drive the diff comparison.
func main() {
	if len(os.Args) != 3 {
		fmt.Println("Usage: diff <old file> <new file>")
		os.Exit(1)
	}

	// Read the old and new files.
	oldFilePath := os.Args[1]
	newFilePath := os.Args[2]

	oldLines, err := ReadFile(oldFilePath)
	if err != nil {
		fmt.Printf("Error reading old file: %v\n", err)
		return
	}

	newLines, err := ReadFile(newFilePath)
	if err != nil {
		fmt.Printf("Error reading new file: %v\n", err)
		return
	}

	// Perform the diff comparison.
	diff := Diff(oldLines, newLines)

	// Print the results.
	PrintDiff(diff)
}

```

## Logical Parts of the Program:

1. **Imports and Package Declaration**:
    - We import necessary packages:
        - `bufio`: for reading the files line by line.
        - `fmt`: for printing results to the console.
        - `os`: for interacting with the file system.
        - `strings`: for string manipulation (though it's not actively used in this version, you might use it for further enhancements).

2. **DiffResult Struct**:
    - A `DiffResult` struct holds the results of the diff operation:
        - `Added`: A slice of strings that contains lines added in the new file but not present in the old file.
        - `Removed`: A slice of strings that contains lines removed in the new file but present in the old file.

3. **ReadFile Function**:
    - Reads a file line by line and returns the content as a slice of strings.
    - Handles file opening, reading, and error checking.
    - Uses a scanner to read each line and store them in a slice.

4. **Diff Function**:
    - This function performs the actual diffing:
        - It creates two sets (maps) to store the old and new lines.
        - It then compares the two sets:
            - Lines in the old set but not in the new set are considered "removed".
            - Lines in the new set but not in the old set are considered "added".
    - The result is a `DiffResult` struct containing the added and removed lines.

5. **PrintDiff Function**:
    - This function prints the diff results to the console.
    - It prints the removed lines with a `-` and the added lines with a `+`.

6. **Main Function**:
    - The main function orchestrates reading the files, performing the diff, and printing the results.
    - File paths are hardcoded for demonstration, but they can be modified to be dynamically passed or read from user input.

## Running the Program:
- You can create two text files, `old_version.txt` and `new_version.txt`, and place some sample content in them.
- Compile and run the Go program, which will read both files, perform the diff, and print the added and removed lines.

## Example Usage:
- For the file `old_version.txt`:
  ```
  line1
  line2
  line3
  ```

- And the file `new_version.txt`:
  ```
  line2
  line3
  line4
  ```

- The output would be:
  ```
  Removed lines:
  - line1

  Added lines:
  + line4
  ```

## Enhancements:
- You can extend this basic program by adding more sophisticated diffing algorithms, such as the Myers' diff algorithm, for more accurate results, especially for larger and more complex text files.