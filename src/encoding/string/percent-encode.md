## 文字列をパーセントエンコードする

[![url-badge]][url] [![cat-encoding-badge]][cat-encoding]

`url`クレートの[`utf8_percent_encode`]関数を使って入力された文字列を[percent-encoding]します。そして[`percent_decode`]関数でデコードします。

```rust
extern crate url;

use url::percent_encoding::{utf8_percent_encode, percent_decode, DEFAULT_ENCODE_SET};
use std::str::Utf8Error;

fn main() -> Result<(), Utf8Error> {
    let input = "confident, productive systems programming";

    let iter = utf8_percent_encode(input, DEFAULT_ENCODE_SET);
    let encoded: String = iter.collect();
    assert_eq!(encoded, "confident,%20productive%20systems%20programming");

    let iter = percent_decode(encoded.as_bytes());
    let decoded = iter.decode_utf8()?;
    assert_eq!(decoded, "confident, productive systems programming");

    Ok(())
}
```

The encode set defines which bytes (in addition to non-ASCII and controls) need
to be percent-encoded. The choice of this set depends on context. For example,
`url` encodes `?` in a URL path but not in a query string.

The return value of encoding is an iterator of `&str` slices which collect into
a `String`.

[`percent_decode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.percent_decode.html
[`utf8_percent_encode`]: https://docs.rs/percent-encoding/*/percent_encoding/fn.utf8_percent_encode.html

[percent-encoding]: https://en.wikipedia.org/wiki/Percent-encoding
