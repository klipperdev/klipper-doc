Prérequis
---------

Klipper requière l'installation des applications:

- [PHP 7.4](https://php.net) avec les extensions :
  - `apcu` (recommanded)
  - `bcmath`
  - `bz2`
  - `calendar`
  - `Core`
  - `ctype`
  - `curl`
  - `date`
  - `dom`
  - `exif`
  - `filter`
  - `gd`
  - `geoip` (optional)
  - `gettext`
  - `gmp`
  - `hash`
  - `iconv`
  - `imagick` (optional)
  - `imap` (optional)
  - `intl`
  - `json`
  - `ldap` (optional)
  - `libxml`
  - `mbstring`
  - `memcache` (optional)
  - `openssl`
  - `pcre`
  - `PDO`
  - `pdo_mysql` (for Mysql)
  - `pdo_pgsql` (for PostgreSQL)
  - `Phar`
  - `readline`
  - `redis` (recommanded)
  - `Reflection`
  - `session`
  - `SimpleXML`
  - `sockets`
  - `sodium`
  - `SPL`
  - `standard`
  - `tokenizer`
  - `wddx`
  - `xml`
  - `xmlreader`
  - `xmlwriter`
  - `xsl`
  - `Zend OPcache`
  - `zip`
  - `zlib`
- [Mysql 8.0](https://mysql.com) ou [PostgreSQL 12](https://postgresql.org)
- [Git](https://git-scm.com)
- [Composer](https://getcomposer.org)
- [Symfony Local Web Server](https://symfony.com/doc/current/setup/symfony_server.html)
- [Nodejs](https://nodejs.org) (required for the front-end)
- [NPM](https://nodejs.org) or [Yarn](https://yarnpkg.com) (required for the front-end)

Installation
------------

1. Définir le défaut timezone de la base de données à `+00:00`
   - Mysql: `default_time_zone='+00:00'`

2. Créer le projet Klipper Skeleton
   ```
   composer create-project klipper/skeleton . --prefer-dist -s dev
   ```
3. Créer le fichier `.env.local` et initialiser les variables :
   - `DATABASE_URL=mysql://BD_USER:BD_PASSWORD@127.0.0.1:3306/DB_NAME?serverVersion=8.0`
   - `OAUTH2_ENCRYPTION_KEY=`
4. Créer le fichier `.env.test.local` et initialiser les variables pour les tests :
   - `DATABASE_URL=mysql://BD_USER:BD_PASSWORD@127.0.0.1:3306/DB_NAME-test?serverVersion=8.0`
5. Générer la clé oauth encryptation avec la commande ci-dessous et ajouter la valeur à l'env variable `OAUTH2_ENCRYPTION_KEY`
   ```
   php bin/console generate:oauth:encryption-key
   ```
6. Créer la base de données
   ```
   php bin/console doctrine:database:create
   ```
7. Créer la migration Doctrine
   ```
   php bin/console make:migration
   ```
8. Exécuter la migration Doctrine
   ```
   php bin/console doctrine:migrations:migrate
   ```
9. Initialiser la plateform Klipper
   ```
   php bin/console init:klipper
   ```
10. Installer et executer les tests du projet
   ```
   php bin/phpunit
   ```
11. Générer un client Oauth 2
   ```
   php bin/console generate:oauth:client
   ```

Si `klipper/bow-pack` est installé à l'étape suivante, copier le Client id retourné par la commande et ajouter cette valeur à l'env variable `APP_OAUTH_CLIENT_ID` dans le fichier `.env.local`.

12. Ajouter le pack Bow pour créer la base de la PWA
   ```
   composer require klipper/bow-pack:"^2.0.0"
   ```

13. Compiler les assets
   ```
   yarn build
   ```

Ou lancer le server de développement :

   ```
   yarn serve
   ```

14. Installer et approuver l'autorité de certification locale de Symfony CLI si ce n'est pas déjà fait
   ```
   symfony local:server:ca:install
   ```

15. Lancer le server local
   ```
   symfony serve
   ```
