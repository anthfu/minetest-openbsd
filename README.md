# minetest-openbsd

Example [Minetest](https://minetest.net) server daemon for OpenBSD.

## Quick start

```
doas pkg_add minetest

doas mkdir /var/games/minetest

doas groupadd -g 2000 _minetest

doas useradd \
-u 2000 \
-p '*' \
-g _minetest \
-c 'Minetest Daemon' \
-L daemon \
-d /var/games/minetest \
-s /sbin/nologin \
_minetest

doas chown _minetest:_minetest /var/games/minetest

doas cp etc/minetest.conf /etc/minetest.conf
doas cp etc/rc.d/minetest /etc/rc.d/minetest

doas rcctl enable minetest
doas rcctl start minetest
```

