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
