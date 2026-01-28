# Git Troubleshooting

## Undo Changes
- git checkout -- file
- git reset HEAD file

## Undo Commit (Keep Changes)
- git reset --soft HEAD~1

## Undo Commit (Discard Changes)
- git reset --hard HEAD~1

## Fix Merge Conflicts
- git status
- edit conflict files
- git add .
- git commit

## DevOps Use Case
Critical when pipelines fail due to bad commits or conflicts.
