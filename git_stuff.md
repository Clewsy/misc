# Add ssh key to github account
Copy key with:
```shell
$ cat ~/.ssh/id_rsa.pub
```
In gitlab/github account settings, add ssh key.
Test with:
```shell
$ ssh -T git@gitlab.com
$ ssh -T git@github.com
```

# Set some global settings
```shell
$ git config --global user.name "clewsy"
$ git config --global user.email "jadon@clews.pro"
$ git config --global color.ui true
$ git config --global core.editor vim
```

# Clone an existing repo to the local machine
```shell
$ git clone git@gitlab.com:clewsy/scripts
```

# Initialise a new repo in the current directory
```shell
$ git init
$ git branch -m main # This will rename the initial branch from "master" to "main".
```

# Add all files in directory to repo
```shell
$ git add .
```
Or
```shell
$ git add -A
```

# Commit files to repo
```shell
$ git commit -m "message to attach to the commit"
```

# Ignore files from repo
Create ```.gitgnore``` file in repo root and add to it a list of files to be ignored
```shell
$ vim .gitignore
```
Add file list.
```shell
$ git add .gitignore
$ git commit -m "Added .gitignore file list."
```

# Connect local repo to gitlab and push local to gitlab
```shell
$ git remote add origin git@gitlab.com:clewsy/scripts
$ git push origin master # Change "master" to "main" if needed.
```

# Rename a file in the repository
```shell
$ git mv old_filename new_filename
$ git status
$ git commit -m "Renamed file"
$ git push origin master # Change "master" to "main" if needed.
```

# Completeley remove a file from repo - including past commits
Follow this guide:
https://blog.tinned-software.net/remove-files-from-git-history/
```shell
$ git filter-branch --force --index-filter 'git rm -rf --cached --ignore-unmatch directory/and/filename.extension' --prune-empty --tag-name-filter cat -- --all
$ git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin
$ git reflog expire --expire=now --all
$ git gc --prune=now
```
Repo has to be unprotected
```shell
$ git push origin --force --all
$ git push origin --force --tags
```

# Clone a repo - push from gitlab to github
## In github:
1. Create the repo - same name as that to be mirrored from gitlab
2. Generate a token: In UI: *Settings* -> *Developer Settings* -> *Personal access tokens* -> *Generate new token* -> <enter a "Note" e.g. "gitlab_push_docs"> -> Check *write:packages* -> *Generate Token*
3. Copy token -> e.g. **GENERATEDTOKEN**

## In gitlab:
1. Open repo to be pushed
2. *Settings* -> *Repository* -> *Mirroring Repositories "Expand"*
3. *Git Repository URL* e.g.: **https://clewsy@github.com/clewsy/docs.git**
4. *Mirror direction*: **Push**
5. *Authentication method*: **Password**
6. *Password*: **GENERATEDTOKEN** (make sure spaces weren't copied).
7. *Mirror Repository*
8. Test by pressing the *Update now* button.

