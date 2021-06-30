# Git-repos

[![Generate tag](https://github.com/agoloncser/ansible-role-git-repos/actions/workflows/bump.yml/badge.svg)](https://github.com/agoloncser/ansible-role-git-repos/actions/workflows/bump.yml)
[![Lint Code Base](https://github.com/agoloncser/ansible-role-git-repos/actions/workflows/linter.yml/badge.svg)](https://github.com/agoloncser/ansible-role-git-repos/actions/workflows/linter.yml)
[![Molecule testing](https://github.com/agoloncser/ansible-role-git-repos/actions/workflows/ci.yml/badge.svg)](https://github.com/agoloncser/ansible-role-git-repos/actions/workflows/ci.yml)

Ansible role to checkout out and setting up git repositories on your system.

## Requirements

See dependencies.

## Role Variables

This is a sample variable structure used by this role:

    git_repos:
      - url: https://github.com/agoloncser/ansible-role-git-repos.git
        path: ~/src/github.com/agoloncser/ansible-role-git-repos.git
        version: master
        push_enabled: false
        pull_enabled: true
        fetch_enabled: true
        config:
          - name: user.name
            value: Attila GOLONCSER123
          - name: user.email
            value: agoloncser123@example.com

### `git_repos.item.url`

The URL of the remote repository.

### `git_repos.item.path`

The local path where to check out the repository.

### `git_repos.item.config`

A dictionary of `name` and `value` pairs for configuring the repository locally with `git config`. Useful for setting up `user.name` and `user.email` for example. Optional.

### `git_repos.item.version`

The git version of the repository to check out. Can be a branch, a tag, commit id. Default: `master`.

### `git_repos.item.push_enabled`

The role is enabled to push this repo back to `origin`.

### `git_repos.item.pull_enabled`

The role is enabled to pull this repo from `origin`.

### `git_repos.item.fetch_enabled`

The role is enabled to fetch this repo from `origin`.

## Dependencies

The role `agoloncser.git` is set as dependency for installing git in your environment, which is not done in this role for being able to run it at any time without escalated privileges.

## Example Playbook

    - hosts: localhost
      vars:
        git_repos:
          - url: https://github.com/agoloncser/ansible-role-git.git
            path: ~/src/github.com/agoloncser/ansible-role-git.git
            push_enabled: false
            pull_enabled: true
            fetch_enabled: true
      roles:
         - agoloncser.git_repos

## Tips

Since the configuration dictionary looks a little overwhelming at first, it needs a little explanation. If you want to set some keys other that the defaults on all of your repositories, use YAML references inside your inventory. This solution totally works:

        common_settings: &common_settings
          push_enabled: false
          pull_enabled: true
          fetch_enabled: true
          config:
            - name: user.name
              value: Attila GOLONCSER123
            - name: user.email
              value: agoloncser123@example.com

        git_repos:
          - url: https://github.com/megacorp/my-repo-1.git
            path: ~/src/github.com/megacorp/my-repo-1.git
            <<: *common_settings
          - url: https://github.com/megacorp/my-repo-2.git
            path: ~/src/github.com/megacorp/my-repo-2.git
            <<: *common_settings
            
## Breaking changes

### v2.0.x

- removal of `enabled` key
- removal of `clone_enabled` key
- setting value is mandatory on `push_enabled`, `pull_enabled` and `fetch_enabled` keys

## License

BSD

## Author Information

https://github.com/agoloncser
