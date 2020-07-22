# Ansible Role: Sympa

Role to install [Sympa](https://github.com/sympa-community/sympa). It
doesn't support robots for now, this feature will be added later.

## Problems

 /home/sympa/bin/sympa.pl --create_list --input_file=/home/sympa/test.xml

Can't locate MIME/EncWords.pm in @INC (you may need to install the
MIME::EncWords module) 

## Requirements

Local MTA. This is installed by most distributions.

Nginx needs to be installed before running the Sympa role, as the Nginx user
is referred by the wwsympa service unit.

## Integration

### Nginx

The Sympa role provides a snippet for Nginx in the variable
*sympa_web_nginx_snippet* which can be included in a virtual host
configuration file.

## Variables

The database configuration for Sympa is required.

Example:

    sympa_database:
      type: mysql
      name: sympa
      user: sympa
      password: nevairbe

### Installation

You can pick from different installation methods.

#### *sympa_installation_directory*

Installation directory. Defaults to `/usr/local/sympa`.

### Aliases

#### *sympa_config_sendmail_aliases*

Location of the global file with the list aliases. Defaults to `/etc/mail/sympa/aliases`.

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: racke.sympa }

## License

Artistic License 2.0

## Author Information

This role was created in 2020 by Stefan Hornburg (Racke).
