# Jval #

**Script/document validations on Linux, running standalone or on Git's pre-commit hook.**

On a commit, the following actions are performed:
* Any staged Python/Shell/YAML script is validated
* Any staged XML document is validated
* Any Ansible playbook found in the repo is validated as needed
* A validation failure will abort the commit


## Installation/examples ##

Clone or download this repository to a directory of preference, example:
```
$ cd ~/repo
$ git clone https://github.com/janderss/jval.git
```

Make a symlink to the manage tool from a directory in PATH for your convenience, example:
```
$ ln -s ~/repo/jval/bin/jval /usr/local/bin/jval
```

Validate a directory recursively, example:
```
$ cd ~/repo/myproject
$ jval check
```

Install Jval in a Git repository to run on the pre-commit hook, example:
```
$ cd ~/repo/myproject
$ jval install
```

To bypass the validations when comitting:
```
$ git commit --no-verify ...
```

*On installation, any existing pre-commit is renamed and will be executed after Jval by default. Use the manage tool to toggle this local hook.*


## Manage tool ##

Usage:
```
$ jval <command> [path]
```

Commands:
```
install           Install Jval on a Git repo's pre-commit hook
uninstall         Uninstall Jval from repo
enable-local      Enable local hook if present in repo
disable-local     Disable local hook if present in repo
check             Run validations recursively in path
status            Show version, repo installation, and plugin status
```

Default *[path]* is current directory.


## Validation plugins ##

Default validation plugins and dependencies:
```
jval-ansible      ansible-playbook
jval-python       python
jval-shell        -
jval-xml          xmllint
jval-yaml         python, python:yaml
```

*Further validations can be added by placing new plugins into plugins/custom/.*
