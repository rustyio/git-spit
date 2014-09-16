# git-spit - Code in the cloud.

### Overview

`git-spit` helps you move your development environment into the
cloud. Typically, the challenge of developing in the cloud is that it
requires your local code editor to be "cloud aware". `git-spit` fixes
this; it watches your local files and mirrors changes to a remote
server.

### Usage

To use `git-spit`:

1. Download the `git-spit` script and put it in your `$PATH`.
2. Add a git remote to the repo you want to mirror, ie: `git remote add foo ssh://your.server/~/path`
3. Run `git-spit REMOTE_NAME`, ie: `git-spit foo`

If you don't specify a remote repo, `git-spit` will assume you want
the "origin" remote repository.

You can also specify the remote hostname and path explicitly instead
of using a remote name. Run `git-spit REMOTE_HOST REMOTE_PATH`

`git-spit` has been tested on Mac and Ubuntu.

### Why code in the cloud?

+ Your app consumes more RAM than your laptop can offer.
+ Your app has unique hardware requirements; a GPU to run CUDA, for example.
+ Your app needs a specific flavor of OS.
+ Your data is too big to store on your laptop.
+ Your data is too sensitive to store on your laptop.
+ You want to preserve battery life by letting another machine run CPU-intensive code, data processing, unit tests.
+ You want to maintain separate environments for different clients.

### Under the Hood

To watch for file changes, `git-spit` piggybacks on top of
git. Basically, a loop runs `git status` to get a list of potentially
changed files, it then uses file modification times to determine which
files have actually changed since the last sync.

To synchronize file changes, `git-spit` piggybacks on top of ssh (more
specifically, scp). It copies any changed files to the remote host and
path.

`git-spit` has some special logic to handle commits, branch switches,
new directories, deletions, etc., but it can't handle everything. If
it encounters something unexpected, it will exit with an error
message.


### FAQ

*Couldn't I just commit the code and push it to the remote server?*

Yes, but it would take a lot of extra steps *and* dirty up your commit history.

*Why doesn't this use some kind of file watching gem like 'listen'?*

An early version did use 'listen', but it hammered the CPU. The
current approach is much more efficient.


### How do I contribute?

1. Fork the repo on Github.
2. Make a branch.
3. Write your changes.
4. Issue a Github pull request with a good description.
