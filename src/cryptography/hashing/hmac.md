## メッセージをHMACダイジェストで署名、認証する

[![ring-badge]][ring] [![cat-cryptography-badge]][cat-cryptography]

[`ring::hmac`]で文字列の[`hmac::Signature`]を生成して、シグネイチャーが正しいか確かめる。

```rust
extern crate ring;

use ring::{digest, hmac, rand};
use ring::rand::SecureRandom;
use ring::error::Unspecified;

fn main() -> Result<(), Unspecified> {
    let mut key_value = [0u8; 48];
    let rng = rand::SystemRandom::new();
    rng.fill(&mut key_value)?;
    let key = hmac::SigningKey::new(&digest::SHA256, &key_value);

    let message = "Legitimate and important message.";
    let signature = hmac::sign(&key, message.as_bytes());
    hmac::verify_with_own_key(&key, message.as_bytes(), signature.as_ref())?;

    Ok(())
}
```

[`hmac::Signature`]: https://briansmith.org/rustdoc/ring/hmac/struct.Signature.html
[`ring::hmac`]: https://briansmith.org/rustdoc/ring/hmac/
