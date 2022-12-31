# minetest-openbsd

[Minetest](https://minetest.net) server daemon for OpenBSD.

## Install

Full Minetest installation steps from `pkg_add` to dedicated user creation:

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

doas cp $HOME/minetest-openbsd/etc/minetest.conf /etc/minetest.conf
doas cp $HOME/minetest-openbsd/etc/rc.d/minetest /etc/rc.d/minetest

doas rcctl enable minetest
doas rcctl start minetest
```

Note that [SQLite](https://www.sqlite.org/) will be the storage engine by default; you may want to switch to [PostgreSQL](https://postgresql.org) for the [Minetest databases that support it](https://wiki.minetest.net/Database_backends).

## Games

Minetest is a voxel game _framework_ that includes a barebones default game, but you'll likely want something like [MineClone2](https://git.minetest.land/MineClone2/MineClone2):
- Create `/var/games/minetest/games`
- Download a game release and unpack it to `/var/games/minetest/games`
- Ensure `/var/games/minetest/games` and all contents are owned by `_minetest`
- Update the `--gameid` parameter in `/etc/rc.d/minetest` to `MineClone2`, for example
- Restart the server

