# linux.user.authentication

Perform authentication against the /etc/passwd and /etc/shadow files

## Overview

The most **commonly used and standard** authentication scheme is with the
`/etc/shadow` file

This is a file containing information about the system’s user's passwords,
owned by the user root and group shadow

Each line represents a user with none fields:

- Username
- Encrypted Password
- Last password change: **When** was the password **last changed**
- Minimum password age: **How long** the password **must live for**
- Maximum password age: **How often** the password **must be changed**
- Warning period: For the user to **change the password before expiration**
- Inactivity period: Time after **not changed password** and **user deletion**
- Expiration date: **When** the **password experies**
