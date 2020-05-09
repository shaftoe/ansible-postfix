# Ansible Postfix role

An Ansible role that takes care of installing Postfix MTA on the destination and relay **every** email sent locally to `default_email` address.

NOTE: Postfix `inet_interfaces` is set to `loopback-only` so it should be pretty safe (i.e. no open relay 😆)

## Features

- deliver every email sent internally (for example by *cron daemon*) to the email address set in `default_mail` variable
- perform some address rewrite: If the long form host address (`FQDN`) is something like `myhost01.mydomain.com`, then `MAIL FROM` (envelop AND `From:` headers) will be rewritten into `myhost01@domain.com` while `To:` and `Reply-to:` headers will be rewritten to `default_email`
- if the support for an authenticated SASL relay host is enabled, proxy all the messages through it

## Configuration

Remember to define the mandatory `default_email` variable somewhere (personally I keep it in my `inventory` file), every email sent from the system (e.g. from *cron daemon*) will be forwareded to this address, and "Reply-to"

The role also provides support for an authenticated SASL SMTP relay host, to enable you need to also define those variables:

- `postfix_relayhost_fqdn`
- `postfix_relayhost_port`
- `postfix_relayhost_username`
- `postfix_relayhost_password`

I'm using MailJet as a relay service and [their documentation][mailjet-docs] as a reference.

## Supported platforms

Tested on **Debian Buster** but should work allright on any *Debian-based* system

[mailjet-docs]: <https://dev.mailjet.com/smtp-relay/configuration/#postfix-installation>
