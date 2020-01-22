Goaccess ![ansible-goaccess](https://img.shields.io/badge/ansible-goaccess-ff69b4.svg)
=========

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
