# Supercharge Your Terminal: 30 Non-Standard Commands That Can Transform Your Workflow

While your operating system may ship with a handful of essential command-line tools, there exists a vast ecosystem of utilities that can make your terminal work smarter and faster. Whether you’re a developer, system administrator, or just a command-line enthusiast, these 30 tools will help you get more out of your shell.

For each tool, you’ll find a compatibility table below its description. Note that while many of these commands are natively available on Linux and macOS (via package managers), Windows users might need to use PowerShell, install via Chocolatey, or leverage the Windows Subsystem for Linux (WSL).

## 1. htop

**What It Is:**  
An interactive process viewer that improves on the classic `top` command with a colorful, user-friendly interface.

**Why You Need It:**  
- Real-time monitoring of system resources  
- Easy process management with intuitive keyboard shortcuts

**Installation:**  
```sh
# Debian/Ubuntu:
sudo apt install htop

# macOS (via Homebrew):
brew install htop
```

**Compatibility:**

| Platform         | Availability & Notes                          |
|------------------|-----------------------------------------------|
| Linux            | Yes (native packages available)               |
| macOS            | Yes (via Homebrew)                            |
| Windows (PS/WSL) | Via WSL or Cygwin; not natively in PowerShell |

## 2. ncdu

**What It Is:**  
A disk usage analyzer with a text-based interface that lets you quickly identify large directories.

**Why You Need It:**
- Interactive navigation through disk usage
- Fast identification of space hogs

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install ncdu

# macOS:
brew install ncdu
```

**Compatibility:**

| Platform         | Availability & Notes                    |
|------------------|-----------------------------------------|
| Linux            | Yes                                     |
| macOS            | Yes (via Homebrew)                      |
| Windows (PS/WSL) | Via WSL; Windows native version is rare |

## 3. bat

**What It Is:**  
A `cat` clone with syntax highlighting, Git integration, and automatic paging for better readability.

**Why You Need It:**
- Enhanced file viewing with syntax highlighting
- Displays Git modifications alongside file contents

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install bat

# macOS:
brew install bat
```

**Compatibility:**

| Platform         | Availability & Notes                |
|------------------|-------------------------------------|
| Linux            | Yes                                 |
| macOS            | Yes (via Homebrew)                  |
| Windows (PS/WSL) | Yes (via Scoop, Chocolatey, or WSL) |

## 4. ripgrep (rg)

**What It Is:**  
A blazing-fast search tool that recursively searches directories with regex support.

**Why You Need It:**
- Multithreaded searching for speed
- Respects `.gitignore` by default

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install ripgrep

# macOS:
brew install ripgrep
```

**Compatibility:**

| Platform         | Availability & Notes                    |
|------------------|-----------------------------------------|
| Linux            | Yes                                     |
| macOS            | Yes (via Homebrew)                      |
| Windows (PS/WSL) | Yes (available via Chocolatey or Scoop) |

## 5. exa

**What It Is:**  
A modern replacement for `ls`, offering a colorful and informative file listing.

**Why You Need It:**
- Enhanced visuals with icons and Git integration
- Tree view for exploring directories

**Installation:**
```sh
# macOS:
brew install exa

# Debian/Ubuntu (via package or binary):
sudo apt install exa
```

**Compatibility:**

| Platform         | Availability & Notes                                  |
|------------------|-------------------------------------------------------|
| Linux            | Yes (available in some distributions or via binaries) |
| macOS            | Yes (via Homebrew)                                    |
| Windows (PS/WSL) | Via WSL or via binaries (limited native support)      |

## 6. fd

**What It Is:**  
A simple, fast, and user-friendly alternative to the `find` command.

**Why You Need It:**
- Intuitive syntax and smart defaults
- Automatically excludes hidden/system files unless specified

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install fd-find

# macOS:
brew install fd
```

*Note:* You might need to alias `fdfind` to `fd` on some systems.

**Compatibility:**

| Platform         | Availability & Notes                |
|------------------|-------------------------------------|
| Linux            | Yes                                 |
| macOS            | Yes (via Homebrew)                  |
| Windows (PS/WSL) | Yes (via Scoop, Chocolatey, or WSL) |

## 7. tldr

**What It Is:**  
Community-driven simplified man pages that provide practical examples for commands.

**Why You Need It:**
- Quick, concise help when you’re in a hurry
- Easy-to-read examples complementing traditional man pages

**Installation:**
```sh
# macOS:
brew install tldr

# Debian/Ubuntu (via npm):
sudo npm install -g tldr
```

**Compatibility:**

