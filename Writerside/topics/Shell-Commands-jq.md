# jq

`jq` is a lightweight and flexible command-line tool used for processing JSON data. It allows users to parse, filter, transform, and manipulate JSON input, making it invaluable for working with structured data in shell scripts and command-line workflows.

## Basic Syntax

```sh
jq [options] 'filter' file
```

## Commonly Used Options

- `-r`: Output raw strings instead of JSON-encoded strings.
- `-c`: Compact output, outputting JSON on a single line.
- `-M`: Disables colored output (useful when piping to other tools).
- `-f`: Specify a filter file instead of a command-line filter.

## Examples

### Basic Filter

Extract the value of a key from a JSON object:

```sh
echo '{"name": "Alice", "age": 30}' | jq '.name'
```

### Access Nested Values

Access a nested field in a JSON object:

```sh
echo '{"person": {"name": "Alice", "age": 30}}' | jq '.person.name'
```

### Filter Arrays

Extract all items from an array:

```sh
echo '[{"name": "Alice"}, {"name": "Bob"}]' | jq '.[].name'
```

### Pipe Filters

Chain multiple filters together:

```sh
echo '{"person": {"name": "Alice", "age": 30}}' | jq '.person | .name'
```

### Modify Data

Update values in a JSON object:

```sh
echo '{"name": "Alice", "age": 30}' | jq '.age = 31'
```

### Select Based on Condition

Filter JSON objects by a condition:

```sh
echo '[{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]' | jq '.[] | select(.age > 28)'
```

### Use Variables

Pass shell variables into `jq` filters:

```sh
name="Alice"
echo '{"name": "Alice", "age": 30}' | jq --arg name "$name" '.name == $name'
```

### Compact Output

Output JSON as a single line:

```sh
echo '{"name": "Alice", "age": 30}' | jq -c '.'
```

### Raw Output

Get raw string output without quotes:

```sh
echo '{"name": "Alice", "age": 30}' | jq -r '.name'
```

## Conclusion

`jq` is an essential tool for handling and processing JSON data efficiently from the command line. With its powerful filtering and transformation capabilities, it is indispensable for working with structured data in shell scripts and automation tasks.