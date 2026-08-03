# Git commands cheatsheet

## Stop tracking a file already commited/tracked
1. Add the file to `.gitignore` file
```gitignore
<file_name>
```

2. Remove it from Git's index but keep the file
```bash
git rm --cached <file_path/name>
```
