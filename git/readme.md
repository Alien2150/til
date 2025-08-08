# Fix history (squash all commits to one commit rather than multiple)
```
git reset --soft $(git merge-base main HEAD)  # or whatever your base is
git commit -am "Your single clean commit message"
git push --force
```
