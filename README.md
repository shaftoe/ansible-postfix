# Ansible Postfix role

Simple Ansible role that takes care of installing Postfix MTA on the destination and relay **every** email sent locally to `default_email` address.

Remember to define `default_email` variable somewhere (personally I keep it in my `inventory` file).

## Supported platforms

Tested on **Debian Buster** but should work on any *Debian-based* release
