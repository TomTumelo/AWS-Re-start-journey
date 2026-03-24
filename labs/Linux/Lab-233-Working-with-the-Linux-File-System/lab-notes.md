# Lab 233 – Personal Notes

## Key Commands Learned

| Command | What it does |
|--------|--------------|
| `mkdir folder` | Creates a new directory |
| `touch file.csv` | Creates an empty file |
| `cp -r source dest` | Copies a folder and all its contents |
| `mv source dest` | Moves a file or folder |
| `rm filename` | Deletes a file |
| `rmdir folder` | Deletes an EMPTY folder only |
| `rm -r folder` | Deletes a folder and everything inside |
| `ls -laR` | Lists all files recursively with details |
| `pwd` | Shows your current directory path |
| `cd ..` | Goes up one folder level |

## Important Notes
- `rmdir` only works on **empty** directories — use `rm -r` for non-empty ones
- `cp -r` is needed for folders (the `-r` means recursive)
- You can use relative paths: `touch Management/file.csv` works from the parent folder
- Always use `pwd` and `ls` to verify you are in the right place before running commands

## Gotchas / Mistakes to Avoid
- Forgetting `-r` when copying or deleting folders
- Running `rmdir` on a non-empty folder (it will fail)
- Not verifying your current directory with `pwd` before running commands
