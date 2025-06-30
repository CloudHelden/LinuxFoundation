# Interactive Lab: Linux Permissions

## 🎯 Lab Overview
**Duration**: 90 minutes  
**Type**: Hands-on Interactive  
**Difficulty**: Progressive (Easy → Hard)  
**Goal**: Master Linux permissions through practical scenarios

---

## 🏗️ Lab Setup Script

Run this first to create your lab environment:

```bash
#!/bin/bash
# Save as: setup-permissions-lab.sh
# Run with: bash setup-permissions-lab.sh

echo "🔧 Setting up Permissions Lab Environment..."

# Create lab directory
mkdir -p ~/permissions-lab/{company,projects,shared,personal}
cd ~/permissions-lab

# Create users simulation (using different groups)
echo "📁 Creating directory structure..."

# Company directories
mkdir -p company/{hr,finance,it,public}
mkdir -p projects/{alpha,beta,gamma}
mkdir -p shared/{documents,tools,reports}

# Create sample files
echo "📄 Creating sample files..."
echo "Employee Handbook" > company/public/handbook.txt
echo "Salary Data - CONFIDENTIAL" > company/hr/salaries.txt
echo "Budget 2024 - RESTRICTED" > company/finance/budget.txt
echo "Server Passwords - IT ONLY" > company/it/passwords.txt

echo "Project Alpha Specs" > projects/alpha/specs.txt
echo "Project Beta Code" > projects/beta/code.sh
echo "Project Gamma Data" > projects/gamma/data.csv

echo "Meeting Notes" > shared/documents/notes.txt
echo "#!/bin/bash\necho 'Backup Tool'" > shared/tools/backup.sh
echo "Q4 Report" > shared/reports/q4-report.txt

# Create a test script
cat > shared/tools/system-info.sh << 'EOF'
#!/bin/bash
echo "=== System Information Tool ==="
echo "User: $(whoami)"
echo "Groups: $(groups)"
echo "Date: $(date)"
echo "Uptime: $(uptime -p)"
EOF

echo "✅ Lab environment created in ~/permissions-lab/"
echo "📋 Ready to start exercises!"
```

---

## 📚 Part 1: Understanding Permissions (30 min)

### Exercise 1.1: Permission Basics

```bash
cd ~/permissions-lab

# Examine permissions
ls -la company/public/
```

#### 🤔 Questions:
1. What does `-rw-rw-r--` mean?
2. Who can read the handbook.txt?
3. Who can modify it?

<details>
<summary>📖 Quick Reference</summary>

```
Permission Format: -rwxrwxrwx
                   │├─┼─┼─┤
                   ││ │ │ └── Others (everyone else)
                   ││ │ └──── Group
                   ││ └────── User (owner)
                   │└──────── File type (- = file, d = directory)
                   │
Permissions: r = read (4), w = write (2), x = execute (1)
```

</details>

### Exercise 1.2: Numeric Notation

Calculate permissions for these scenarios:

```bash
# What numeric value gives:
# Owner: read, write, execute
# Group: read, execute
# Others: read only

# Try it:
touch test-file.txt
chmod ??? test-file.txt  # Replace ??? with your answer
ls -l test-file.txt
```

<details>
<summary>💡 Answer</summary>

```bash
chmod 754 test-file.txt
# 7 = rwx (4+2+1) for owner
# 5 = r-x (4+0+1) for group  
# 4 = r-- (4+0+0) for others
```

</details>

### Exercise 1.3: The Permission Game

```bash
# Create a file with specific permissions
touch game.txt
chmod 640 game.txt

# Now achieve these permissions using symbolic notation:
# -rw-r----- 
chmod u=??,g=?,o=? game.txt  # Fill in the blanks
```

---

## 🔐 Part 2: Practical Scenarios (30 min)

### Scenario 2.1: Secure the Passwords File

```bash
# The IT passwords file is currently readable by everyone!
ls -l company/it/passwords.txt

# Your task: Make it readable only by owner
# Try solving it yourself first!
```

<details>
<summary>🔑 Solution</summary>

```bash
chmod 600 company/it/passwords.txt
# OR
chmod u=rw,g=,o= company/it/passwords.txt

# Verify:
ls -l company/it/passwords.txt
# Should show: -rw-------
```

</details>

### Scenario 2.2: Shared Project Collaboration

```bash
# Project Alpha team needs to collaborate
# Requirements:
# - Team members can read and write specs.txt
# - Others can only read
# - Create a shared directory where team can add files

# Start here:
cd projects/alpha
```

<details>
<summary>🔑 Solution</summary>

