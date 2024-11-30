When working on an isolated/local git repo,  
`git remote show` to see whether it has any remote origin. If the output is empty, that means there are no such thing as 'origin'.  

To add a remote repo(eg. from Github): `git remote add "origin" https://github.com/username/repo-clone-url.git`

now the previous command will output 'origin'. To see the url the local repo links to(syncs to): `git remote get-url origin`

`git push --force` wont work if the local branch name and remote branch names are different.

To push to specific remote branch:  
`git push -u origin master:edge-function`

Alternate:   
Use`git branch --set-upstream-to=origin/edge-fun` to set the upstream-branch explicitly so that in future we can just use `git push` instead of `git push -u origin master:edge-function`

