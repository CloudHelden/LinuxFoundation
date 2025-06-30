# Linux Command Reference Sheet

## 🎯 Quick Reference Format
Each command shows: `command [options] <required> [optional]`

---

## 📁 Navigation Commands

### pwd - Print Working Directory
```bash
pwd                     # Show current directory
```
**Remember**: "Where am I?"

### cd - Change Directory
```bash
cd                      # Go home
cd ~                    # Go home (explicit)
cd /path/to/dir        # Go to specific path
cd ..                   # Go up one level
cd ../..               # Go up two levels
cd -                    # Go to previous directory
```
**Remember**: "cd" = "change directory"

### ls - List
```bash
ls                      # List files
ls -l                   # Long format (details)
ls -a                   # All files (including hidden)
ls -la                  # Combine options
ls -lh                  # Human readable sizes
ls -lt                  # Sort by time
ls /path/to/dir        # List specific directory
```
**Remember**: "ls" = "list"

---

## 📝 File Operations

### touch - Create/Update File
```bash
touch filename          # Create empty file
touch file1 file2      # Create multiple files
```
**Remember**: "Touch to create"

### cp - Copy
```bash
cp source dest         # Copy file
cp -r source dest      # Copy directory (recursive)
cp -i source dest      # Interactive (ask before overwrite)
```
**Remember**: "cp" = "copy"

### mv - Move/Rename
```bash
mv oldname newname     # Rename file
mv file /path/to/      # Move file
mv -i source dest      # Interactive mode
```
**Remember**: "mv" = "move"

### rm - Remove
```bash
rm filename            # Delete file
rm -i filename         # Confirm before delete
rm -r directory        # Delete directory
rm -rf directory       # Force delete (DANGEROUS!)
```
**Remember**: "rm" = "remove" (NO UNDO!)

### mkdir - Make Directory
```bash
mkdir dirname          # Create directory
mkdir -p path/to/dir   # Create parent directories too
```
**Remember**: "mkdir" = "make directory"

---

## 👀 Viewing Files

### cat - Concatenate/Display
```bash
cat filename           # Show entire file
cat file1 file2       # Show multiple files
```
**Remember**: "Cat shows all"

### less - Page Through File
```bash
less filename          # View with pagination
# Inside less:
# Space = next page
# b = previous page
# / = search
# q = quit
```
**Remember**: "Less is more (controlled)"

### head - Show Beginning
```bash
head filename          # First 10 lines
head -n 20 filename   # First 20 lines
```
**Remember**: "Head = top"

### tail - Show End
```bash
tail filename          # Last 10 lines
tail -n 20 filename   # Last 20 lines
tail -f filename      # Follow/watch file
```
**Remember**: "Tail = bottom"

---

## 🔍 Searching

### grep - Search in Files
```bash
grep "text" filename   # Find text in file
grep -i "text" file   # Case insensitive
grep -n "text" file   # Show line numbers
grep -r "text" dir/   # Search in directory
```
**Remember**: "Grep grabs patterns"

### find - Find Files
```bash
find . -name "*.txt"   # Find by name
find / -type f         # Find only files
find / -type d         # Find only directories
find . -size +1M       # Find files larger than 1MB
```
**Remember**: "Find finds files"

---

## ℹ️ Getting Help

### man - Manual Pages
```bash
man command            # Show manual for command
man -k keyword        # Search manuals
```
**Navigation**: Space=forward, b=back, q=quit

### help - Built-in Help
```bash
command --help         # Quick help
help command          # For shell built-ins
```

### which - Find Command Location
```bash
which command          # Show path to command
```

### type - Show Command Type
```bash
type command           # Show what command is
```

---

## 🚀 Productivity Shortcuts

### History
```bash
history                # Show command history
!!                    # Run last command
!n                    # Run command number n
!text                 # Run last command starting with 'text'
```

### Tab Completion
```bash
comm[TAB]             # Complete command
/ho[TAB]/us[TAB]     # Complete path
```

### Wildcards
```bash
*                     # Match any characters
?                     # Match single character
[abc]                 # Match a, b, or c
[0-9]                 # Match any digit
```

---

## ⚡ Essential Combinations

### Pipes and Redirection
```bash
command1 | command2    # Pipe output to next command
command > file        # Redirect output to file
command >> file       # Append output to file
command < file        # Read input from file
command 2> error.log  # Redirect errors
```

### Common Combos
```bash
ls -la | grep ".txt"   # List only txt files
ps aux | grep process  # Find running process
history | grep cd      # Find cd commands
cat file | less        # Page through file
```

---

## 🔧 System Information

### System Info
```bash
uname -a               # System information
hostname              # Show hostname
whoami                # Current username
id                    # User and group IDs
date                  # Current date/time
uptime                # System uptime
```

### Disk and Memory
```bash
df -h                 # Disk free space
du -h                 # Disk usage
free -h               # Memory usage
```

### Process Commands
```bash
ps                    # Your processes
ps aux                # All processes
top                   # Interactive process viewer
kill PID              # Stop process
```

---

## 💡 Pro Tips for Beginners

### Safety First
1. **Always use `ls` before `rm`**
2. **Use `-i` flag for interactive confirmation**
3. **Make backups before big changes**
4. **Read error messages carefully**

### Learning Path
1. **Master navigation first** (cd, ls, pwd)
2. **Then file operations** (cp, mv, rm)
3. **Then viewing** (cat, less, head, tail)
4. **Finally searching** (grep, find)

### Memory Tricks
- **pwd** = "print working directory" = "where?"
- **cd** = "change directory" = "go to"
- **ls** = "list" = "show me"
- **cp** = "copy" = "duplicate"
- **mv** = "move" = "relocate/rename"
- **rm** = "remove" = "delete forever!"

### Practice Commands
```bash
# Safe practice area
mkdir ~/playground
cd ~/playground
# Practice here!
```

---

## 📋 Command Checklist

### Week 1 Essentials
- [ ] pwd - Know where you are
- [ ] ls - See what's there
- [ ] cd - Move around
- [ ] mkdir - Create directories
- [ ] touch - Create files
- [ ] cp - Copy stuff
- [ ] mv - Move/rename stuff
- [ ] rm - Delete (carefully!)
- [ ] cat - View files
- [ ] man - Get help

### Week 2 Goals
- [ ] grep - Search in files
- [ ] find - Find files
- [ ] less - View large files
- [ ] head/tail - View parts
- [ ] | - Use pipes
- [ ] > - Redirect output

---

**Print this sheet and keep it handy during exercises!**