```bash
# Set file permissions
chmod 664 specs.txt

# For true collaboration (if you had groups):
# chmod 664 specs.txt
# chgrp project-alpha specs.txt

# Create shared workspace
mkdir shared-workspace
chmod 775 shared-workspace
# This allows group members to create files
```

</details>

### Scenario 2.3: The Executable Script

```bash
cd ~/permissions-lab/shared/tools

# Make the backup script executable by owner and group only
ls -l backup.sh

# Test before:
./backup.sh  # Should fail

# Fix permissions:
# Your solution here...

# Test after:
./backup.sh  # Should work
```

<details>
<summary>🔑 Solution</summary>

```bash
chmod 750 backup.sh
# OR
chmod u=rwx,g=rx,o= backup.sh

# Verify it works:
./backup.sh
```

</details>

---

## 🎮 Part 3: Interactive Challenges (30 min)

### Challenge 3.1: Permission Puzzle

```bash
# Run this setup:
mkdir -p puzzle/{box1,box2,box3}
echo "Treasure!" > puzzle/box2/gold.txt
chmod 711 puzzle
chmod 700 puzzle/box1
chmod 711 puzzle/box2  
chmod 755 puzzle/box3
chmod 644 puzzle/box2/gold.txt

# Challenge: Without being root or using sudo:
# 1. Can you list contents of puzzle/?
# 2. Can you read gold.txt?
# 3. Can you ls inside box2?
# 4. Why do these permissions create this behavior?
```

<details>
<summary>🧩 Solution & Explanation</summary>

```bash
# 1. List puzzle/
ls puzzle/  # Works! Directory has execute (1) = can traverse

# 2. Read gold.txt
cat puzzle/box2/gold.txt  # Works! You can traverse through

# 3. List box2
ls puzzle/box2/  # Fails! No read permission on directory

# Explanation:
# - Execute on directory = can pass through
# - Read on directory = can list contents
# - Directory 711 = can access if you know filename!
```

</details>

### Challenge 3.2: The Restricted Report

```bash
# Setup
echo "Confidential Report v2" > shared/reports/confidential.txt
chmod 640 shared/reports/confidential.txt

# Challenge: Set permissions so that:
# 1. You can read/write
# 2. Your group can read only  
# 3. Others cannot access at all
# 4. But create a "public summary" that everyone can read
```

<details>
<summary>🔐 Solution</summary>

```bash
# Already correct for confidential.txt (640)

# Create public summary
echo "Report Summary: All Good" > shared/reports/summary.txt
chmod 644 shared/reports/summary.txt

# Verify
ls -la shared/reports/
```

</details>

### Challenge 3.3: The Execute Mystery

```bash
# Create this test scenario:
cd ~/permissions-lab
cat > test-exec.sh << 'EOF'
#!/bin/bash
echo "Script executed by: $(whoami)"
echo "Current permissions: $(ls -l $0)"
EOF

# Set unusual permissions:
chmod 111 test-exec.sh

# Questions:
# 1. Can you read the script?
# 2. Can you execute it?
# 3. Can you edit it?
```

<details>
<summary>🎭 Answer</summary>

```bash
# 1. Read it?
cat test-exec.sh  # NO! No read permission

# 2. Execute it?
./test-exec.sh  # YES! Execute permission exists

# 3. Edit it?
echo "new line" >> test-exec.sh  # NO! No write permission

# This shows execute permission works independently!
```

</details>

---

## 🏆 Part 4: Advanced Interactive Lab (30 min)

### Lab 4.1: Build a Secure Directory Structure

```bash
# Your mission: Create a mini company directory system
# Requirements:
# - Public folder: Everyone can read, only you can write
# - Private folder: Only you can access
# - Team folder: You and group can read/write, others nothing
# - Archive folder: Read-only for everyone

# Start building:
mkdir -p mycompany/{public,private,team,archive}
```

<details>
<summary>📋 Complete Solution</summary>

```bash
# Public folder
chmod 755 mycompany/public

# Private folder  
chmod 700 mycompany/private

# Team folder
chmod 770 mycompany/team

# Archive folder
chmod 755 mycompany/archive
# Make files inside read-only:
touch mycompany/archive/old-data.txt
chmod 444 mycompany/archive/old-data.txt

# Verify all:
ls -la mycompany/
```

</details>

### Lab 4.2: The Permission Simulator

