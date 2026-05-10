# Informative git prompt for zsh

> **Fork of [olivierverdier/zsh-git-prompt](https://github.com/olivierverdier/zsh-git-prompt)** with macOS compatibility fixes: defaults to `python3` and accepts both `python` and `python3` as `GIT_PROMPT_EXECUTABLE`.

[![Build Status](https://travis-ci.org/olivierverdier/zsh-git-prompt.svg)](https://travis-ci.org/olivierverdier/zsh-git-prompt)

A `zsh` prompt that displays information about the current git repository. In particular the branch name, difference with remote branch, number of files staged, changed, etc.

(an original idea from this [blog post][]).

## Examples

The prompt may look like the following:

-   `(master↑3|✚1)`: on branch `master`, ahead of remote by 3 commits, 1 file changed but not staged
-   `(status|●2)`: on branch `status`, 2 files staged
-   `(master|✚7…)`: on branch `master`, 7 files changed, some files untracked
-   `(master|✖2✚3)`: on branch `master`, 2 conflicts, 3 files changed
-   `(experimental↓2↑3|✔)`: on branch `experimental`; your branch has diverged by 3 commits, remote by 2 commits; the repository is otherwise clean
-   `(:70c2952|✔)`: not on any branch; parent commit has hash `70c2952`;
    the repository is otherwise clean

Here is how it could look like when you are ahead by 4 commits, behind by 5 commits, and have 1 staged files, 1 changed but unstaged file, and some untracked files, on branch `dev`:


<img src="https://github.com/olivierverdier/zsh-git-prompt/raw/master/screenshot.png" width=300/>


## Prompt Structure

By default, the general appearance of the prompt is:

```
(<branch><branch tracking>|<local status>)
```

The symbols are as follows:

### Local Status Symbols

|Symbol|Meaning
|------|------|
|✔ |   repository clean
|●n |   there are `n` staged files
|✖n |   there are `n` unmerged files
|✚n |   there are `n` changed but *unstaged* files
|… |   there are some untracked files


### Branch Tracking Symbols

Symbol | Meaning
-------|-------
↑n |   ahead of remote by `n` commits
↓n |   behind remote by `n` commits
↓m↑n |   branches diverged, other by `m` commits, yours by `n` commits

### Branch Symbol

When the branch name starts with a colon `:`, it means it’s actually a hash, not a branch (although it should be pretty clear, unless you name your branches like hashes :-)

## Install

1.  Clone this repository somewhere on your hard drive.
2.  Source the file `zshrc.sh` from your `~/.zshrc` config file, and
    configure your prompt. So, somewhere in `~/.zshrc`, you should have:

    ```sh
    source path/to/zshrc.sh
    # an example prompt
    PROMPT='%B%m%~%b$(git_super_status) %# '
    ```
3.  Go in a git repository and test it!

### Python version

By default, `python3` is used. To use a different executable, set `GIT_PROMPT_EXECUTABLE` before sourcing:

```sh
export GIT_PROMPT_EXECUTABLE="python"  # use python instead of python3
source path/to/zshrc.sh
```

### Haskell (optional)

There is now a Haskell implementation as well, which can be four to six times faster than the Python one. The reason is not that Haskell is faster in itself (although it is), but that this implementation calls `git` only once. To install, do the following:

1.  Make sure [Haskell's stack](http://docs.haskellstack.org/en/stable/README.html#how-to-install) is installed on your system
2.  `cd` to this folder
2.  Run `stack setup` to install the Haskell compiler, if it is not already there
3.  Run `stack build && stack install` (don't worry, the executable is only “installed” in this folder, not on your system)
4.  Define the variable `GIT_PROMPT_EXECUTABLE="haskell"` somewhere in
    your `.zshrc`

## Customisation

- You may redefine the function `git_super_status` (after the `source` statement) to adapt it to your needs (to change the order in which the information is displayed).
- Define the variable `ZSH_THEME_GIT_PROMPT_CACHE` in order to enable caching.
- You may also change a number of variables (which name start with `ZSH_THEME_GIT_PROMPT_`) to change the appearance of the prompt.  Take a look in the file `zshrc.sh` to see how the function `git_super_status` is defined, and what variables are available.

**Enjoy!**

  [blog post]: http://sebastiancelis.com/2009/nov/16/zsh-prompt-git-users/
  
