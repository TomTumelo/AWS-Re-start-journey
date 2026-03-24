# Lab 234 – Instructions

## Task 1: Connect to EC2 via SSH

### Windows (PuTTY)
1. Click **Details > Show** and download the `labsuser.ppk` file
2. Note the **PublicIP** address
3. Open PuTTY and connect using the PPK file

### Mac/Linux
```bash
cd ~/Downloads
chmod 400 labsuser.pem
ssh -i labsuser.pem ec2-user@<public-ip>
```

---

## Task 2: Write the Backup Shell Script
```bash
# Confirm you are in the home folder
pwd

# Create the backup.sh file
touch backup.sh

# Make it executable
sudo chmod 755 backup.sh

# Open it in the vi editor
vi backup.sh
```

### Inside vi:
1. Press `i` to enter insert mode
2. Type the script below
3. Press `Esc` then type `:wq` and press Enter to save and exit

### backup.sh contents:
```bash
#!/bin/bash
DAY="$(date +%Y_%m_%d)"
BACKUP="/home/$USER/backups/$DAY-backup-CompanyA.tar.gz"
tar -csvpzf $BACKUP /home/$USER/CompanyA
```

---

## Run the Script
```bash
# Run the script
./backup.sh

# Verify the backup was created
ls backups/
```

### Expected output:
```
2022_05_18-backup-CompanyA.tar.gz
```
