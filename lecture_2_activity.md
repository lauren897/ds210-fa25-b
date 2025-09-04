
# In-Class Activity: Shell Challenge

## In Class Activity Part 1: Access/Install Terminal Shell

Directions for [MacOS Users](#macos-users) and [Windows Users](#windows-users).

### macOS Users:

Your Mac already has a terminal! Here's how to access it:

1. **Open Terminal:**
   - Press `Cmd + Space` to open Spotlight
   - Type "Terminal" and press Enter
   - Or: Applications → Utilities → Terminal

2. **Check Your Shell:**
   ```bash
   echo $SHELL
   # Modern Macs use zsh, older ones use bash
   ```

3. **Optional: Install Better Tools:**

Install Homebrew (package manager for macOS)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Install useful tools

```bash
brew install tree      # Visual directory structure
```

```bash
brew install ripgrep   # Fast text search
```

### Windows Users:

Windows has several terminal options. For this exercise we recommend Option 1, Git bash.

When you have more time, you might want to explore Windows Subsystem for Linux
so you can have a full, compliant linux system accessible on Windows.

PowerShell aliases some commands to be Linux-like, but they are fairly quirky.

We recommend Git Bash or WSL:

1. **Option A: Git Bash (Easier)**
   - Download Git for Windows from [git-scm.com](https://git-scm.com/)
   - During installation, select "Use Git and optional Unix tools from the Command Prompt"
   - Open "Git Bash" from Start menu
   - This gives you Unix-like commands on Windows

2. **Option B: Windows Subsystem for Linux (WSL)**
   ```powershell
   # Run PowerShell as Administrator, then:
   wsl --install
   # Restart your computer
   # Open "Ubuntu" from Start menu
   ```

3. **Option C: PowerShell (Built-in)**
   - Press `Win + X` and select "PowerShell"
   - Note: Commands differ from Unix (use `dir` instead of `ls`, etc.)
   - Not recommended for the in-class activities.

## Verify Your Setup (Both Platforms)

```bash
pwd              # Should show your current directory
ls               # Should list files (macOS/Linux) or use 'dir' (PowerShell)
which ls         # Should show path to ls command (if available)
echo "Hello!"    # Should print Hello!
```

## Part 2: Scavenger Hunt

Complete the steps **using only the command line!**

You can use `echo` to write to the file, or text editor `nano`.

Feel free to reference the cheat sheet below and the notes above.

0. Create a folder for the course if you haven't!

1. Create a directory called `treasure_hunt` in your course projects folder.

2. In that directory create a file called `command_line_scavenger_hunt.txt` that contains the following:
   - Your name / group members

3. Run these lines and record the output into that `.txt` file:
```bash
whoami                    # What's your username?
hostname                  # What's your computer's name?
pwd                      # Where do you start?
echo $HOME               # What's your home directory path?
```

4. Inside that directory, create a text file named `clue_1.txt` with the content "The treasure is hidden in plain sight"

5. Create a subdirectory called `secret_chamber`

6. In the `secret_chamber` directory, create a file called `clue_2.txt` with the content "Look for a hidden file"

7. Create a hidden file in the `secret_chamber` directory called `.treasure_map.txt` with the content "Congratulations. You found the treasure"


8. When you're done, change to the parent directory of `treasure_hunt` and run
the command `zip -r treasure_hunt.zip treasure_hunt`.
   - Or if you are on Git Bash, you may have to use the command `tar.exe -a -c -f treasure_hunt.zip treasure_hunt`

9. Upload `treasure_hunt.zip` to gradescope - next time we will introduce git and github and use that platform going forward.


10. **Optional: For Bragging Rights**  Create a shell script that does all of the above commands
and upload that to Gradescope as well.

---

# Command Line Cheat Sheet

## Basic Navigation & Listing

```bash
# Navigate directories
cd ~                    # Go to home directory
cd /path/to/directory   # Go to specific directory
pwd                     # Show current directory

# List files and directories
ls                      # List files
ls -la                  # List all files (including hidden) with details
ls -lh                  # List with human-readable file sizes
ls -t                   # List sorted by modification time
```

## Finding Files
```bash
# Find files by name
find /home -name "*.pdf"           # Find all PDF files in /home
find . -type f -name "*.log"       # Find log files in current directory
find /usr -type l                  # Find symbolic links

# Find files by other criteria
find . -type f -size +1M           # Find files larger than 1MB
find . -mtime -7                   # Find files modified in last 7 days
find . -maxdepth 3 -type d         # Find directories up to 3 levels deep
```



## Counting & Statistics

```bash
# Count files
find . -name "*.pdf" | wc -l       # Count PDF files
ls -1 | wc -l                      # Count items in current directory

# File and directory sizes
du -sh ~/Documents                 # Total size of Documents directory
du -h --max-depth=1 /usr | sort -rh  # Size of subdirectories, largest first
ls -lah                            # List files with sizes
```


## Text Processing & Search

```bash
# Search within files
grep -r "error" /var/log           # Search for "error" recursively
grep -c "hello" file.txt           # Count occurrences of "hello"
grep -n "pattern" file.txt         # Show line numbers with matches

# Count lines, words, characters
wc -l file.txt                     # Count lines
wc -w file.txt                     # Count words
cat file.txt | grep "the" | wc -l  # Count lines containing "the"
```


## System Information

```bash
# System stats
df -h                              # Disk space usage
free -h                            # Memory usage (Linux)
system_profiler SPHardwareDataType # Hardware info (Mac)
uptime                             # System uptime
who                                # Currently logged in users

# Process information
ps aux                             # List all processes
ps aux | grep chrome               # Find processes containing "chrome"
ps aux | wc -l                     # Count total processes
```

## File Permissions & Properties

```bash
# File permissions and details
ls -l filename                     # Detailed file information
stat filename                     # Comprehensive file statistics
file filename                     # Determine file type

# Find files by permissions
find . -type f -readable           # Find readable files
find . -type f ! -executable       # Find non-executable files
```

## Network & Hardware

```bash
# Network information
ip addr show                       # Show network interfaces (Linux)
ifconfig                          # Network interfaces (Mac/older Linux)
networksetup -listallhardwareports # Network interfaces (Mac)
cat /proc/cpuinfo                 # CPU information (Linux)
system_profiler SPHardwareDataType # Hardware info (Mac)
```


## Platform-Specific Tips

### Mac/Linux Users:
- Your home directory is `~` or `$HOME`
- Hidden files start with a dot (.)
- Use `man command` for detailed help
- Try `which command` to find where a command is located

### Windows Users:
- Your home directory is `%USERPROFILE%` (Command Prompt) or `$env:USERPROFILE` (PowerShell)
- Hidden files have the hidden attribute (use `dir /ah` to see them)
- Use `Get-Help command` in PowerShell or `help command` in Command Prompt for detailed help
- Try `where command` to find where a command is located

### Universal Tips:
- Use Tab completion to avoid typing long paths
- Most shells support command history (up arrow or Ctrl+R)
- Combine commands with pipes (`|`) to chain operations
- Search online for "[command name] [your OS]" for specific examples


