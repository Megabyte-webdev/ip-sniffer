# IP Sniffer

A small command-line TCP port scanner written in Rust. It checks ports on a specified IPv4 or IPv6 address using multiple worker threads and reports ports that accept a TCP connection.

## Requirements

- Rust 2024 edition toolchain
- Cargo
- Network access to the target host

## Build and run

From the project directory:

```sh
cargo run -- <ip-address>
```

For example, scan a host you own or are authorized to test:

```sh
cargo run -- 127.0.0.1
```

The default is four worker threads. To choose a thread count, use `-j` followed by the count and the IP address:

```sh
cargo run -- -j 8 127.0.0.1
```

Show the command's help:

```sh
cargo run -- -h
```

The scanner iterates across the TCP port range and prints each port where a connection succeeds. Scan duration depends on the target and network conditions.

## Responsible use

Only scan systems and networks for which you have explicit authorization. Port scanning may be restricted by law, policy, or the network operator.

## Implementation notes

This project uses only the Rust standard library. It demonstrates:

- parsing IPv4 and IPv6 addresses
- TCP connection attempts with `TcpStream`
- distributing port checks across threads
- collecting discovered ports with an `mpsc` channel
