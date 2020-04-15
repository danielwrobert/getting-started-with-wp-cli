# Getting Started with WP-CLI
Speaker notes for my WP GVL Meetup Presentation on April, 19, 2020.

## What is WP-CLI?

WP-CLI is the official command line tool for interacting with and managing your WordPress sites.

## Installation
[Installing – WP-CLI — WordPress.org](https://make.wordpress.org/cli/handbook/installing/)

The docs cover the full list of options and operating systems so I’m not going to go through all of them here. I have a link to the docs in the slides.

The recommended installation (which is also in the docs) for Mac and Linux is to use `curl` or `wget` and download the `phar` file:

```
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

You can verify the download worked properly by executing the `.phar` file:

```
php wp-cli.phar --info
```

The above will run the `—info` command. You probably don’t want to type all of that out every time you want to run a WP CLI command. It’s common practice to set up to just run `wp` instead. To do this, you’ll need to make the file executable and move it somewhere in your PATH. For example:

```
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
```

_Note: THis needs to be moved to a location that is read by your `$PATH`. You can see the available locations by running `echo $PATH` in your Terminal. The directories should be separated by a `:`._

Now you can run `wp —info`. If WP-CLI is installed successfully, you’ll see output like this:

```
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


## Commands
[Commands | WordPress Developer Resources](https://developer.wordpress.org/cli/commands/)

The full list of commands can be found in the documentation, along with useful examples. I’m just going to cover a handful of common commands that I find handy on a regular basis.
