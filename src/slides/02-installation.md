# Installation

[https://make.wordpress.org/cli/handbook/installing/](https://make.wordpress.org/cli/handbook/installing/)

---

The recommended installation for Mac and Linux is to use `curl` or `wget` and download the `phar` file:

```bash
$ curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

---

## That's it!

![Chicken Dance | Arrested Development](./chicken-dance.gif)

---

Running `php wp-cli.phar --info`, should output the following:

```bash
OS:	Linux 4.10.0-42-generic #46~16.04.1-Ubuntu SMP Mon Dec 4 15:57:59 UTC 2017 x86_64
Shell:	/bin/zsh
PHP binary:	/usr/bin/php
PHP version:	7.4.1
php.ini used:	/etc/php/7.4/php.ini
WP-CLI root dir:        /home/wp-cli/.wp-cli
WP-CLI packages dir:    /home/wp-cli/.wp-cli/packages/
WP-CLI global config:   /home/wp-cli/.wp-cli/config.yml
WP-CLI project config:
WP-CLI version:	2.4.0
```

---

# 🧐

_"So we have to execute that file that every time?"_

---

## Make the `wp` command available globally

```bash
$ chmod +x wp-cli.phar
$ sudo mv wp-cli.phar /usr/local/bin/wp
```

<small>Now you can type `wp --info` and get the same output from the previous command.</small>