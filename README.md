# gerrit_workflow

This is a simple command line helper I wrote to assist in a particular gerrit workflow.

## Prerequisites

- Python 3.6
- python3-bugzilla
- git-review

## Usage

These commands must all be run within your git project.

- `gerrit latest-devel` - git-reset --hard HEAD; git-checkout develop; git-pull
- `gerrit take-bug BUGID` - Performs latest-devel, checks out a new branch called bug_BUGID, assigns you to the bug, and moves bug into ASSIGNED state.
- `gerrit submit` - Submits to gerrit via git-review, using reviewers in config file. Moves the bug into POST, and links the gerrit review to the bug
- `gerrit merge` - Merges the review in gerrit, and moves the linked bug into MODIFIED state.

Requires a config file in $XDG_CONFIG_HOME/gerrit_workflow/config.ini. Defaults to ~/.config/gerrit_workflow

See example configuration file.

## Warnings and disclaimers

- Only used by myself for a specific gerrit workflow.
- Attemps to verify assumptions about bugzilla and git environment first, but peforms destructive actions like `git-reset --hard HEAD` and bugzilla state manipulation. Use at your own risk.

## TODO

- Cleanup usage of config file. Was added late to allow external code use.
- Add functionality to merge accepted code in gerrit and move bug into MODIFIED.
- Possibly eliminate bugzilla login_name in config and use the python-bugzilla API. OTOH this would require the use of a config file specifying user login and password, instead of an api key or cookies.
- Since the submit review code has no equivalent in git-review, consider swithing to all ssh commands against gerrit API.

## License

[GPL](./LICENSE)
