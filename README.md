# git_hook_stack:

This script provides a way to stack multiple git hooks and to
install global hooks that will run before any local repository hooks.

## Installation:

NOTE: you can replace --global with --system in the below instructions
if you want to install git_hook_stack for all users on your system.

NOTE: these instructions assume you are in the directory containing the 
git_hook_stack script.

1. HOOKS_PATH="<path-to-global-hooks>" && \
   git config --global gitHookStack.hooksPath "${HOOKS_PATH}" && \
   git config --global core.hooksPath "${HOOKS_PATH}"

     This will tell git_hook_stack where your global hooks are stored and 
     make the hooks global to the current user.

2. ./git_hooks_stack --init

     This will create the required symlinks for each of the standard
     git hooks in the <path-to-global-hooks> directory.


## Add global hooks:

Put a script in <hook_name>.d in the <path-to-hook_stack-directory>
and make it executable.

## Add local hooks:

Create a hook in .git/hooks as normal.

or

Put a script in a directory called <hook_name>.d in the .git/hooks directory
and make it executable.

## Order of execution:

1. global hooks in <path-to-hook_stack-directory>/<hook_name>.d

1. local hook in .git/hooks/<hook_name>

1. local hook in .git/hooks/<hook_name>.d/

If a hook returns a non-zero return code no futher hooks will be run.

## Debugging

To enable debug output:

```bash
export GIT_HOOKS_STACK_DEBUG=1
```
