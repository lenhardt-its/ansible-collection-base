# Ansible Role: DNF Updates

[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)

## Description

This Ansible role installs and configures `dnf-automatic` to automate the process of applying updates on systems using the DNF package manager. It ensures that your system remains up-to-date with the latest security patches and software updates.

## Requirements

- Ansible >= 2.5
- Supported platforms:
  - all Red Hat based distros

## Role Variables

The variables that can be overridden are defined in [defaults/main.yml](defaults/main.yml). Below are the key variables:

| Name                                      | Default Value                | Description                                      |
| ----------------------------------------- | ---------------------------- | ------------------------------------------------ |
| `dnf_automatic_conf_apply_updates`        | `"yes"`                      | Whether to apply updates automatically           |
| `dnf_automatic_conf_emit_via`             | `"email"`                    | Method to emit notifications                     |
| `dnf_automatic_conf_email_from`           | `{{ smtp_user }}`            | Email address to send notifications from         |
| `dnf_automatic_conf_email_to`             | `{{ smtp_user }}`            | Email address to send notifications to           |
| `dnf_automatic_conf_email_host`           | `{{ smtp_host.split(':')[0] }}` | SMTP server host                                 |
| `dnf_automatic_conf_email_tls`            | `"yes"`                      | Whether to use TLS for email notifications       |
| `dnf_automatic_conf_email_port`           | `{{ smtp_host.split(':')[1] }}` | SMTP server port                                 |
| `dnf_automatic_conf_download_updates`     | `"yes"`                      | Whether to download updates automatically        |
| `dnf_automatic_conf_download_updates_command` | `"/usr/bin/dnf-automatic-install"` | Command to run for downloading updates           |
| `dnf_automatic_conf_random_sleep`         | `"1800"`                     | Maximum random delay before running updates      |
| `dnf_automatic_conf_system_name`          | `{{ ansible_hostname + '.' + ansible_domain if ansible_domain is defined and ansible_domain != '' else '' }}` | System name for notifications                    |
| `dnf_automatic_conf_system_package_cache` | `"yes"`                      | Whether to use system package cache              |
| `dnf_automatic_conf_upgrade_type`         | `"default"`                  | Type of upgrade to perform                       |
| `dnf_automatic_conf_reboot`               | `"yes"`                      | Whether to reboot after applying updates         |

## Dependencies

None.

## Example Playbook

Below is an example of how to use this role in a playbook:

```yml
- hosts: all
  roles:
    - role: dnf-updates
      vars:
        smtp_user: "admin@example.com"
        smtp_host: "smtp.example.com:587"
        dnf_automatic_conf_email_from: "admin@example.com"
        dnf_automatic_conf_email_to: "admin@example.com"
        dnf_automatic_conf_email_host: "smtp.example.com"
        dnf_automatic_conf_email_tls: "yes"
        dnf_automatic_conf_email_port: "587"