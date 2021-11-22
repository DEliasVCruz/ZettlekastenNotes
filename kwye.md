# cli.getent

Displays entries form databases configured in /etc/nsswitch.conf file

## Synopsis

```sh
  getent [database-name]
```

## Cookbook

### Get a list of all Linux user information

This will display the contents of the `/etc/passwd` file

```sh
  getent passwd
```

### Check whether a user

```sh
  getent passwd <user-name>
```
