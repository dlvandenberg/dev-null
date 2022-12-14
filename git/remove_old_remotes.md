# Remove old git remotes
When working with _feature branches_ a lot, after a while you end up with loads of local branches where the _remote_ has been deleted (if the _source_ branch has been deleted after merging the _Pull Request_). To clean up these local branches, you can do the following:

## Fetch all changes from remote
Run the command:
```bash
$ git fetch --prune
```

This will fetch all changes from the remotes and remove tracking branches

## Show a list of branches
Run:
```bash
$ git branch -vv
```

It will output the list of branches locally, with information about the remote. It will indicate `[origin/<remote-branch>: gone]` if the remote branch has been deleted. You can use that information to chain the output:

## Delete merged branches
In combination with the previous command, run:
```bash
$ git branch -vv | awk '/: gone]/{ print $1 }' | xargs git branch -d
```
Which will do the following:
1. `git branch -vv` : show all branches with their remote branch information
2. `awk '/: gone]/{ print $1 }'`: find all branches with the text `: gone]` and print the first word (which is the branch name)
3. `xargs git branch -d`: for every name, run the command `git branch -d`, which will delete the branch locally if it has been merged.

In case the branch has not been merged, but deleted on the remote, the last command will show a warning. You can still delete the branch locally by changing the flag to `-D` (uppercase).