| Platform         | Availability & Notes                 |
|------------------|--------------------------------------|
| Linux            | Yes                                  |
| macOS            | Yes                                  |
| Windows (PS/WSL) | Yes (via npm or Chocolatey packages) |

## 8. thefuck

**What It Is:**  
A tool that corrects your previous command when you make a typo—just type `fuck` afterward!

**Why You Need It:**
- Saves time by suggesting corrections
- Helps you learn the proper command syntax

**Installation:**
```sh
pip install thefuck
# Then add to your shell config:
eval $(thefuck --alias)
```

**Compatibility:**

| Platform         | Availability & Notes                       |
|------------------|--------------------------------------------|
| Linux            | Yes                                        |
| macOS            | Yes                                        |
| Windows (PS/WSL) | Yes (via pip; works in WSL or in Git Bash) |

## 9. fzf

**What It Is:**  
A general-purpose fuzzy finder for your command line, ideal for searching files, history, and more.

**Why You Need It:**
- Fast fuzzy search with minimal input
- Seamless integration with many workflows

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install fzf

# macOS:
brew install fzf
```

**Compatibility:**

| Platform         | Availability & Notes                |
|------------------|-------------------------------------|
| Linux            | Yes                                 |
| macOS            | Yes (via Homebrew)                  |
| Windows (PS/WSL) | Yes (via Scoop, Chocolatey, or WSL) |

## 10. tmux

**What It Is:**  
A terminal multiplexer that lets you manage multiple terminal sessions in one window.

**Why You Need It:**
- Persistent sessions even after disconnecting
- Customizable layouts and key bindings

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install tmux

# macOS:
brew install tmux
```

**Compatibility:**

| Platform         | Availability & Notes                                     |
|------------------|----------------------------------------------------------|
| Linux            | Yes                                                      |
| macOS            | Yes (via Homebrew)                                       |
| Windows (PS/WSL) | Yes (via WSL or using Windows Terminal with tmux in WSL) |

## 11. speedtest-cli

**What It Is:**  
A command-line interface for testing internet bandwidth using speedtest.net.

**Why You Need It:**
- Quickly measure your network’s download and upload speeds
- Useful for troubleshooting connectivity issues

**Installation:**
```sh
pip install speedtest-cli
```

**Compatibility:**

| Platform         | Availability & Notes              |
|------------------|-----------------------------------|
| Linux            | Yes (via pip or package managers) |
| macOS            | Yes (via pip or Homebrew)         |
| Windows (PS/WSL) | Yes (via pip)                     |

## 12. jq

**What It Is:**  
A lightweight and flexible command-line JSON processor.

**Why You Need It:**
- Parse and transform JSON data easily
- Ideal for working with API responses

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install jq

# macOS:
brew install jq
```

**Compatibility:**

| Platform         | Availability & Notes          |
|------------------|-------------------------------|
| Linux            | Yes                           |
| macOS            | Yes (via Homebrew)            |
| Windows (PS/WSL) | Yes (via Chocolatey or Scoop) |

## 13. yq

**What It Is:**  
A portable command-line YAML processor (similar to jq for JSON).

**Why You Need It:**
- Edit and query YAML files with ease
- Perfect for configuration management tasks

**Installation:**
```sh
# Debian/Ubuntu:
sudo snap install yq

# macOS:
brew install yq
```

**Compatibility:**

| Platform         | Availability & Notes        |
|------------------|-----------------------------|
| Linux            | Yes (via snap or binaries)  |
| macOS            | Yes (via Homebrew)          |
| Windows (PS/WSL) | Yes (via Chocolatey or WSL) |

## 14. tig

**What It Is:**  
A text-mode interface for Git, providing a visual history and repository browsing.

**Why You Need It:**
- Streamlined Git repository navigation
- Visualize branches, commits, and changes interactively

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install tig

# macOS:
brew install tig
```

**Compatibility:**

| Platform         | Availability & Notes    |
|------------------|-------------------------|
| Linux            | Yes                     |
| macOS            | Yes (via Homebrew)      |
| Windows (PS/WSL) | Yes (via WSL or Cygwin) |

## 15. lazygit

**What It Is:**  
A simple terminal UI for Git commands that offers a streamlined workflow.

**Why You Need It:**
- Simplifies Git operations with an intuitive interface
- Great for quickly staging, committing, and reviewing changes

**Installation:**
```sh
# macOS:
brew install lazygit

# For other platforms, check releases on GitHub.
```

**Compatibility:**

| Platform         | Availability & Notes                   |
|------------------|----------------------------------------|
| Linux            | Yes (via binaries or package managers) |
| macOS            | Yes (via Homebrew)                     |
| Windows (PS/WSL) | Yes (via binaries, Scoop, or WSL)      |

