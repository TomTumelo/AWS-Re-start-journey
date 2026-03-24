# Lab 234 - Personal Notes

## Key Commands Learned

| Command | What it does |
|--------|--------------|
| touch file.sh | Creates an empty shell script file |
| chmod 755 file.sh | Makes the script executable |
| ./script.sh | Runs the script |
| vi file.sh | Opens file in vi text editor |
| date +%Y_%m_%d | Returns current date formatted as YYYY_MM_DD |
| tar -csvpzf archive.tar.gz folder/ | Creates a compressed archive of a folder |
| ls backups/ | Verifies the backup was created |

## Script Breakdown

| Line | What it does |
|------|--------------|
| #!/bin/bash | Shebang - tells the system this is a Bash script |
| DAY=$(date +%Y_%m_%d) | Stores todays date in a variable |
| BACKUP=/home/$USER/backups/... | Builds the full backup file path |
| tar -csvpzf $BACKUP /home/$USER/CompanyA | Creates the compressed backup |

## Important Notes
- $USER automatically returns the current logged-in username
- chmod 755 gives the owner full rights and others read/execute
- tar warning Removing leading / is normal, not an error
- You could schedule this script with cron to run daily automatically

## Gotchas / Mistakes to Avoid
- Forgetting #!/bin/bash on line 1 - script will not run properly
- Forgetting chmod 755 - script will not be executable
- The backups/ folder must exist before running the script
