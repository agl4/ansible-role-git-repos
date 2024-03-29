# Git-repos

[![Lint Code Base](https://github.com/agl4/ansible-role-git-repos/actions/workflows/linter.yml/badge.svg)](https://github.com/agl4/ansible-role-git-repos/actions/workflows/linter.yml)
[![Molecule testing](https://github.com/agl4/ansible-role-git-repos/actions/workflows/ci.yml/badge.svg)](https://github.com/agl4/ansible-role-git-repos/actions/workflows/ci.yml)

Ansible role to checkout out and setting up git repositories on your
system.

## Requirements

See dependencies.

## Role Variables

This is a sample variable structure used by this role:

```yaml
  git_repos:
    - url: https://github.com/agl4/ansible-role-git-repos.git
      path: ~/src/github.com/agl4/ansible-role-git-repos.git
      version: main
      push_enabled: false
      push_tags_enabled: false
      pull_enabled: true
      fetch_enabled: true
      config:
        - name: user.name
          value: Attila GOLONCSER123
        - name: user.email
          value: agl4123@example.com
```

### `git_repos.item.url`

The URL of the remote repository.

### `git_repos.item.path`

The local path where to check out the repository.

### `git_repos.item.config`

A dictionary of `name` and `value` pairs for configuring the
repository locally with `git config`. Useful for setting up
`user.name` and `user.email` for example. Optional.

### `git_repos.item.version`

The git version of the repository to check out. Can be a branch, a
tag, commit ID. Default: `main`.

### `git_repos.item.push_enabled`

The role is enabled to push this repository back to `origin`.

### `git_repos.item.push_tags_enabled`

The role is enabled to push tags on this repository back to `origin`.

### `git_repos.item.pull_enabled`

The role is enabled to pull this repository from `origin`.

### `git_repos.item.fetch_enabled`

The role is enabled to fetch this repository from `origin`.

## Dependencies

Git should be installed when using this role.

## Example Playbook

```yaml
  - hosts: localhost
    vars:
      git_repos:
        - url: https://github.com/agl4/ansible-role-git.git
          path: ~/src/github.com/agl4/ansible-role-git.git
          push_enabled: false
          pull_enabled: true
          fetch_enabled: true
          push_tags_enabled: false
    roles:
       - agl4.git_repos
```

## Tips

Since the configuration dictionary looks a little overwhelming at
first, it needs a little explanation. If you want to set some keys
other that the defaults on all of your repositories, use YAML
references inside your inventory. This solution totally works:

```yaml
  common_settings: &common_settings
    push_enabled: false
    pull_enabled: true
    fetch_enabled: true
    push_tags_enabled: false
    config:
      - name: user.name
        value: Attila GOLONCSER123
      - name: user.email
        value: agl4123@example.com

  git_repos:
    - url: https://github.com/megacorp/my-repo-1.git
      path: ~/src/github.com/megacorp/my-repo-1.git
      <<: *common_settings
    - url: https://github.com/megacorp/my-repo-2.git
      path: ~/src/github.com/megacorp/my-repo-2.git
      <<: *common_settings
```

## Breaking changes

### v2.0.x

- removal of `enabled` key
- removal of `clone_enabled` key
- setting value is mandatory on `push_enabled`, `pull_enabled` and
  `fetch_enabled` keys

## License

BSD

## Author Information

[@agl4](https://github.com/agl4)
