Git Rails
=========

Manage bundle and migrations automatically while you use git!

For example:

- If you pull down code from your remote and there are new or updated gems
  * it will run `bundle` for you
- If you checkout a branch that uses a different set of migrations
  * it will roll back the old set and apply the new ones
- If you rebase and there are new gems and migrations
  * it will run `bundle` and `rake db:migrate test:prepare`
- If you don't like automagical git hooks
  * run `git_rails` and it will try and find out where you came from and run the same check

### Install

Copy or symlink:

1. `bin/git_rails` into your executable `$PATH`
2. `hooks/*` into your `.git/hooks/`

### Usage

#### Command

After you checkout a branch, if you realize your migrations or gems are messed up from the switch, just run:

`git_rails`

This is the same as running:

`git_rails ORIG_HEAD HEAD`

If you know what ref you are coming from and it isn't `ORIG_HEAD` use:

`git_rails [REF_YOU_JUST_CAME_FROM]`

Or if you really know what you are doing and you want to pretend like you are on a different branch you can do:

`git_rails [REF_YOU_CAME_FROM] [REF_YOU_ARE_GOING_TO]`

Migrations that were added between `REF_YOU_CAME_FROM` and `REF_YOU_ARE_GOING_TO` that do not exist on your current `HEAD` will not be applied because they don't exist!!

#### Options

The following command line options are supported:

* -v, --verbose
  * Display pending changes, prompt to continue, display command output
* -y, --auto_confirm
  * Use in conjunction with verbose mode to apply pending changes without prompting
* -d, --dry_run
  * Display pending changes and exit
* -h, --help
  * Display usage and exit

#### Hooks

You shouldn't have to think about the hooks once they are installed. Just pull, checkout, and rebase as normal and they should work fine. If you find that `git_rails` hasn't fired when it should follow the command instructions to run it manually.

Also, the hooks are optional, you can use `git_rails` without them!

#### Monorepo usage

If the Rails project is not in the root of the Git repository, execute `git_rails` and hooks in the Rails directory.

For example, to make the post-checkout hook run in a particular subdirectory, create the following `.git/hooks/post-checkout` file:

```sh
#!/bin/sh
cd path/to/rails/project
exec /path/to/git_rails/hooks/post-checkout "$@"
```
