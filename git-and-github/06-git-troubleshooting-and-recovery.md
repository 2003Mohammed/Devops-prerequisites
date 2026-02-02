1. Undo Local Changes (Not Committed)
git restore file.txt


Reset everything:

git restore .

2. Undo Last Commit (Keep Changes)
git reset --soft HEAD~1


Used when:

Commit message is wrong

Files are correct

3. Fix “Diverged Branch” Issue
git pull --rebase


Preferred in teams to avoid noisy merge commits.

4. Recover Lost Commits
git reflog


Restore:

git reset --hard <commit-hash>

5. Abort a Bad Merge
git merge --abort


Used when conflicts go wrong.

DevOps Insight

git reflog is the emergency exit — almost nothing is truly lost in Git.

✅ Commit commands (exact)
git add networking/02-linux-networking-core-troubleshooting.md
git add git/02-git-troubleshooting-and-recovery.md
git commit -m "Add concise networking and git troubleshooting prerequisites"
git push
