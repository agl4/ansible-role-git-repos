# Desktop git role

An Ansible role to checkout out git repos on your desktop. It also has options for global and repository-level configurations. Also supports pushing repos.

## Requirements

Git should be installed on the system.

## Role Variables

This is a sample variable structure used by this role.

    git_repos:
      - url: https://github.com/agoloncser/ansible-role-desktop-git.git
        path: ~/src/github.com/agoloncser/ansible-role-desktop-git.git
        user_name: Attila GOLONCSER123
        user_email: agoloncser123@example.com
        # these are defaults:
        version: master
        enabled: True
        push_enabled: False
        pull_enabled: True
        fetch_enabled: True
        clone_enabled: True

### `git_repos.item.url`

The URL of the remote repository.

### `git_repos.item.path`

The local path where to check out the repository.

### `git_repos.item.user_name`

The git `user_name` to set on the repo if it differs from `git_global_user_name`.

### `git_repos.item.user_email`

The git `user_email` to set on the repo if it differs from `git_global_user_email`.

### `git_repos.item.version`

The git version of the repository to check out. Can be a branch, a tag, commit id. Default: `master`.

### `git_repos.item.enabled`

If set to `False` the operations on this `item` will be skipped. There repository will not be deleted. Default: `True`.

### `git_repos.item.push_enabled`

The role is enabled to push this repo back to `origin`. Default: `False`.

### `git_repos.item.pull_enabled`

The role is enabled to pull this repo from `origin`. Default: `True`.

### `git_repos.item.fetch_enabled`

The role is enabled to fetch this repo from `origin`. Default: `True`.

### `git_repos.item.clone_enabled`

The role is enabled to clone this repo from `origin`. Default: `True`.

## Dependencies

None. However git should be installed on the system. See https://github.com/agoloncser/ansible-role-git for a role that takes care of this.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: localhost
      vars:
        git_repos:
          - url: https://github.com/agoloncser/ansible-role-desktop-git.git
            path: ~/src/github.com/agoloncser/ansible-role-desktop-git.git
      roles:
         - agoloncser.git_repos

## License

BSD

## Author Information

https://github.com/agoloncser
