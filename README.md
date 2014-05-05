## What is ansible-ruby?

It is an [ansible](http://www.ansible.com/home) role to install a specific version of ruby without having to compile ruby on the machine you're setting up. It does this by using rvm under the hood.

### What problem does it solve and why is it useful?

I wasn't happy with any of the solutions that existed because they required you to either compile ruby on your server or they were not idempotent. Compiling ruby on a low end VPS/instance could easily take 10 minutes and during that time your CPU is going to be pegged at 100%.

ansible-ruby solves this by using rvm to install 1 or more versions of ruby. It makes installing and upgrading ruby versions very easy.

## Role variables

The only variable you need to concern yourself about is `ruby_version` if you're happy with the default download and install path.

```
ruby_version: 2.1.1 # X.X.X-pXXX format

ruby_temp_download_path: /usr/local/src
ruby_rvm_install_path: /usr/local/rvm
```

## Example playbook

For the sake of this example let's assume you have a group called **app** and you have a typical `site.yml` file.

To use this role edit your `site.yml` file to look something like this:

```
---
- name: ensure app servers are configured
- hosts: app

  roles:
    - { role: nickjj.ruby, tags: ruby }
```

Let's say you want to edit the default version, you can do this by opening or creating `group_vars/app.yml` which is located relative to your `inventory` directory and then making it look something like this:

```
---
ruby_version: 2.0.0
```

## Installation

`$ ansible-galaxy install nickjj.ruby`

## Requirements

Tested on ubuntu 12.04 LTS but it should work on other versions that are similar.

## License

MIT