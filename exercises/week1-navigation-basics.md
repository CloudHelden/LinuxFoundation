# Week 1: Navigation Basics Exercises

## Exercise Set Overview
**Time**: 60 minutes  
**Difficulty**: Dual-track  
**Prerequisites**: Completed Day 1-2 lessons

---

## 🟢 Track A: Foundations Exercises

### Exercise A1: Directory Explorer (20 min)
**Objective**: Master basic navigation commands

#### Part 1: Where Am I?
```bash
# 1. Check your current location
pwd

# 2. What do you see in the output?
# Write your answer: ________________

# 3. Go to your home directory (3 different ways)
cd
cd ~
cd $HOME

# 4. Verify you're home
pwd
```

#### Part 2: Moving Around
```bash
# 1. Go to the root directory
cd /

# 2. List what's there
ls

# 3. Go to /etc directory
cd etc

# 4. Go back to previous directory
cd -

# 5. Go up one level
cd ..
```

#### Part 3: Creating Your Workspace
```bash
# 1. Go home
cd

# 2. Create a directory structure:
mkdir linux101
cd linux101
mkdir exercises
mkdir projects
mkdir notes

# 3. Verify your structure
ls
tree  # If tree is installed
```

**Success Checklist:**
- [ ] Can use pwd without thinking
- [ ] Understand difference between / and ~
- [ ] Can navigate up and down directories
- [ ] Created organized workspace

### Exercise A2: Listing Files (20 min)
**Objective**: Understand ls options

#### Guided Discovery:
```bash
# 1. Basic listing
cd /etc
ls

# 2. Detailed listing
ls -l
# Question: What do the columns mean?

# 3. Show hidden files
cd ~
ls -a
# Question: What files start with dot?

# 4. Human readable sizes
ls -lh
# Question: What changed?

# 5. Sort by time
ls -lt
# Question: Which file is newest?
```

#### Practice Tasks:
1. Find the largest file in /var/log
2. List only directories in /etc
3. Show hidden files in your home
4. Count files in /bin

**Hints Box:**
```
Remember:
- Hidden files start with .
- ls -la combines options
- Use man ls for help
```

### Exercise A3: Getting Help (20 min)
**Objective**: Learn to find information

#### Help Methods:
```bash
# Method 1: Manual pages
man ls
# Navigation: Space=next, q=quit

# Method 2: Help flag
ls --help

# Method 3: Command info
info ls

# Method 4: Which and Type
which ls
type ls
```

#### Scavenger Hunt:
Using help, find out:
1. How to list files in reverse order
2. How to show file sizes in bytes
3. What ls -R does
4. How to list only directories

**Answer Template:**
```
1. Reverse order: ls _____
2. Size in bytes: ls _____
3. ls -R does: ___________
4. Only directories: _____
```

---

## 🔵 Track B: Accelerated Exercises

### Exercise B1: Advanced Navigation (20 min)
**Objective**: Efficient filesystem navigation

#### Speed Challenge:
```bash
# Setup (run this first):
mkdir -p ~/maze/{level1/{room1,room2},level2/{room3,room4}}
touch ~/maze/level1/room1/{key1,door1}
touch ~/maze/level2/room3/{treasure,trap}

# Now navigate and complete tasks:
# 1. Find all files containing 'key' (one command)
# 2. List all directories only (no files)
# 3. Show full path of all 'treasure' files
# 4. Count total files in maze
```

#### Power Navigation:
```bash
# Use these advanced techniques:
# 1. Jump to previous directory
cd -

# 2. Use CDPATH
export CDPATH=.:~:/etc:/var
cd log  # Goes to /var/log

# 3. Quick substitution
cd /var/log
cd log tmp  # Changes to /var/tmp

# 4. Stack directories
pushd /etc
pushd /var
popd
```

### Exercise B2: Command Combinations (20 min)
**Objective**: Chain commands effectively

#### Pipeline Practice:
```bash
# 1. Find 10 largest files in /usr
ls -la /usr/bin | sort -k5 -n -r | head -10

# 2. Count unique file extensions in /etc
ls /etc | grep '\.' | sed 's/.*\.//' | sort | uniq -c

# 3. Find recently modified configs
find /etc -name "*.conf" -mtime -7 2>/dev/null

# 4. Create directory report
echo "=== System Directories ===" > ~/report.txt
ls -ld /etc /var /usr >> ~/report.txt
```

#### Challenge Tasks:
1. Write a one-liner to find all PDF files in home
2. List top 5 space-consuming directories
3. Find all files modified in last hour
4. Create directory tree visualization

### Exercise B3: Efficiency Tools (20 min)
**Objective**: Work faster with shortcuts

#### Setup Your Environment:
```bash
# 1. Create useful aliases
echo "alias ll='ls -la'" >> ~/.bashrc
echo "alias ..='cd ..'" >> ~/.bashrc
echo "alias ...='cd ../..'" >> ~/.bashrc
source ~/.bashrc

# 2. History shortcuts
history | tail -20
!ls  # Run last ls command
!!   # Run last command
!$   # Use last argument

# 3. Tab completion mastery
cd /u[TAB]/lo[TAB]/sh[TAB]

# 4. Glob patterns
ls *.conf
ls [a-c]*
ls {*.txt,*.log}
```

#### Productivity Challenge:
Create a command that:
1. Finds all log files
2. Shows only today's files
3. Displays size and path
4. Saves result to report

**Bonus**: Make it an alias!

---

## 📊 Assessment Rubric

### Track A Success Criteria:
- Complete 3 exercises: **Pass**
- Use help effectively: **+Bonus**
- No syntax errors: **Good**
- Explains what commands do: **Excellent**

### Track B Success Criteria:
- Complete core + 2 challenges: **Pass**
- Efficient solutions: **Good**
- Creative approaches: **Excellent**
- Helps Track A student: **+Bonus**

## 🤝 Pair Programming Option

### Mixed Pairs (A+B):
- B student guides without taking over
- A student types all commands
- Both explain what's happening
- Switch roles every 10 minutes

### Same Track Pairs:
- Take turns being "driver" and "navigator"
- Discuss before typing
- Challenge each other
- Share discoveries

## 📝 Reflection Questions

### For Everyone:
1. What was the most useful command you learned?
2. What confused you the most?
3. How will you remember these commands?
4. What would you like to explore more?

### Track A Additional:
- Which help method do you prefer?
- Draw your mental map of the filesystem

### Track B Additional:
- What efficiency tip saves most time?
- Design a complex pipeline for a real task

---

## 🏠 Homework

### Track A:
1. Practice navigation for 15 min daily
2. Explore one new directory each day
3. Use `man` for one new command daily

### Track B:
1. Create 5 useful aliases
2. Write script to organize downloads
3. Explore `find` command in depth

## 💡 Tips for Success

### Universal Tips:
- **Practice daily**: Even 10 minutes helps
- **Make mistakes**: They're learning opportunities
- **Ask questions**: No question is stupid
- **Take notes**: In your own words

### Track-Specific:
- **Track A**: Focus on accuracy over speed
- **Track B**: Challenge yourself with constraints

---

**Remember**: The goal isn't to finish first, but to understand deeply!