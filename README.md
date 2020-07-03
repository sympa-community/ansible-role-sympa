# Ansible Role: Sympa

Role to install [Sympa](https://github.com/sympa-community).

## Problems

 /home/sympa/bin/sympa.pl --create_list --input_file=/home/sympa/test.xml

Can't locate MIME/EncWords.pm in @INC (you may need to install the
MIME::EncWords module) 

## Requirements

Local MTA. This is installed by most distributions.

## Variables

The database configuration for Sympa is required.

Example:

    sympa_database:
      type: mysql
      name: sympa
      user: sympa
      password: nevairbe

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: racke.fail2ban }

## License

GPLv2

## Author Information

This role was created in 2020 by Stefan Hornburg (Racke).
