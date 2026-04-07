# 🐧 Lab 06 — Bash Shell Scripts (Lab 234)

> **Domain:** Linux | **Status:** ✅ Complete

---

## 🎯 Lab Objective

Write and execute Bash shell scripts to automate tasks. Covers script creation, file management automation, permission handling, and working with company file structures.

---

## 📚 What I Did

### Tasks Completed

| Task | Description | Screenshot |
|---|---|---|
| Script creation | Wrote a functional Bash script | `script.png` |
| File management | Created and managed CompanyA file structure | `companyA files.png` |
| Listing & output | Used commands to list and display data | `list].png` |
| Permissions | Set correct permissions on scripts and files | `permissions.png` |

---

## 🧠 Key Concepts Covered

### Bash Script Structure
```bash
#!/bin/bash
# ^^^ Shebang line — tells the OS to use bash to run this script

# Variables
NAME="Tumelo"
DATE=$(date +%Y-%m-%d)

# Echo output
echo "Hello, $NAME! Today is $DATE"

# Conditional
if [ -f "file.txt" ]; then
    echo "File exists"
else
    echo "File not found"
fi

# Loop
for file in *.txt; do
    echo "Processing: $file"
done
```

### Making Scripts Executable
```bash
chmod +x script.sh      # Add execute permission
./script.sh             # Run the script
bash script.sh          # Alternative way to run
```

### Automating File & Directory Tasks
```bash
#!/bin/bash
# Create company folder structure
mkdir -p CompanyA/{HR,Finance,IT,Marketing}

# Create files in each department
for dept in HR Finance IT Marketing; do
    touch "CompanyA/$dept/README.txt"
    echo "Department: $dept" > "CompanyA/$dept/README.txt"
done

echo "CompanyA structure created!"
ls -R CompanyA/
```

### Variables & User Input
```bash
# Read user input
read -p "Enter your name: " USERNAME
echo "Welcome, $USERNAME!"

# Command substitution
CURRENT_DIR=$(pwd)
FILE_COUNT=$(ls | wc -l)
echo "You are in: $CURRENT_DIR with $FILE_COUNT files"
```

### Exit Codes
```bash
command_that_might_fail
if [ $? -eq 0 ]; then
    echo "Success"
else
    echo "Command failed with exit code $?"
fi
```

---

## 💡 Key Takeaways

1. **Always start with `#!/bin/bash`** — without the shebang, the OS doesn't know how to interpret the script.
2. **`chmod +x` before running** — scripts need execute permission or they won't run with `./`.
3. **Quote your variables** — `"$VAR"` prevents word splitting when variables contain spaces.
4. **Test with `bash -x script.sh`** — debug mode prints each line as it executes.
5. **Scripts are reusable automation** — one script that creates a folder structure saves hours of manual work.

---

## 📸 Screenshots

> Screenshots available in [`./bash screenshots/`](./bash%20screenshots/)
