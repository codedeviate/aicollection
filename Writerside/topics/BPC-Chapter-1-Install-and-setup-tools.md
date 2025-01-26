# Chapter 1 - Installing and Setting Up Tools

This guide will walk you through the installation and setup of all the tools you'll need to follow the Basic Programming course. By the end of this guide, you'll have a fully functioning programming environment, ready for Python, PHP, C++, Zig, and Go development on Linux, Windows, and macOS.

---

## Tools Overview
1. **Code Editor**: Visual Studio Code (VS Code) is recommended for this course.
2. **Compilers/Interpreters**:
    - Python: Python interpreter (latest version)
    - PHP: PHP runtime
    - C++: GCC or Clang compiler
    - Zig: Zig programming language toolchain
    - Go: Go programming language toolchain
3. **Version Control**: Git for source code management.
4. **Terminal Emulator**: Optional for Windows users—install Windows Terminal or use the built-in Command Prompt/PowerShell.
5. **Build Tools**: Additional build tools like Make or CMake for C++ projects.

---

## Installing Visual Studio Code

### Linux
1. Download the VS Code package for your Linux distribution:
   ```bash
   wget -qO- https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64 -O vscode.deb
   sudo dpkg -i vscode.deb
   sudo apt-get install -f  # Fix dependencies
   ```
2. Start VS Code:
   ```bash
   code
   ```

### Windows
1. Download VS Code from [Visual Studio Code’s official website](https://code.visualstudio.com/).
2. Run the installer and follow the setup wizard.
3. Ensure the "Add to PATH" option is checked during installation.

### macOS
1. Download the VS Code `.dmg` file from [Visual Studio Code’s website](https://code.visualstudio.com/).
2. Drag the VS Code icon into the Applications folder.
3. Open VS Code from Launchpad or Finder.

---

## Installing Compilers and Runtimes

### Python
- **Linux**:
  ```bash
  sudo apt update
  sudo apt install python3 python3-pip
  ```
- **Windows**:
    1. Download Python from [python.org](https://www.python.org/).
    2. Run the installer and ensure "Add Python to PATH" is selected.
- **macOS**:
  ```bash
  brew install python
  ```

### PHP
- **Linux**:
  ```bash
  sudo apt update
  sudo apt install php
  ```
- **Windows**:
    1. Download PHP from [php.net](https://windows.php.net/).
    2. Add PHP to the system PATH.
- **macOS**:
  ```bash
  brew install php
  ```

### C++ Compiler (GCC/Clang)
- **Linux**:
  ```bash
  sudo apt update
  sudo apt install build-essential
  ```
- **Windows**:
    1. Install [MSYS2](https://www.msys2.org/).
    2. Open MSYS2 and run:
       ```bash
       pacman -S mingw-w64-x86_64-gcc
       ```
- **macOS**:
  ```bash
  xcode-select --install
  ```

### Zig
- **Linux**:
  ```bash
  wget https://ziglang.org/download/index.html -O zig.tar.xz
  tar -xf zig.tar.xz
  sudo mv zig-* /opt/zig
  sudo ln -s /opt/zig/zig /usr/local/bin/zig
  ```
- **Windows**:
    1. Download Zig from [ziglang.org](https://ziglang.org/download/).
    2. Extract the zip file and add Zig to your system PATH.
- **macOS**:
  ```bash
  brew install zig
  ```

### Go
- **Linux**:
  ```bash
  wget https://golang.org/dl/go1.20.linux-amd64.tar.gz -O go.tar.gz
  sudo tar -C /usr/local -xzf go.tar.gz
  echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.profile
  source ~/.profile
  ```
- **Windows**:
    1. Download Go from [golang.org](https://golang.org/dl/).
    2. Run the installer and follow the setup wizard.
    3. Restart your terminal to ensure Go is added to the PATH.
- **macOS**:
  ```bash
  brew install go
  ```

---

## Installing Git
- **Linux**:
  ```bash
  sudo apt update
  sudo apt install git
  ```
- **Windows**:
    1. Download Git from [git-scm.com](https://git-scm.com/).
    2. Follow the setup wizard, choosing default options unless otherwise specified.
- **macOS**:
  ```bash
  brew install git
  ```

---

## Optional: Installing Build Tools (Make/CMake)

### Make
- **Linux**:
  ```bash
  sudo apt install make
  ```
- **Windows**:
    1. Install [GNU Make](http://gnuwin32.sourceforge.net/packages/make.htm).
    2. Add Make to the PATH.
- **macOS**:
  ```bash
  brew install make
  ```

### CMake
- **Linux**:
  ```bash
  sudo apt install cmake
  ```
- **Windows**:
    1. Download CMake from [cmake.org](https://cmake.org/download/).
    2. Run the installer and select "Add CMake to system PATH."
- **macOS**:
  ```bash
  brew install cmake
  ```

---

## Verifying Your Setup

Run the following commands to verify the installation of each tool:

- **Python**:
  ```bash
  python3 --version
  ```
- **PHP**:
  ```bash
  php --version
  ```
- **GCC (C++)**:
  ```bash
  gcc --version
  ```
- **Zig**:
  ```bash
  zig version
  ```
- **Go**:
  ```bash
  go version
  ```
- **Git**:
  ```bash
  git --version
  ```
- **Make** (if installed):
  ```bash
  make --version
  ```
- **CMake** (if installed):
  ```bash
  cmake --version
  ```

---

## Setting Up Your Development Environment

1. **Install Extensions in VS Code**:
    - Python
    - PHP Intelephense
    - C++
    - Zig Language Support
    - Go
    - GitLens (for Git integration)

2. **Configure Git**:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "youremail@example.com"
   ```

3. **Test a "Hello, World!" Program in Each Language**:

- **Python**:
  ```python
  print("Hello, World!")
  ```
- **PHP**:
  ```php
  <?php
  echo "Hello, World!";
  ?>
  ```
- **C++**:
  ```cpp
  #include <iostream>
  using namespace std;

  int main() {
      cout << "Hello, World!" << endl;
      return 0;
  }
  ```
- **Zig**:
  ```zig
  const std = @import("std");

  pub fn main() void {
      std.debug.print("Hello, World!\n", .{});
  }
  ```
- **Go**:
  ```go
  package main

  import "fmt"

  func main() {
      fmt.Println("Hello, World!")
  }
  ```

4. Run each program using the respective compiler or interpreter.

---

Now that you have all the tools installed and configured, you're ready to dive into the Basic Programming course!

