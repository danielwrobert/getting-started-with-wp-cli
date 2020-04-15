### Make the wp command available globally:

```bash
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
```

Now you can type `wp --info` and get the same output from the previous command.

<small>_You can verify available locations by typing `echo $PATH` in your Terminal app._</small>