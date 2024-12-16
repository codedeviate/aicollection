# JED

JED is a simple, yet powerful text editor designed for developers who want a fast and efficient editing experience. Its minimalist interface belies its feature-rich capabilities, making it a versatile tool for various tasks.

## Key Features of JED

1. **Minimalist Interface**: JED provides a clean and straightforward interface, focusing on efficiency.
2. **Syntax Highlighting**: Offers syntax highlighting for a wide range of programming languages.
3. **Macro Support**: Supports macros to automate repetitive tasks.
4. **Configurable**: Users can customize JED's behavior through configuration files.
5. **Multiple Buffers**: Allows editing multiple files simultaneously using buffers.
6. **Extensible**: Can be extended with additional functionality through scripting.

## Common Commands

- **Ctrl + X Ctrl + S**: Save the current buffer.
- **Ctrl + X Ctrl + C**: Exit JED.
- **Ctrl + K**: Cut the current line.
- **Ctrl + Y**: Paste the cut line.
- **Ctrl + S**: Search for a string.
- **Ctrl + R**: Replace a string.
- **Ctrl + G**: Cancel the current command.

## Example Usage

To open a file with JED, use the following command in the terminal:

```sh
jed filename.txt
```

This will open `filename.txt` in the JED editor. You can then use the commands mentioned above to edit the file.

## Configuration

JED can be configured using the `jed.rc` file. Here is an example configuration:

```lisp
% Enable syntax highlighting
enable_syntax_highlighting();

% Set tab width to 4 spaces
set_tab_width(4);

% Enable auto-indentation
enable_auto_indentation();
```

This configuration enables syntax highlighting, sets the tab width to 4 spaces, and enables auto-indentation.

JED is a powerful and flexible text editor that can be tailored to meet the needs of both beginners and experienced users. Its extensive customization options and wide range of features make it a valuable tool for text editing and development.
