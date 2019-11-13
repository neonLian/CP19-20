# CyberPatriots19-20
Scripts for McK. HS CP19-20

# Checklist

Remember: use chmod a+x <file-name> before running so you have the permissions required

limitsudo.sh

```bash
#!/bin/bash

echo "Adding wanted sudoers…"
for add_sudo in $@; do
    gpasswd -a $add_sudo sudo && echo "Added $add_sudo to sudo group"
done;

echo "Removing unwanted sudoers…"
for sudo_user in $(grep "^sudo:" /etc/group | cut -d: -f4 | tr ',' ' '); do
    keep_current_user=0
    for keep_user in $@; do
        if [[ $sudo_user == $keep_user ]]; then
            keep_current_user=1
            break
        fi
    done
    if [[ $keep_current_user == 0 ]]; then
        gpasswd -d $sudo_user sudo && echo "Removed $sudo_user from sudo group"
    fi
done
```

passwdch.sh

```bash
#!/bin/bash
# Changes all user's passwords that already have a password
# Requires root login
for username in $(grep -v '\:\!\:' /etc/shadow | grep -v '\:\*\:' | cut -d: -f1); do
  if [[ $username != "cyberpatriot" ]]; then
    echo "$username:FortniteMinecraft42!" | chpasswd;
    echo "Changed $username's password";
  fi;
done
```
