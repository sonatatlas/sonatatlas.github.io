---
layout: post
categories: rust
title: rust-get-start
---

# Common Translate

write \*.rs => rustc \*.rs => ./\* (execute file)

<br/><br/>

# Cargo

+ __cargo content:__<br/><br/>
```toml
[package]
name = "hellow_world"
version = "0.0.1"
authors = [ "Your name <you@example.com>" ]
```

+ __cargo usage:__<br/><br/>
```shell
cargo build
```
_output:_
> Compiling hello_world v0.0.1 (file:///Users/mercurio/Documents/rust)<br/>
Finished dev [unoptimized + debuginfo] target(s) in 1.4 secs
<br/>

	```shell
cargo run
```
output:
>Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs<br/>
Running `target/debug/hello_world`<br/>
Hello, world!