```bash
# This exercise simulates multi-user permissions
# Since we can't create actual users, we'll role-play

# Setup simulation:
mkdir -p simulation/{alice,bob,shared}
echo "Alice's diary" > simulation/alice/diary.txt
echo "Bob's code" > simulation/bob/code.py
echo "Shared notes" > simulation/shared/notes.txt

# Set permissions as if:
# - alice/ is private to Alice
# - bob/ is private to Bob  
# - shared/ is collaborative

chmod 700 simulation/alice
chmod 700 simulation/bob
chmod 775 simulation/shared
chmod 664 simulation/shared/notes.txt

# Test scenarios:
# 1. If you were Bob, could you read Alice's diary?
# 2. If you were Alice, could you edit shared notes?
# 3. What permissions would let Bob share his code with Alice?
```

### Lab 4.3: Real-World Script Permissions

```bash
# Create a production-like script setup
mkdir -p scripts/{development,production,archive}

# Development script (developers can modify)
cat > scripts/development/deploy-test.sh << 'EOF'
#!/bin/bash
echo "Deploying to TEST environment..."
echo "Version: Development"
EOF

# Production script (read/execute only)
cat > scripts/production/deploy-prod.sh << 'EOF'
#!/bin/bash
echo "Deploying to PRODUCTION environment..."
echo "Version: Stable"
echo "⚠️  CAUTION: Production deployment!"
EOF

# Set appropriate permissions:
# Development: rwxrwx---
# Production: r-xr-x---
# Your commands here...
```

<details>
<summary>🚀 Solution</summary>

```bash
# Development scripts
chmod 770 scripts/development/deploy-test.sh

# Production scripts (no write to prevent accidents)
chmod 550 scripts/production/deploy-prod.sh

# Test them
./scripts/development/deploy-test.sh
./scripts/production/deploy-prod.sh

# Try to modify production (should fail for group)
echo "bad change" >> scripts/production/deploy-prod.sh
```

</details>

---

## 🎯 Final Challenge: The Permission Escape Room

```bash
# Setup the escape room
mkdir -p escape-room/{door1,door2,door3,exit}
echo "🔑 Key to door2" > escape-room/door1/key1.txt
echo "🔑 Key to door3" > escape-room/door2/key2.txt
echo "🔑 Key to exit" > escape-room/door3/key3.txt
echo "🎉 Congratulations! You escaped!" > escape-room/exit/freedom.txt

# Set the puzzle permissions
chmod 111 escape-room
chmod 755 escape-room/door1
chmod 600 escape-room/door1/key1.txt
chmod 111 escape-room/door2
chmod 644 escape-room/door2/key2.txt
chmod 100 escape-room/door3
chmod 444 escape-room/door3/key3.txt
chmod 500 escape-room/exit
chmod 400 escape-room/exit/freedom.txt

# Your mission:
# Navigate through all doors and read the freedom.txt file
# Document which commands work and why!
```

<details>
<summary>🏃 Escape Route</summary>

```bash
# Can't ls escape-room/ (no read), but can cd (execute)
cd escape-room

# Door 1: Can ls and enter
ls door1/  # Works (755)
cat door1/key1.txt  # Fails (600 - owner only)

# Door 2: Can enter but not ls
cd door2  # Works (execute)
ls  # Fails (no read)
cat key2.txt  # Works if you know filename! (644)

# Door 3: Can only enter
cd ../door3  # Works (execute only)
cat key3.txt  # Works (444 - everyone can read)

# Exit: 
cd ../exit  # Works (execute)
cat freedom.txt  # Works (400 - owner read)

# The lesson: Execute permission lets you traverse!
```

</details>

---

## 📝 Lab Summary & Best Practices

### Key Takeaways:
1. **Read** = see contents (files) or list (directories)
2. **Write** = modify contents or add/remove files
3. **Execute** = run (files) or traverse (directories)

### Permission Quick Guide:
```bash
# Common permission patterns:
644 - Standard file (rw-r--r--)
755 - Executable/Directory (rwxr-xr-x)
600 - Private file (rw-------)
700 - Private directory (rwx------)
666 - Warning! Too open (rw-rw-rw-)
777 - Danger! Never use (rwxrwxrwx)
```

### Real-World Tips:
1. **Default umask**: Check with `umask` command
2. **Special bits**: Learn about setuid, setgid, sticky bit
3. **ACLs**: For complex permissions use `getfacl`/`setfacl`
4. **Security**: Principle of least privilege always!

---

## 🏁 Completion Checklist

Track your progress:
- [ ] Completed Part 1: Understanding Permissions
- [ ] Completed Part 2: Practical Scenarios  
- [ ] Completed Part 3: Interactive Challenges
- [ ] Completed Part 4: Advanced Lab
- [ ] Escaped the Permission Escape Room
- [ ] Can explain rwx for files vs directories
- [ ] Comfortable with both numeric and symbolic notation

**Congratulations! You've mastered Linux permissions! 🎉**