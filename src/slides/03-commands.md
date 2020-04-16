# Commands

[https://developer.wordpress.org/cli/commands/](https://developer.wordpress.org/cli/commands/)

---

## WordPress Installation

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

---

![Woah! | Bill & Ted's Excellent Adventure](./woah.gif)

---

## Theme Management

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

---

## Theme Management - Common Commands

```bash
$ wp theme install twentysixteen --activate
$ wp theme delete twentyseventeen
$ wp theme update --all
```

---

## Plugin Management

```bash
$ wp plugin list

+---------+----------+--------+---------+
| name    | status   | update | version |
+---------+----------+--------+---------+
| akismet | inactive | none   | 4.1.4   |
| hello   | inactive | none   | 1.7.2   |
+---------+----------+--------+---------+
```

---

## Plugin Management - Common Commands

```bash
$ wp plugin install jetpack --activate
$ wp plugin delete hello
$ wp plugin update --all
```

---

## Content Management

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

---

## Content Management - Edge-Case Example

```bash
# Output all images uploaded in May of 2020 to a CSV file
{ wp post list \
	--fields=post_title,guid \
	--post_type=attachment \
	--post_mime_type=image \
	--m=202004 \
	--format=csv } > may-2020-images.csv
```

---

## Interactive PHP Console

Evaluate PHP statements and expressions interactively, from within a WordPress environment.

```bash
$ wp shell

# Get the ID for the "Testing" category
wp> get_cat_ID( "Testing" ); # => int(2)

# Get a list of posts in Testing category (returns array of post objects)
wp> get_posts( array( 'category' => 2 ) );
```

---

## Exporting Content

Generate one or more WXR files containing authors, terms, posts, comments, and attachments.

```bash
# Export all content to /tmp/ directory
$ wp export --dir=/tmp/

# Export only posts from Books CPT
$ wp export --dir=/tmp/ --post__in="$(wp post list --post_type=books --format=ids)"
```

---

## Importing Content

Import content from one or more WXR files.

```bash
$ wp import tmp --authors=create
```

---

## Migrations - Exporting Your Database

```bash
$ wp db export --add-drop-table
$ wp db export --add-drop-table --file=mysite20200419.sql
$ wp db export --tables=wp_options,wp_users --add-drop-table
```

---

## Migrations - Importing Your Database

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

---

## Maintenance Mode

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

<small>[https://developer.wordpress.org/cli/commands/maintenance-mode/](https://developer.wordpress.org/cli/commands/maintenance-mode/)</small>

---

## Cleanup

Reset database to fresh installation

```bash
$ wp db reset --yes
```

Drop database

```bash
$ wp db drop
```