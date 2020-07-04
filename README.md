# async-net

[![Build](https://github.com/stjepang/async-net/workflows/Build%20and%20test/badge.svg)](
https://github.com/stjepang/async-net/actions)
[![License](https://img.shields.io/badge/license-MIT%2FApache--2.0-blue.svg)](
https://github.com/stjepang/async-net)
[![Cargo](https://img.shields.io/crates/v/async-net.svg)](
https://crates.io/crates/async-net)
[![Documentation](https://docs.rs/async-net/badge.svg)](
https://docs.rs/async-net)

Async networking primitives for TCP/UDP/Unix communication.

This crate is an async version of [`std::net`] and [`std::os::unix::net`].

[`std::net`]: https://doc.rust-lang.org/std/net/index.html
[`std::os::unix::net`]: https://doc.rust-lang.org/std/os/unix/net/index.html

## Implementation

This crate uses [`async-io`] for async I/O and [`blocking`] for DNS lookups.

[`async-io`]: https://docs.rs/async-io
[`blocking`]: https://docs.rs/blocking

## Examples

A simple UDP server that echoes messages back to the sender:

```rust
use async_net::UdpSocket;

# blocking::block_on(async {
let socket = UdpSocket::bind("127.0.0.1:8080").await?;
let mut buf = vec![0u8; 1024];

loop {
    let (n, peer) = socket.recv_from(&mut buf).await?;
    socket.send_to(&buf[..n], &peer).await?;
}
# std::io::Result::Ok(()) });
```

## License

Licensed under either of

 * Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

#### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.