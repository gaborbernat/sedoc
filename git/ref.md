Git Refs
========

A "ref" is essentially a variable whose value eventually can be
resolved to the SHA1 of a git object (most often a commit). The name
is in Unix path format (`refs/a/b/c`); a name with subnames
(`refs/a/b`) cannot be a ref itself.

"Standard" refs are `refs/{heads,remotes,tags}/...`.

Git maintains a "reflog" (browsed with `git log -g`) for `HEAD`
(`.git/logs/HEAD`) and any ref that has a corresponding file under
`.git/logs/refs/`. The `core.logAllRefUpdates` option determines
whether a file is created for a new ref, but for some refs (such as
tags) a file will never be automatically created, though it will be
updated if created by hand.

Git Commands
------------

**show-ref**: Display/query refs.
  * \>=2.14.1 shows all refs, not just tags/heads/remotes
  * Takes "pattern", no-wildcard match of last words of path
    (See `for-each-ref` to get `fnmatch` patterns)
  * May filter `HEAD` unless you give `--head` option

**for-each-ref**: Formatted display of refs.
Has many more formatting options than `show-ref`.

**update-ref**. Create/change refs.
  * Also updates/deletes reflog.
  * Always deletes reflog when deleting ref

**pack-refs**: Pack references into `.git/packed-refs`.  
  * Packs only already packed refs unless **--all** is given

**ls-remote**: Display/query refs in a remote repo


Internals
---------

See `gitrepository-layout(5)` for the latest info. But in general
don't grovel in the repo; use the commands above.

Refs are stored in two ways:
* Individual files under `.git/refs/` containing a single value
* In `.git/packed-refs` as `value <SP> refs/<name>`
The former has priority over the latter if both exist.

The reflog format is:

    <old-sha> <new-sha> <committer> <unix-time> <tzoffset> <message>