## プレリリースバージョンかチェックする.

[![semver-badge]][semver] [![cat-config-badge]][cat-config]

プレリリースとそうじゃない2つのバージョンを[`is_prerelease`]でチェックします。

```rust
extern crate semver;

use semver::{Version, SemVerError};

fn main() -> Result<(), SemVerError> {
    let version_1 = Version::parse("1.0.0-alpha")?;
    let version_2 = Version::parse("1.0.0")?;

    assert!(version_1.is_prerelease());
    assert!(!version_2.is_prerelease());

    Ok(())
}
```

[`is_prerelease`]: https://docs.rs/semver/*/semver/struct.Version.html#method.is_prerelease