## 16. ranger

**What It Is:**  
A text-based file manager with VI key bindings that makes directory navigation a breeze.

**Why You Need It:**
- Visual directory tree in your terminal
- Quick file previews and efficient file management

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install ranger

# macOS:
brew install ranger
```

**Compatibility:**

| Platform         | Availability & Notes    |
|------------------|-------------------------|
| Linux            | Yes                     |
| macOS            | Yes (via Homebrew)      |
| Windows (PS/WSL) | Yes (via WSL or Cygwin) |

## 17. httpie

**What It Is:**  
A user-friendly command-line HTTP client that’s a more intuitive alternative to `curl`.

**Why You Need It:**
- Simple syntax for making HTTP requests
- Colorized output for easier reading of responses

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install httpie

# macOS:
brew install httpie
```

**Compatibility:**

| Platform         | Availability & Notes        |
|------------------|-----------------------------|
| Linux            | Yes                         |
| macOS            | Yes (via Homebrew)          |
| Windows (PS/WSL) | Yes (via Chocolatey or pip) |

## 18. asciinema

**What It Is:**  
A tool for recording and sharing terminal sessions as high-quality, text-based animations.

**Why You Need It:**
- Record and share your terminal workflows
- Great for tutorials, debugging sessions, and presentations

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install asciinema

# macOS:
brew install asciinema
```

**Compatibility:**

| Platform         | Availability & Notes                     |
|------------------|------------------------------------------|
| Linux            | Yes                                      |
| macOS            | Yes (via Homebrew)                       |
| Windows (PS/WSL) | Yes (via WSL; native support is limited) |

## 19. figlet

**What It Is:**  
A program for creating large letters out of ordinary text, perfect for banners and fun messages.

**Why You Need It:**
- Easily generate ASCII art text
- Add flair to your terminal scripts and presentations

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install figlet

# macOS:
brew install figlet
```

**Compatibility:**

| Platform         | Availability & Notes    |
|------------------|-------------------------|
| Linux            | Yes                     |
| macOS            | Yes (via Homebrew)      |
| Windows (PS/WSL) | Yes (via WSL or Cygwin) |

## 20. lolcat

**What It Is:**  
A tool that adds rainbow coloring to your text output, making your terminal output more vibrant.

**Why You Need It:**
- Fun, colorful output for scripts and log files
- Great for adding a bit of personality to your terminal

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install lolcat

# macOS:
brew install lolcat
```

**Compatibility:**

| Platform         | Availability & Notes        |
|------------------|-----------------------------|
| Linux            | Yes                         |
| macOS            | Yes (via Homebrew)          |
| Windows (PS/WSL) | Yes (via WSL or Chocolatey) |

## 21. cmus

**What It Is:**  
A small, fast, and powerful console music player with a text-based interface.

**Why You Need It:**
- Enjoy music directly in your terminal
- Lightweight and efficient for low-resource systems

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install cmus

# macOS:
brew install cmus
```

**Compatibility:**

| Platform         | Availability & Notes                             |
|------------------|--------------------------------------------------|
| Linux            | Yes                                              |
| macOS            | Yes (via Homebrew)                               |
| Windows (PS/WSL) | Yes (via WSL; native Windows support is limited) |

## 22. nmap

**What It Is:**  
A network exploration and security auditing tool that can scan for open ports and services.

**Why You Need It:**
- Detailed network mapping and security analysis
- Ideal for system administrators and security professionals

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install nmap

# macOS:
brew install nmap
```

**Compatibility:**

| Platform         | Availability & Notes                     |
|------------------|------------------------------------------|
| Linux            | Yes                                      |
| macOS            | Yes (via Homebrew)                       |
| Windows (PS/WSL) | Yes (via native installer or Chocolatey) |

## 23. iperf3

**What It Is:**  
A tool for measuring network performance, including throughput and latency.

**Why You Need It:**
- Evaluate network bandwidth and performance
- Diagnose network issues in real time

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install iperf3

# macOS:
brew install iperf3
```

**Compatibility:**

| Platform         | Availability & Notes               |
|------------------|------------------------------------|
| Linux            | Yes                                |
| macOS            | Yes (via Homebrew)                 |
| Windows (PS/WSL) | Yes (via native installers or WSL) |

## 24. mycli

**What It Is:**  
A command-line interface for MySQL that offers auto-completion and syntax highlighting.

**Why You Need It:**
- Enhances productivity with smart auto-completion
- Makes managing databases more interactive and enjoyable

**Installation:**
```sh
pip install mycli
```

