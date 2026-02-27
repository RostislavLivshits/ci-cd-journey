# CLI Cheatsheet (Git + Basics)

## 1) Daily Git workflow (commit + push)
### Check status
git status

### (Optional) See what changed
git diff

### Stage changes
git add .                       # stage all changes
git add path/to/file            # stage one file

### Commit
git commit -m "short clear message"

### Push
git push


## 2) View history and state
git log --oneline               # short commit history
git branch                      # list local branches
git remote -v                   # show remote URLs


## 3) Fix: GitHub HTTPS push fails (password not supported)
### Symptom
"Password authentication is not supported for Git operations"

### Cause
Remote uses HTTPS, GitHub требует SSH или Personal Access Token.

### Solution (recommended): switch remote to SSH
# Check current remote
git remote -v

# Switch to SSH remote
git remote set-url origin git@github.com:USERNAME/REPO.git

# Test SSH auth
ssh -T git@github.com

# Push again
git push


## 4) SSH keys (Mac)
ls -al ~/.ssh                   # list keys

# Copy public key to clipboard (paste into GitHub -> Settings -> SSH keys)
pbcopy < ~/.ssh/id_rsa.pub

# (If needed) Add key to ssh-agent (optional, when permission denied)
eval "$(ssh-agent -s)"
ssh-add --apple-use-keychain ~/.ssh/id_rsa
ssh-add -l


## 5) Terminal pager (less) shortcuts
q       # quit
space   # page down
b       # page up
/word   # search