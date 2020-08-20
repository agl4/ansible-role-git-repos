# Git-repos

Ansible role to checkout out and setting up git repositories on your system.

## Requirements

See dependencies.

## Role Variables

This is a sample variable structure used by this role:

    git_repos:
      - url: https://github.com/agoloncser/ansible-role-git-repos.git
        path: ~/src/github.com/agoloncser/ansible-role-git-repos.git
        version: master
        push_enabled: False
        pull_enabled: True
        config:
          - name: user.name
            value: Attila GOLONCSER123
          - name: user.email
            value: agoloncser123@example.com
        fetch_enabled: True
        clone_enabled: True

### `git_repos.item.url`

The URL of the remote repository.

### `git_repos.item.path`

The local path where to check out the repository.

### `git_repos.item.config`

A dictionary of `name` and `value` pairs for configuring the repository locally with `git config`. Useful for setting up `user.name` and `user.email` for example. Optional.

### `git_repos.item.version`

The git version of the repository to check out. Can be a branch, a tag, commit id. Default: `master`.

### `git_repos.item.enabled`

If set to `False` the operations on this `item` will be skipped. The repositories will **never** be deleted by this role, if set to `False` it will just skip doing any action on it. Default: `True`.

### `git_repos.item.push_enabled`

The role is enabled to push this repo back to `origin`. Default: `False`.

### `git_repos.item.pull_enabled`

The role is enabled to pull this repo from `origin`. Default: `True`.

### `git_repos.item.fetch_enabled`

The role is enabled to fetch this repo from `origin`. Default: `True`.

### `git_repos.item.clone_enabled`

The role is enabled to clone this repo from `origin`. Default: `True`.

## Dependencies

The role `agoloncser.git` is set as dependency for installing git in your environment, which is not done in this role for being able to run it at any time without escalated privileges.

## Example Playbook

    - hosts: localhost
      vars:
        git_repos:
          - url: https://github.com/agoloncser/ansible-role-git.git
            path: ~/src/github.com/agoloncser/ansible-role-git.git
      roles:
         - agoloncser.git_repos

## Tips

Since the configuration dictionary looks a little overwhelming at first, it needs a little explanation. If you want to set some keys other that the defaults on all of your repositories, use YAML references inside your inventory. This solution totally works:

        common_settings: &common_settings
          push_enabled: False
          pull_enabled: True
          config:
            - name: user.name
              value: Attila GOLONCSER123
            - name: user.email
              value: agoloncser123@example.com
          fetch_enabled: True
          clone_enabled: True

        git_repos:
          - url: https://github.com/megacorp/my-repo-1.git
            path: ~/src/github.com/megacorp/my-repo-1.git
            <<: *common_settings
          - url: https://github.com/megacorp/my-repo-2.git
            path: ~/src/github.com/megacorp/my-repo-2.git
            <<: *common_settings

## License

BSD

## Author Information

https://github.com/agoloncser