**Compatibility:**

| Platform         | Availability & Notes                               |
|------------------|----------------------------------------------------|
| Linux            | Yes (via pip)                                      |
| macOS            | Yes (via pip)                                      |
| Windows (PS/WSL) | Yes (via pip; works in native Python environments) |

## 25. pgcli

**What It Is:**  
A similar tool to mycli, but for PostgreSQL, with rich auto-completion and colorized output.

**Why You Need It:**
- Improves efficiency when working with PostgreSQL
- Features intelligent suggestions for SQL commands

**Installation:**
```sh
pip install pgcli
```

**Compatibility:**

| Platform         | Availability & Notes |
|------------------|----------------------|
| Linux            | Yes (via pip)        |
| macOS            | Yes (via pip)        |
| Windows (PS/WSL) | Yes (via pip)        |

## 26. broot

**What It Is:**  
A new way to navigate directories that provides a tree-view along with an interactive search interface.

**Why You Need It:**
- Quickly locate files and directories
- Offers a dynamic and visually appealing alternative to `find`

**Installation:**
```sh
# macOS:
brew install broot

# For Linux and Windows, check GitHub releases.
```

**Compatibility:**

| Platform         | Availability & Notes                          |
|------------------|-----------------------------------------------|
| Linux            | Yes (via GitHub releases or package managers) |
| macOS            | Yes (via Homebrew)                            |
| Windows (PS/WSL) | Yes (via GitHub releases; WSL recommended)    |

## 27. glances

**What It Is:**  
A cross-platform monitoring tool that provides a comprehensive overview of your system’s performance.

**Why You Need It:**
- Real-time system monitoring for CPU, memory, disk I/O, and more
- Easy-to-read dashboard with a wealth of performance data

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install glances

# macOS:
brew install glances
```

**Compatibility:**

| Platform         | Availability & Notes    |
|------------------|-------------------------|
| Linux            | Yes                     |
| macOS            | Yes (via Homebrew)      |
| Windows (PS/WSL) | Yes (via pip or in WSL) |

## 28. s-tui

**What It Is:**  
A terminal UI for monitoring and stress-testing your system’s CPU, temperature, frequency, and power consumption.

**Why You Need It:**
- Visual performance monitoring under load
- Helps diagnose thermal issues and CPU throttling

**Installation:**
```sh
# Debian/Ubuntu:
sudo apt install s-tui

# macOS (via pip):
pip install s-tui
```

**Compatibility:**

| Platform         | Availability & Notes                     |
|------------------|------------------------------------------|
| Linux            | Yes                                      |
| macOS            | Yes (via pip)                            |
| Windows (PS/WSL) | Yes (via WSL; native support is limited) |

## 29. btop

**What It Is:**  
A resource monitor that provides an attractive, real-time view of system performance, similar to htop but with a modern twist.

**Why You Need It:**
- Beautiful and intuitive interface
- Monitors CPU, memory, disks, network, and processes in real time

**Installation:**
```sh
# macOS:
brew install btop

# For Linux, check GitHub releases.
```

**Compatibility:**

| Platform         | Availability & Notes                                  |
|------------------|-------------------------------------------------------|
| Linux            | Yes (via GitHub releases or package managers)         |
| macOS            | Yes (via Homebrew)                                    |
| Windows (PS/WSL) | Yes (via WSL; native version not typically available) |

## 30. dust

**What It Is:**  
A more intuitive alternative to `du` (disk usage), designed to show which directories are consuming the most space.

**Why You Need It:**
- Fast and easy-to-read disk usage reports
- Helps you quickly identify space-heavy directories

**Installation:**
```sh
# macOS:
brew install dust

# Debian/Ubuntu (via cargo or prebuilt binary):
cargo install du-dust
```

**Compatibility:**

| Platform         | Availability & Notes                                |
|------------------|-----------------------------------------------------|
| Linux            | Yes (via cargo or binaries)                         |
| macOS            | Yes (via Homebrew)                                  |
| Windows (PS/WSL) | Yes (via WSL; native support via cargo is possible) |

## Conclusion

Expanding your terminal toolkit with these 30 non-standard commands can dramatically enhance your workflow—from system monitoring and file management to network diagnostics and developer productivity. Each tool offers unique advantages that can streamline everyday tasks and make your command-line experience more powerful and enjoyable.

Be sure to check the compatibility tables for each tool to find the best installation method for your platform—whether you’re on Linux, macOS, or Windows (via PowerShell/WSL).

Have you already integrated some of these tools into your routine, or are you excited to try something new? Share your favorites or any other hidden gems in the comments below!

Happy hacking!
