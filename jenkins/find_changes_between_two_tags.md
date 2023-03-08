# Issue

GIT_PREVIOUS_COMMIT is not set correctly when tag checkout is being used. This makes it harder to get the proper changelog

# Fix
Get previous tag:

```
sh(script: "git describe --tags --abbrev=0 ${env.TAG_NAME}^1", returnStdout: true) 
```

Get changes between current tag and previous tag:

```
sh(script: "git log --name-only --oneline ${env.PREVIOUS_TAG_NAME}..${env.TAG_NAME}", returnStdout: true).trim()
```
