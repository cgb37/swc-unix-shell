# Command Glossary (one-line answers)

For "what does ___ mean?" Say the **bold** line. The note after it is the memory hook or the name's origin.

---

## Moving around and looking

| Command | Say this | Hook |
|---|---|---|
| `pwd` | **Shows which folder you're in right now.** | "print working directory" |
| `ls` | **Lists what's in a folder.** | "list" |
| `cd` | **Moves you into a different folder.** | "change directory". Alone, it takes you home. |
| `cd ..` | **Moves you up one folder.** | `..` = the folder above |
| `cd -` | **Jumps back to the folder you were just in.** | like a "back" button |
| `clear` | **Wipes the screen so it's tidy.** | history is not deleted |

## Getting help

| Command | Say this | Hook |
|---|---|---|
| `man` | **Opens the manual for a command.** | "manual". `q` to quit. Mac only. |
| `--help` | **Prints a short usage guide for a command.** | Git Bash: `ls --help` |
| `help` | **Explains the built-in commands like `cd`.** | `help cd` |
| `type` | **Tells you what a command name really is.** | e.g. `type ls` shows the alias |

## Making, copying, moving, deleting

| Command | Say this | Hook |
|---|---|---|
| `mkdir` | **Creates a new folder.** | "make directory" |
| `touch` | **Creates an empty file.** | also used to update a file's timestamp |
| `nano` | **A simple text editor that runs in the terminal.** | commands shown at the bottom; `^` = Ctrl |
| `cp` | **Copies a file or folder.** | "copy". Folders need `-r`. |
| `mv` | **Moves a file, or renames it.** | "move". Same command does both. |
| `rm` | **Deletes a file. There is no undo.** | "remove". No trash can. |

## Looking inside files

| Command | Say this | Hook |
|---|---|---|
| `cat` | **Prints a whole file on the screen.** | from "concatenate", meaning "join and print" |
| `less` | **Lets you scroll through a file page by page.** | `Space` = next page, `q` = quit |
| `head` | **Shows the first lines of a file.** | the "head" of the file. 10 lines by default. |
| `tail` | **Shows the last lines of a file.** | the "tail" of the file. 10 lines by default. |
| `wc` | **Counts lines, words and characters.** | "word count". `-l` = lines only. |

## Reshaping and searching data

| Command | Say this | Hook |
|---|---|---|
| `sort` | **Puts lines in order.** | `-n` = by number, not alphabet |
| `uniq` | **Collapses repeated neighbouring lines into one.** | sort first. `-c` = count each. |
| `cut` | **Pulls out one column from a table.** | `-d ,` = split at commas, `-f 2` = column 2 |
| `echo` | **Prints whatever you type after it.** | like "say" |
| `grep` | **Shows only the lines that contain a word or pattern.** | "search inside files" |
| `find` | **Finds files by name or type.** | "search for files" |
| `history` | **Lists the commands you've typed.** | `!!` = repeat the last one |

## Running things

| Command | Say this | Hook |
|---|---|---|
| `bash` | **Runs a script file, or starts a bash shell.** | `bash middle.sh` |
| `for … do … done` | **Repeats commands once for each item in a list.** | a loop |
| `explorer .` (Windows) | **Opens the current folder in File Explorer.** | Git Bash only |

---

## Symbols

| Symbol | Say this | Example |
|---|---|---|
| `.` | **"This folder."** | `cp file .` |
| `..` | **"The folder above."** | `cd ..` |
| `~` | **"My home folder."** | `cd ~` |
| `/` | **Separates folders in a path. A leading `/` means "from the very top."** | `/Users/nelle` |
| `*` | **Wildcard: matches any number of characters.** | `ls *.pdb` |
| `?` | **Wildcard: matches exactly one character.** | `ls ?ethane.pdb` |
| `>` | **Sends output into a file, replacing what was there.** | `ls > list.txt` |
| `>>` | **Adds output to the end of a file.** | `echo hi >> list.txt` |
| `\|` | **Passes one command's output to the next command.** | `ls \| wc -l` |
| `$` (prompt) | **The computer saying "I'm ready." Don't type it.** | |
| `$name` | **"The value stored in `name`."** | `echo $filename` |
| `$(...)` | **Runs the inside command first and pastes its output.** | `wc -l $(find . -name "*.txt")` |
| `$1`, `$2` | **First, second input to a script.** | `bash middle.sh octane.pdb 15 5` |
| `$@` | **All inputs given to a script.** | |
| `#` | **A comment: the computer ignores the rest of the line.** | |
| `;` | **Separates two commands on one line.** | `cd data; ls` |

---

## Options (flags)

| Option | Say this | Used with |
|---|---|---|
| `-F` | **Adds `/` to folders so you can tell them apart.** | `ls -F` |
| `-a` | **Includes hidden files too.** ("all") | `ls -a` |
| `-l` | **Long list: size, date, and more.** | `ls -l` |
| `-h` | **Human-readable sizes (K, M).** | `ls -lh` |
| `-r` | **Reverse the order.** In `cp`/`rm`: **go into folders too.** ("recursive") | `ls -r`, `cp -r`, `rm -r` |
| `-t` | **Sort by time.** | `ls -t` |
| `-p` | **Also create any missing parent folders.** | `mkdir -p a/b/c` |
| `-i` | **Ask before overwriting or deleting.** In `grep`: **ignore capitals.** | `rm -i`, `grep -i` |
| `-n` | **Number.** In `head`/`tail`: **how many lines.** In `sort`: **sort as numbers.** In `grep`: **show line numbers.** | `head -n 5` |
| `-w` | **Match whole words only.** | `grep -w` |
| `-v` | **Invert: show lines that do NOT match.** | `grep -v` |
| `-c` | **Count.** | `uniq -c` |
| `-d` | **Delimiter: the character that separates columns.** | `cut -d ,` |
| `-f` | **Field: which column to pick.** | `cut -f 2` |

---

## Keys

| Key | Say this |
|---|---|
| `Tab` | **Finishes a name for you. Press twice to see choices.** |
| `↑` | **Brings back your last command.** |
| `Ctrl+C` | **Stops whatever is running.** (Not "copy".) |
| `Ctrl+R` | **Searches your past commands.** |
| `Ctrl+O` / `Ctrl+X` (in nano) | **Save / Exit.** |
| `q` | **Quit** `man`, `less`. |

---

## Three words people ask about

| Word | Say this |
|---|---|
| **Shell** | **The program that reads what you type and runs it.** |
| **Terminal** | **The window that shows the shell.** |
| **Bash** | **The most common kind of shell** (macOS uses zsh, which behaves almost the same). |
| **Directory** | **A folder.** |
| **Path** | **The address of a file or folder, e.g. `Desktop/shell-lesson-data`.** |
| **Argument** | **What a command acts on**, e.g. the `Desktop` in `ls Desktop`. |
| **Option** | **A setting that changes how it acts**, e.g. the `-F` in `ls -F`. |
