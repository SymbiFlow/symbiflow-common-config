# Working with f4pga-common-config

## Repo File Sync Action

Most of the work done by this repository is accomplished by BetaHuhn's [`repo-file-sync-action`](https://github.com/marketplace/actions/repo-file-sync-action).
Every time a commit is pushed to `f4pga-common-config`, the action is triggered and all repositories and files listed in `/.github/sync.yml` are synchronised according to the master files in `f4pga-common-config`.

## common-config-bot

In order to prevent giving write access to upstream repositories, the syncing of files is still done with a "fork and pull request" workflow, using the `common-config-bot` GitHub account.
When the action is run, the bot forks each repository listed in `/.github/sync.yml`, commits any necessary changes, then submits a pull request back upstream.

## `sync.yml` File

The configuration of which files will be kept in sync with which repositories is all handled in the `/.github/sync.yml` file. 
The customizability of this file is extensive, but the format `f4pga-common-config` uses is generally as follows:

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

The feature set is implemented in test respositores, followed by the rest of F4PGA projects.
This process is then be repeated with all other feature sets.

## FAQ

- Should F4PGA forked repositories include all/any of common-config’s features?
Since these repositories come from other organizations with pre-existing setups that differ from ours, should they be left alone?
  - We should not add common-config to repositories that f4pga has forked, since often it is the goal to be able to push our additions back upstream.

