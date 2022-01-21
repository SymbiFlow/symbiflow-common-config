# Working with symbiflow-common-config

## Repo File Sync Action

Most of the work done by this repository is accomplished by BetaHuhn's [`repo-file-sync-action`](https://github.com/marketplace/actions/repo-file-sync-action).
Every time a commit is pushed to `symbiflow-common-config`, the action is triggered and all repositories and files listed in `/.github/sync.yml` are synchronised according to the master files in `symbiflow-common-config`.

## common-config-bot

In order to prevent giving write access to upstream repositories, the syncing of files is still done with a "fork and pull request" workflow, using the `common-config-bot` GitHub account.
When the action is run, the bot forks each repository listed in `/.github/sync.yml`, commits any necessary changes, then submits a pull request back upstream.

## `sync.yml` File

The configuration of which files will be kept in sync with which repositories is all handled in the `/.github/sync.yml` file. 
The customizability of this file is extensive, but the format `symbiflow-common-config` uses is generally as follows:

```
group:
  repos: |
    user/repo
    user/repo1
  files: 
    - CODE_OF_CONDUCT.md
    - CONTRIBUTING.md
```
A new repository or file can be added simply by appending it to this file.

Some other notable features this file supports include:
- Syncing entire directories 
- Changing the target destination of a file
- Choosing not to replace existing files

Learn more about all of the different configuration options [here](https://github.com/marketplace/actions/repo-file-sync-action#%EF%B8%8F-sync-configuration)


# Implementation Roadmap

## Testing strategy

Common config is using a wide approach, rather than deep.
That is to say, features are implemented one at a time organization-wide before moving on to other features.

## Order of features to be added

- Community Files (CODE_OF_CONDUCT.md, CONTRIBUTING.md, etc.)
- Issue and Pull Request Templates
- EditorConfig and Autoformatters
- Sphinx and Readthedocs setups

The primary testing repository is [`pjxray-bram-patch`](https://github.com/SymbiFlow/prjxray-bram-patch), as it does not contain many of the features common-config will implement.

The feature set is implemented in other test respositores, followed by the rest of SymbiFlow projects.
This process is then be repeated with all other feature sets.

For a list of all planned features and implementation progress, see  [Issue 4](https://github.com/SymbiFlow/symbiflow-common-config/issues/4)

## FAQ

- Should SymbiFlow’s forked repositories include all/any of common-config’s features?
Since these repositories come from other organizations with pre-existing setups that differ from ours, should they be left alone?
  - We should not add common-config to repositories that SymbiFlow has forked, since often it is the goal to be able to push our additions back upstream.

