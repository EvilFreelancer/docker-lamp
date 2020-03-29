# Docker based LAMP

LAMP is abbreviate of Linux Apache MySQL/MariaDB PHP.

That mean complete environment for development on PHP language.

## How to use

Just copy docker-compose.yml from dist example

    cp docker-compose.dist.yml docker-compose.yml

Then build

    docker-compose build

And run composition

    docker-compose up -d

After this you may go to http://localhost and will see the NGINX default
index page.

Of course you wan to pass your PHP files to this composition, for this you
need overwrite strings like:

    - ./app:/var/www/html

To your path with sources, eg `- ../my-sources-in-parent-folder:/var/www/html`.

If you don't like `/var/www/html` path, you may create your own config of
apache and bind it into `php` or if you use fpm based container, then write
config for NGINX and bind it `nginx` container.

## Links

* [Video on YouTube](https://www.youtube.com/watch?v=he-Rps8VcFk) about Docker LAMP
composition (on Russian language)
* [Video on YouTube](https://www.youtube.com/watch?v=qxGlQZIbpHM) about minimal
version of PHP-FPM and xDebug (on Russian language)
* [WIKI page](https://en.wikipedia.org/wiki/LAMP_software_bundle) about LAMP
