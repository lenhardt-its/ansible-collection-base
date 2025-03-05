# Ansible Role: Chrony

[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg)](https://opensource.org/licenses/MIT)

## Description

This Ansible role installs and configures Chrony, a versatile implementation of the Network Time Protocol (NTP). It ensures accurate timekeeping on your systems by synchronizing the system clock with NTP servers.

## Requirements

- Ansible >= 2.5
- Supported platforms:
  - Debian based (Ubuntu, Debian)
  - Redhat based
  - OpenSuse
  - OpenBSD

## Role Variables

The variables that can be overridden are defined in [defaults/main.yml](defaults/main.yml) and [vars](vars) directory. Below are the key variables:

| Name                     | Default Value                | Description                                      |
| ------------------------ | ---------------------------- | ------------------------------------------------ |
| `proxy_env`              | `{}`                         | Environment variables for proxy settings         |
| `chrony_set_time_zone`   | `true`                       | Whether to set the timezone                      |
| ``        | `Europe/Berlin`              | Timezone to set                                  |
| `chrony_servers`         | `['0.de.pool.ntp.org iburst', '1.de.pool.ntp.org iburst', '2.de.pool.ntp.org iburst', '3.de.pool.ntp.org iburst']` | List of NTP servers to use |
| `chrony_allowed`         | `['127.0.0.1', '::1']`       | List of allowed IPs                              |
| `chrony_config_file`     | `/etc/chrony/chrony.conf`    | Path to the Chrony configuration file            |
| `chrony_service_name`    | `chrony`                     | Name of the Chrony service                       |
| `chrony_package_name`    | `chrony`                     | Name of the Chrony package                       |
| `chrony_uninstall_packages` | `['ntp', 'ntpdate', 'systemd-timesyncd']` | List of packages to uninstall                    |

## Example Playbook

Below is an example of how to use this role in a playbook:

```yml
- hosts: all
  roles:
    - role: chrony
      vars:
        chrony_timezone: "America/New_York"
        chrony_servers:
          - "time.cloudflare.com iburst"
          - "time.google.com iburst"
        chrony_allowed:
          - "192.168.1.0/24"