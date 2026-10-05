Git & GitHub Setup Notes (Windows)
Terminals
Git Bash — installed with Git for Windows. Uses Linux-style commands (ls, pwd, ~). Recommended for learning since it matches most tutorials/docs.
CMD — built into Windows. Uses Windows-style commands (dir, cd).
Git commands themselves (git add, git commit, etc.) are identical in both — only the surrounding shell commands differ.
Git Bash is not real Linux — it's a Windows compatibility layer (MSYS2/MinGW) that lets you type Linux-style commands.
Check Git identity (already set up)
git config --global user.name
git config --global user.email
These identify who made each commit.
⚠️ Flags are case-sensitive: use --global user.email, not user,email (comma) — small typo breaks the command.
Two ways to authenticate with GitHub
Method	How it works	Typing needed after setup
SSH keys	Key pair (private stays on your PC, public goes on GitHub)	None
HTTPS + Personal Access Token (PAT)	Token used like a password	Sometimes, unless cached

GitHub stopped accepting real account passwords for Git operations since Aug 2021 — HTTPS now requires a PAT instead.

SSH Setup (done ✅)

1. Check for existing keys

ls -al ~/.ssh
ls = list files, -a = show hidden files, -l = long/detailed format, ~ = home folder.

2. Generate a new key pair

ssh-keygen -t ed25519 -C "your_email@example.com"
-t ed25519 = modern, secure key type
-C = comment/label (your email) — must be capital C
Press Enter through the prompts (default location, no passphrase for simplicity)
Creates two files:
id_ed25519 → private key — never share
id_ed25519.pub → public key — safe to share, goes on GitHub

3. Display the public key

cat ~/.ssh/id_ed25519.pub
Copy the full output.

4. Add it to GitHub

GitHub → profile picture → Settings → SSH and GPG keys → New SSH key
Paste the public key → Add SSH key

5. Test the connection

ssh -T git@github.com
First time: you'll be asked to trust GitHub's host key (Trust On First Use) → type yes
Success message: Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.
("No shell access" is expected — normal and fine.)
HTTPS + Personal Access Token (PAT) — alternative method
GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
Generate new token (classic)
Give it a name, set an expiration, check the repo scope
Generate token → copy it immediately (shown only once)
Use this token as the "password" when Git prompts for credentials over HTTPS
Push / Pull Practice Workflow (next steps)

1. Create a repo on GitHub

+ → New repository → name it (e.g. git-practice) → check Add a README → Create repository

2. Copy the SSH URL

Green Code button → SSH tab → copy URL (looks like git@github.com:username/repo.git)

3. Clone it to your machine

git clone git@github.com:username/repo.git
cd repo

4. Make a change, then push

echo "hello" >> notes.txt
git add notes.txt
git commit -m "add notes file"
git push

5. Practice pull (simulate a remote change)

Edit a file directly on GitHub's website (or from another folder/clone), commit it there
Then on your machine:
git pull
This fetches and merges the remote changes into your local copy.