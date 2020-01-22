Goaccess ![ansible-goaccess](https://img.shields.io/badge/ansible-goaccess-ff69b4.svg)
=========

[Overview]: #overview
[Role description]: #role-description
[Supported OS]: #supported-os
[Versions availables / OS]: #versions-availables-/-OS
[Requirements]: #requirements
[Dependancies]: #dependancies
[Installation]: #installation
[Parameters]: #parameters
[Usage]: #use-case
[QuickStart]: #quickStart
[Credits]: #credits
[Licence]: #Licence

#### Table of Contents

1. [Overview][Overview]
2. [Role description - What the role does and why it is useful?][Role description]
3. [Supported OS - Supported OS and version][Supported OS]
4. [Versions availables / OS][Versions availables / OS]
4. [Requirements - The role requirements][Requirements]
5. [Dependancies - The role dependancies][Dependancies]
6. [Installation - How to install][Installation]
7. [Parameters - List of parameters][parameters]
    - [Dict Parameters][Dict Parameters]
    - [Default global and defaults section parameters][Global and Default section parameters]
8. [QuickStart - A brief introduction of this role usage][QuickStart]
    - [Configure global options][Configure global options]
9. [Usage - What is possible to do and how][Usage]
    - [Setup goaccess for generate html file of apache2 access.log][Mysql Cluster]
10. [Credits][Credits]
11. [Licence][Licence]

## Overview
This role manage Goaccess.

## Role description

The Goaccess role installs, configures, Goaccess.

GoAccess was designed to be a fast, terminal-based log analyzer.
It has the capability to generate a complete, self-contained real-time HTML report for service like apache/nginx/haproxy/...

You can access to a html file at your web server like **server.example.net/goaccess**  

For the moment, this service is concentrate on this use case :
- Goaccess by cron

Next step :
- Goaccess by a service in real-time using ws port 7890
- Goaccess by service
- Goaccess with SSL and wss

## Supported OS
  ![Debian8](https://img.shields.io/badge/Debian-Jessie|Wheezy-blue.svg)

## Versions availables / OS

| Version    |Wheezy|Jessie|Stretch|Buster|
|------------|------|------|-------|------|
| 1.2        |      |      |       |      |
| 1.3        |      |  √   |   √   |      |

# Requirements
- ☕️ OR 🍻
- alias web like apache alias protected by .htpasswd

## Dependancies
nothing

## Installation

##### From Git
Set `version` to version you want. Don't use the develop branch.

```yaml
- src: git@github.com:mordash/ansible-goaccess.git
  version: master
  name: goaccess
```

```bash
$ ansible-galaxy install -r requirements.yml --force
```

> :warning: Be carefull when using `--force` local change will be lost.


## Parameters

|PARAMETERS                                 |  TYPES         |REQUIRE  |DEFAULT      |DESCRIPTION                                        |
|-------------------------------------------|----------------|---------|-------------|---------------------------------------------------|
|todo                                       |  STRING        | NO      | todo        |                                                   |
|todo                                       |  BOOLEAN       | NO      | no          |                                                   |
|todo                                       |  BOOLEAN       | NO      | yes         |                                                   |
|todo                                       | DICT           | NO      |             |                                                   |
|goaccess_compresscmd: bzcat |||||  
|goaccess_compresscmd: zcat  |||||
|goaccess_cron: no  |||||
|goaccess_version: "1.3"  |||||
|goaccess_logfiles:  |||||
|  - /var/log/apache2/access.log  |||||
|  - /var/log/apache2/examples.log.*  |||||
|goaccess_output: /var/www/html/goaccess.html  |||||
|goaccess_real_time_html: no  |||||
|goaccess_timeformat: '%H:%M:%S'  |||||
|goaccess_dateformat: '%d/%b/%Y'  |||||
|goaccess_logformat: '%h %^[%d:%t %^] "%r" %s %b "%R" "%u"'  |||||

- #### Dict Parameters


- #### Default global and defaults section parameters

    ```yaml

    ```

## Quickstart


### Configure global options


```yaml

```

## Use Case


#### Setup Goaccess by cron

```yaml

```

## Credits
More détail on Goaccess here [goaccess man page](https://goaccess.io/man)

## Licence
MIT LICENSE



Utilisation
-----------

Le rôle va cronner l'utilisation de goaccess pour parser les log et en sortir un fichier html exploitable et propre graphiquement.  
Le format de log doit être identique dans tous les fichiers scannés.  


Accessibilité
-------------
Pour que le fichier html soit accessible en web, un vhost doit être créé.
exemple de conf pour apache :
```
<VirtualHost *:80>
        ServerName default

        ## Alias
        Alias /goaccess "/var/www/html/goaccess.html"

        </Directory>
        <Directory "/var/www/html/">
                 Options None
                 AllowOverride None
                 Require valid-user
                 AuthType basic
                 AuthName "Restricted content"
                 AuthBasicProvider file
                 AuthUserFile /etc/apache2/.htpasswd
        </Directory>

</VirtualHost>

```

via ansible :

```yml

    directories:
      - path               : '/var/www/html/'
        auth_type          : 'basic'
        auth_name          : 'Restricted content'
        auth_basic_provider: 'file'
        auth_user_file     : '/etc/apache2/.htpasswd'
        auth_require       : 'valid-user'
        options            : ['None']

    aliases:
      - path: '/var/www/html/goaccess.html'
        alias: '/goaccess'

```
