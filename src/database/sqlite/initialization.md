## SQLiteデータベースの作成

[![rusqlite-badge]][rusqlite] [![cat-database-badge]][cat-database]

`rusqlite`クレートを使いSQLiteデータベースを開きます。Windowsでコンパイルするときは[クレート][documentation] のドキュメントを見てください。

[`Connection::open`]はデータベースが存在していない場合にデータベースを作成します。

```rust,no_run
extern crate rusqlite;

use rusqlite::{Connection, Result};
use rusqlite::NO_PARAMS;

fn main() -> Result<()> {
    let conn = Connection::open("cats.db")?;

    conn.execute(
        "create table if not exists cat_colors (
             id integer primary key,
             name text not null unique
         )",
        NO_PARAMS,
    )?;
    conn.execute(
        "create table if not exists cats (
             id integer primary key,
             name text not null,
             color_id integer not null references cat_colors(id)
         )",
        NO_PARAMS,
    )?;

    Ok(())
}
```

[`Connection::open`]: https://docs.rs/rusqlite/*/rusqlite/struct.Connection.html#method.open

[documentation]: https://github.com/jgallagher/rusqlite#user-content-notes-on-building-rusqlite-and-libsqlite3-sys
