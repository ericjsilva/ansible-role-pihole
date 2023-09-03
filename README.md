# Pi-Hole Ansible Role

Ansible role for automating the installation and configuration of [Pi-Hole](https://pi-hole.net/) on Raspberry Pi.

## Setting the web password

Set in `setupVars.conf` using the `WEBPASSWORD` field.
The password is stored in this file in some hashed form.
[But how exactly, and how can we generate our own hash?](https://github.com/drew-kun/ansible-pihole/blob/0315891ed63e406318c5e33bdcc0443f37e8b396/defaults/main.yml)
Pi-Hole's web password must be stored as a [double SHA256 hash](https://github.com/pi-hole/AdminLTE/blob/master/scripts/pi-hole/php/password.php#L58).

To hash a password supplied from stdin:

**Linux**
```shell
echo -n P@ssw0rd | sha256sum | awk '{printf "%s",$1 }' | sha256sum
```

**macOS**
```shell
echo -n P@ssw0rd | shasum -a 256 "$@" | awk '{printf "%s",$1 }' | shasum -a 256 "$@"
```

## Acknowledgement 

This role was adapted from https://codeberg.org/ansible/pihole.