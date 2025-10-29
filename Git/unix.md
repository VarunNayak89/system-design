# 🐧 The 50 Most Popular Linux & Terminal Commands

A quick-reference guide for beginners learning essential **Linux commands** and **VI editor operations**.

---

## 📂 Basic Linux Commands

| Command | Description |
|----------|--------------|
| `ls` | Lists all files and directories in the present working directory |
| `ls -R` | Lists files in sub-directories as well |
| `ls -a` | Lists hidden files as well |
| `ls -al` | Lists files and directories with detailed information like permissions, size, owner, etc. |
| `cd` or `cd ~` | Navigate to HOME directory |
| `cd ..` | Move one level up |
| `cd [directory]` | Change to a particular directory |
| `cd /` | Move to the root directory |
| `cat > filename` | Creates a new file |
| `cat filename` | Displays the file content |
| `cat file1 file2 > file3` | Joins two files (`file1`, `file2`) and stores the output in a new file (`file3`) |
| `mv file "new file path"` | Moves the file to a new location |
| `mv filename new_file_name` | Renames the file |
| `sudo` | Allows regular users to run programs with superuser privileges |
| `rm filename` | Deletes a file |
| `man [command]` | Displays help information for a command |
| `history` | Shows a list of all past commands in the current terminal session |
| `clear` | Clears the terminal screen |
| `touch index.html` | Creates a new file named `index.html` |
| `mkdir directoryname` | Creates a new directory |
| `rmdir directoryname` | Deletes a directory |
| `mv` | Renames a directory |
| `pr -x` | Divides the file into *x* columns |
| `pr -h` | Assigns a header to the file |
| `pr -n` | Numbers the lines of the file |
| `lp -nc` or `lpr c` | Prints “c” copies of the file |
| `lp -d` or `lp -P` | Specifies the name of the printer |
| `apt-get` | Installs and updates packages |
| `mail -s 'subject' -c 'cc-address' -b 'bcc-address' 'to-address'` | Sends an email |
| `mail -s "Subject" to-address < Filename` | Sends an email with an attachment |

---

## ✍️ VI Editing Commands

| Command | Description |
|----------|--------------|
| `i` | Insert at cursor (insert mode) |
| `a` | Write after cursor (insert mode) |
| `A` | Write at the end of line (insert mode) |
| `ESC` | Exit insert mode |
| `u` | Undo last change |
| `U` | Undo all changes to the entire line |
| `o` | Open a new line (insert mode) |
| `dd` | Delete current line |
| `3dd` | Delete 3 lines |
| `D` | Delete contents of line after the cursor |
| `C` | Delete contents of a line after the cursor and insert new text (press ESC to end) |
| `dw` | Delete word |
| `4dw` | Delete 4 words |
| `cw` | Change word |
| `x` | Delete character at cursor |
| `r` | Replace character |
| `R` | Overwrite characters from cursor onward |
| `s` | Substitute one character under cursor and continue inserting |
| `S` | Substitute entire line and begin inserting at line start |
| `~` | Change case of individual character |
| `:q!` | Quit without saving |
| `Shift+z+z` or `:wq` | Write file and quit |

---

## 🧠 Quick Tip

> Practice using these commands inside a Linux terminal or WSL (Windows Subsystem for Linux).  
> Start with navigation (`cd`, `ls`), file operations (`cat`, `touch`, `rm`), and gradually move to editors like `vi` and package management commands.

---

📘 **Reference:** *FreeCodeCamp - The 50 Most Popular Linux & Terminal Commands (Full Course for Beginners)*
