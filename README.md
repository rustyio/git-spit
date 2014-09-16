# git-spit

### Overview

`git-spit` is a developer utility for people who want to write code
locally, but offload the CPU-heavy work (ie: unit tests, running the
website) to the cloud. It works by mirroring file changes in a local
git repo to a remote git repo in real time, via SSH.

### Usage

Here's how it works:

1. Download `git-spit` and put it somewhere in your `$PATH`.
2. Add a git remote to the repo you want to mirror, ie: `git remote
   add foo ssh://your.server/~/path`
3. Run **git-spit** followed by the name of your remote repo, ie:
   `git-spit foo`

The `git-spit` utility will make sure the two git repos are
synchronized, and then monitor the local repo for file changes. When
it detects a change, it will send the updated file to the remote repo
via SSH. `git-spit` will even handle branch changes.

### FAQ

*Couldn't you just commit the code and push it to the remote server?*

Well, yes, but it would take a lot of extra steps *and* dirty up your
commit history.
