# Contributing to Clamshell

This guide will walk you through contributing to Clamshell, and assumes you
have some experience with the game go, but might be relatively new to
programming or to the tools/technologies.

## Bugs, Features, Questions, Comments

If you have any bugs, feature requests, questions, or comments, please file
them on our Issue on our [github tracker](https://github.com/otrego/clamshell/issues)

## Getting Started on Go

First, if you're new to Go, the language, check out:

1.  [Installing Go](https://golang.org/doc/install)
2.  [The Go Tour](https://tour.golang.org/welcome/1)
3.  [How to Write Go Code](https://golang.org/doc/code.html)

If you're very new to Go, you might want to check out the
[otrego/experimental](https://github.com/otrego/experimental)
repository.

## Getting Started with Git

If you're new to Git / Github, check out:

1.  [The Git Book](https://git-scm.com/book/en/v2). In particular, I find these
    sections very helpful:
    1.  [Basic Branching & Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
    2.  [Distributed Workflows](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows#ch05-distributed-git).
        Specifically, we use an [Integration-Manager workflow (Github)](https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows#wfdiag_b).
2.  [Getting Started with Github](https://help.github.com/en/github/getting-started-with-github)

## Editors

You are, of course, free to use whichever text editor you feel most comfortable
with. Many people working on Clamshell use Vim or IntelliJ, so we can help you
get started with these editors.

**Vim**
*   [`vimtutor`](https://superuser.com/questions/246487/how-to-use-vimtutor) run
    from the Bash command-line is the easiest way to get started with Vim.
*   If you want to delve deep into learning about Vim, check out
    [Vim the Hard Way](https://learnvimscriptthehardway.stevelosh.com/)
*   Install a plugin manager: [Vim-Plug](https://github.com/junegunn/vim-plug) or
    [Vundle](https://github.com/VundleVim/Vundle.vim) are good choices.
*   Install the go-plugin for Vim: [vim-go](https://github.com/fatih/vim-go)

**IntelliJ**

TODO: Add some details about IntelliJ. Pull requests welcome!

**Sublime Text**
*   This [workflow tutorial](https://www.alexedwards.net/blog/streamline-your-sublime-text-and-go-workflow) is a great guide towards setting up features such as auto-formatting, auto-linting, and auto-completion

## Setting Up Your Dev Environment

First, make sure you have
[two-factor auth](https://help.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa)
setup in Github. This is a requirement for working with Otrego.

We expect all developers, both external contributors and maintainers to
interact with Clamshell via a
[fork-and-pull-request model](https://help.github.com/en/github/getting-started-with-github/fork-a-repo).
So generally, developers will fork the Clamshell repository and then submit
pull requests to the primary `otrego/clamshell` repository.

You will want to set up your `GOPATH` and `GOBIN` environment variables:

- `GOPATH` controls where dependencies are downloaded via `go get`
- `GOBIN` controls where go binaries are installed.

On OSX or Linux using bash, you can set these by adding the following to your
`$HOME/.bash_profile` or `$HOME/.bashrc`:

```shell
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export PATH=$GOBIN:$PATH
``` 

Assuming you have created a
[fork](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) 
of Clamshell (see Development Model), then create the relevant directories &
clone the repo:

```shell
git clone github.com/<USERNAME>/clamshell
```

Set the upsteams appropriately:

```shell
cd clamshell
git remote add upstream git@github.com:otrego/clamshell.git

# Check everything's set up correctly:
git remote -v
```

Then, make sure it builds!

```shell
cd clamshell
go test ./...
```

Before you are ready to commit your changes, we recommend doing the following:
1. Install golint
```shell
go get -u golang.org/x/lint/golint
``` 
2. Enable the pre-commit hooks in this repository
```shell
git config core.hooksPath .githooks
```

3. Run the following to ensure go code quality

```shell
gofmt
golint
govet
```
## For Windows 10 Users:  Setting Up Your Dev Environment

This is a setup checklist for setting up a Windows 10 software development environment to program in GoLang language,
 and to collaborate with your software development team using GitHub.

This assumes your computer operating system is Microsoft Windows 10.

1. Install Visual Studio Code.  <https://code.visualstudio.com/Download>

  - Check to ensure that the "Terminal" command line feature is installed with VS Code.  (See "Terminal" menu on topline header)
  - If not installed, install the Terminal feature from the Visual Studio catalog of VS Code extensions.

2. Install the GoLang language extension for VS Code, <https://marketplace.visualstudio.com/vscode> ... search for "GO". 

3. We use GitHub collaboration tools.  GitHub is a website and cloud-based service that helps developers, and their collaborators, 
   store and manage their code, as well as track and control changes to their code.
   Learn about GitHub from <https://kinsta.com/knowledgebase/what-is-github/> 
  - For using GitHub we recommend using Git commands from the Terminal.  
  - We don't recommend installing the GitHub extension for VS Code.

## Change Workflow

Now that you've set up your dev environment, let's talk about git development
workflow. The general flow should be:

1.  Do development on branches in your fork.
2.  Make pull requests to the main repo `otrego/clamshell`
3.  Get your code reviewed by a team member.
4.  Once approved, submit the changes.

First, here's what my workflow looks like (which is quite similar to this
[Atlassian guide](https://www.atlassian.com/git/tutorials/git-forks-and-upstreams).

### Example Workflow (kashomon)

1.  Rebase on any upstream changes into master via merge.

    ```shell
    git checkout master
    git fetch upstream
    git merge upstream/master

    # update my fork's master branch.
    git push
    ```

2.  Do feature development on a branch

    ```shell
    git checkout -b somefeature
    # ... do some work
    git add -A .
    git commit -a
    git push origin somefeature
    ```

3.  (Optional) If much time has passed, make sure your local master & feature
    branches are updated, running through 1. and then rebasing on top of that.

    ```shell
    git checkout master
    git fetch upstream
    git merge upstream/master
    git push

    # Update feature branch
    git checkout somefeature
    git merge master

    git push
    ```

4.  When your change is ready, use the Github UI to get code reviewed & merge
    the changes into the repository:

    1.  Perform pull request via Github UI from your repsitory + feature branch
        to Github.

    2.  Get code reviewed by team member in Github UI. If you are reviewing
        code, make sure to 'Approve' the change.

    3.  Sqaush into single commit via Github UI and merge into the repository
        (this should happen by default.).
