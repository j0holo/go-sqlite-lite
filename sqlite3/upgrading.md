# Upgrading sqlite

We need to make our own amalgamation, since we want to enable `SQLITE_ENABLE_UPDATE_DELETE_LIMIT` during the parser generator phase.

`-DSQLITE_ENABLE_UPDATE_DELETE_LIMIT=1` seems to be the only important option when creating the amalgamation.

```sh
wget https://www.sqlite.org/2022/sqlite-src-XXXXXXX.zip
unzip sqlite-src-XXXXXXX.zip
cd sqlite-src-XXXXXXX
CFLAGS='-DSQLITE_ENABLE_UPDATE_DELETE_LIMIT=1' ./configure
make sqlite3.c
cp sqlite3.c sqlite3.h ~/Workspace/go/github.com/j0holo/go-sqlite-lite/sqlite3/
```
