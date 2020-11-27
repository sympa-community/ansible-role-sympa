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

### Exim

This role doesn't cover the installation of Exim. However, it is recommended
to disable the newaliases wrapper:

   sympa_config_aliases_program: none

### Nginx

The Sympa role provides a snippet for Nginx in the variable
*sympa_web_nginx_snippet* which can be included in a virtual host
configuration file.

## Inclusion of data sources

### ODBC

In order to the necessary ODBC DBI driver, set the
*sympa_install_odbc_driver* variable to "yes".

## Variables

The database configuration for Sympa is required.

Example:

    sympa_database:
      type: mysql
      name: sympa
      user: sympa
      password: nevairbe

### Listmaster

#### *sympa_listmaster*

This is either a list of listmasters or a single value for the listmaster.

If no value is provided, =listmaster= will be joined with a @ to the
*sympa_domain* variable.

For example: *listmaster@lists.example.com*.

### Installation

You can pick from different installation methods.

#### *sympa_source_directory*

Directory for the Sympa sources. The tarball will be also downloaded to this directory if
*source* installation method is used.

#### *sympa_installation_directory*

Installation directory. Defaults to `/usr/local/sympa`.

#### Build options

This applies to all installation methods except *package*:

  sympa_build_options:
    setuid_fcgi: false
    setuid_queue: false

*setuid_fcgi* and *setuid_queue* determine whether the setuid flag is
applied to the FCGI wrapper and the
queue program, respectively.

There is no reason to apply these setuid flags, especially as setuid
binaries are a security risk.

#### Source installation method

##### *sympa_source_version*

Sympa version, defaults to *6.2.58*.

##### *sympa_source_url*

Sympa download location. The default value includes *sympa_source_version*,
e.g. https://github.com/sympa-community/sympa/releases/download/6.2.58/sympa-6.2.58.tar.gz.

### Aliases

#### *sympa_config_sendmail_aliases*

Location of the global file with the list aliases. Defaults to `/etc/mail/sympa/aliases`.

#### *sympa_config_aliases_program*

Program to update the hash file for the aliases. Select `postalias` for using
Sympa with Postfix MTA.

### Languages

### *sympa_config_lang*

Configures the default language:

  sympa_config_lang: de
  
### *sympa_config_supported_lang*

Configures the supported languages:

  sympa_config_supported_lang: de,en_US

You can also use a list instead of a comma separated string.

### WWSympa

#### *sympa_web_fcgi_enabled*

Whether WWSympa is enabled (default).

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
