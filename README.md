# Custom Command Line Interpreter (Shell) in C

A lightweight, modular, and extensible Unix-like shell written in C — built from scratch to mimic core functionalities of Bash, including command execution, piping, redirection, aliasing, history management, wildcard expansion, and signal handling.

---

##  Features

-  **Basic Command Execution**
  - Executes all Unix binaries using `fork()` + `execvp()`
  - Supports background jobs (`&`)

-  **Piping**
  - Full support for command pipelines: `ls | grep txt | sort`

-  **I/O Redirection**
  - Input: `< file.txt`
  - Output: `> out.txt`
  - Append: `>> log.txt`

-  **History Management**
  - Stores command history in memory using a linked list
  - Re-execute commands with `history <number>`

-  **Alias Management**
  - Create aliases: `createalias lsl "ls -l";`
  - View all: `aliases`
  - Delete: `destroyalias lsl`
  - Aliases are **persisted** across sessions (`~/.aliases`)

-  **Wildcard Expansion**
  - Automatically expands patterns like `*.c`, `file?.txt` using `glob()`

-  **Signal Handling**
  - Handles `Ctrl+C` and `Ctrl+Z` gracefully
  - Prevents shell from crashing or exiting unexpectedly

-  **Built-in Commands**
  - `cd <dir>` – change working directory
  - `ver` – show shell version (`mySH version 1.0.0`)
  - `history`, `createalias`, `destroyalias`, `aliases`

---

##  Project Structure

```
Command-Line-Interpreter/
├── main.c              # Main shell loop
├── executor.c          # Handles execvp(), fork(), redirection
├── pipeline.c          # Handles piped commands
├── parser.c            # Tokenizes input, handles wildcards
├── redirection.c       # Handles <, >, >> using dup/open
├── alias.c             # Hash table implementation with file I/O
├── history.c           # Linked list for command history
├── signals.c           # Signal handlers for SIGINT/SIGTSTP
├── includes.h          # Shared definitions and macros
└── Makefile
```

---

##  Installation

```bash
git clone https://github.com/your-username/Command-Line-Interpreter.git
cd Command-Line-Interpreter
make
```

---

##  Usage

Launch the shell:

```bash
./mysh
```

Try commands like:

```bash
ls -l
cd ..
history
createalias gs "git status";
aliases
cat < file.txt | grep error > out.txt
```

---

##  How It Works

Internally, the shell:

- Uses `fork()` and `execvp()` to run commands
- Detects and handles `|`, `<`, `>`, and `>>` with custom logic
- Supports wildcard expansion using `glob()`
- Stores and loads aliases from `~/.aliases`
- Tracks history using a linked list and allows re-execution
- Catches signals using `signal()` to improve UX

---

##  Future Improvements

- [ ] Job control (`jobs`, `fg`, `bg`)
- [ ] `.myshrc` config file for alias autoload
- [ ] Persistent history (`~/.mysh_history`)
- [ ] Tab auto-completion using `readline`
- [ ] Scripting support (read commands from `.sh` files)
