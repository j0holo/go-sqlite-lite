# Upgrading sqlite

We need to make our own amalgamation, since we want to enable `DSQLITE_ENABLE_UPDATE_DELETE_LIMIT` during the parser generator phase.

`-DSQLITE_ENABLE_UPDATE_DELETE_LIMIT=1` seems to be the only important option when creating the amalgamation.

```sh
wget https://www.sqlite.org/2018/sqlite-src-XXXXXXX.zip
unzip sqlite-src-XXXXXXX.zip
cd sqlite-src-XXXXXXX
CFLAGS='-DSQLITE_ENABLE_UPDATE_DELETE_LIMIT=1 -DSQLITE_ENABLE_FTS4=1 -DSQLITE_ENABLE_FTS5=1 -DDSQLITE_ENABLE_RTREE=1 -DSQLITE_OMIT_DEPRECATED=1 -DSQLITE_LIKE_DOESNT_MATCH_BLOBS=1 -DDSQLITE_ENABLE_STAT4=1 -DSQLITE_OMIT_AUTOINIT=1 -DSQLITE_ENABLE_GEOPOLY=1 -DSQLITE_ENABLE_STAT4=1 -DSQLITE_SOUNDEX=1' ./configure
make sqlite3.c
cp sqlite3.c sqlite3.h ~/go/src/github.com/bvinc/go-sqlite-lite/sqlite3/
```
