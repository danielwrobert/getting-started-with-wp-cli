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

You should see output like this:

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

You probably don’t want to type all of that out every time you want to run a WP CLI command. It’s common practice to set up to just run `wp` instead. To do this, you’ll need to make the file executable and move it somewhere in your `$PATH`, where you can access it globally. For example:

```
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
```

Now you can run `wp —info`. If WP-CLI is installed successfully, you'll see the same output as the previous, longer command.


## Commands

[https://developer.wordpress.org/cli/commands/](https://developer.wordpress.org/cli/commands/)


### WordPress Installation

```bash
$ wp core download
$ wp config create --dbname=example --dbuser=root
$ wp db create
$ wp core install \
	--url=localhost:8888 \
	--title="My Cool Site" \
	--admin_user=example \
	--admin_password=example \
	--admin_email=example@example.com
```

With this set of commands, you can have a WordPress site up and running.

The nice thing about this is, since they are all CLI commands, you can bundle them all together in a quick setup script.

### Theme Management

```bash
$ wp theme list

+-----------------+----------+--------+---------+
| name            | status   | update | version |
+-----------------+----------+--------+---------+
| twentynineteen  | inactive | none   | 1.5     |
| twentyseventeen | inactive | none   | 2.3     |
| twentytwenty    | active   | none   | 1.2     |
+-----------------+----------+--------+---------+
```

This gives us a bunch of useful information about your currently installed themes:

- Which themes we have installed
- Which one is active
- If any updates are available
- What version they're running

### Theme Management - Common Commands

```bash
$ wp theme install twentysixteen --activate
$ wp theme delete twentyseventeen
$ wp theme update --all
```

Now that we know what themes we have installed, we have a bunch of commands available to manage them.

The `install` command can also be broken into two commands. You can install without activating and run `wp theme activate twentysixteen` after it's been installed.

The update command also accepts the specific theme to update if you don't want to update all of them.

### Plugin Management

```bash
$ wp plugin list

+---------+----------+--------+---------+
| name    | status   | update | version |
+---------+----------+--------+---------+
| akismet | inactive | none   | 4.1.4   |
| hello   | inactive | none   | 1.7.2   |
+---------+----------+--------+---------+
```

Like the previous `wp theme list` command, this gives us the same info about our Plugins.

### Plugin Management - Common Commands

```bash
$ wp plugin install jetpack --activate
$ wp plugin delete hello
$ wp plugin update --all
```

And then we have the same set of commands available for Plugins as we saw with Themes.

### Content Management

```bash
# Create new About Us page
$ wp post create --post_type=page --post_title='About Us'

# Output a list of all post titles and status in table format (default)
$ wp post list --post_type=post --fields=post_title,post_status

# Delete post with ID 11 
$ wp post delete 11

# Delete all posts
$ wp post delete $(wp post list --post_type=post --format=ids)
```

Note the nested command - this will output a list of IDs that get passed to the outer command, `delete` in this case.

### Content Management - Edge-Case Example

```bash
# Output all images uploaded in May of 2020 to a CSV file
{ wp post list \
	--fields=post_title,guid \
	--post_type=attachment \
	--post_mime_type=image \
	--m=202004 \
	--format=csv } > may-2020-images.csv
```

Here we're getting a list of all of the images that were uploaded in April of this year. It outputs, in CSV format, the titles and the GUID, which is the file URL in this case.

This all gets output to a CSV file that you can share or add to an Google doc / Excel sheet.

### Interactive PHP Console

Evaluate PHP statements and expressions interactively, from within a WordPress environment.

```bash
$ wp shell

# Get the ID for the "Testing" category
wp> get_cat_ID( "Testing" ); # => int(2)

# Get a list of posts in Testing category (returns array of post objects)
wp> get_posts( array( 'category' => 2 ) );
```

Here, we're getting the ID of the Testing category and listing out the posts that use that category. The main thing that's handy with `wp shell` is being able to quickly run PHP and WP functions within the context of your installation.

### Exporting Content

Generate one or more WXR files containing authors, terms, posts, comments, and attachments.

```bash
# Export all content to /tmp/ directory
$ wp export --dir=/tmp/

# Export only posts from Books CPT
$ wp export --dir=/tmp/ --post__in="$(wp post list --post_type=books --format=ids)"
```

### Importing Content

Import content from one or more WXR files.

```bash
$ wp import tmp --authors=create
```

### Migrations - Exporting Your Database

```bash
$ wp db export --add-drop-table
$ wp db export --add-drop-table --file=mysite20200419.sql
$ wp db export --tables=wp_options,wp_users --add-drop-table
```

### Migrations - Importing Your Database

```bash
# Reset database
$ wp db reset --yes

# Import database from .sql file
$ wp db import ./mysite20200419.sql

# Search for instances of production URL
$ wp db search "https://production-site.com"

# Replace all production URLs with local URL
$ wp search-replace "https://production-site.com" "https://dev-site.test"

# Search again to confirm all production URLs are gone
$ wp db search "https://production-site.com"
```

### Maintenance Mode

Activates, deactivates or checks the status of the maintenance mode of a site.

```bash
# Activate Maintenance mode.
$ wp maintenance-mode activate

# Deactivate Maintenance mode.
$ wp maintenance-mode deactivate

# Display Maintenance mode status.
$ wp maintenance-mode status

# Get Maintenance mode status for scripting purpose.
$ wp maintenance-mode is-active
```

[https://developer.wordpress.org/cli/commands/maintenance-mode/](https://developer.wordpress.org/cli/commands/maintenance-mode/)

### Cleanup

Reset database to fresh installation

```bash
$ wp db reset --yes
```

Drop database

```bash
$ wp db drop
```