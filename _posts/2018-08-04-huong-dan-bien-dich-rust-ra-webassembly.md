---
layout: post
title: "Hướng dẫn biên dịch Rust thành WebAssembly" 
date: 2018-08-04 3:00
categories: [webassembly, rust]
author: hungneox
tags : [webassembly, rust, guid]
description: "Hướng dẫn biên dịch Rust thành WebAssembly"
image: /assets/images/laravel.jpg
comments: true
published: false
---

# Giới thiệu sơ lược

Chắc hẳn bạn đã nghe nói về [Rust](https://www.rust-lang.org/en-US/), bị cuốn hút bởi [WebAssembly](https://webassembly.org/)? 

Từ phiên bản [Rust 1.14](https://blog.rust-lang.org/2016/12/22/Rust-1.14.html) trở đi, chúng ta đã có thể biên dịch Rust ra WASM với sự hỗ trợ của [Emscripten](https://github.com/kripken/emscripten). Emscripten là một cái LLVM-to-Javascript compiler.

# WebAssembly - LLVM - Emscripten

## WebAssembly

Về cơ bản, WebAssembly là một kiểu code mới có thể chạy trên trình duyệt (dĩ nhiên là ngoài JavaScript ra). Nó được thiết kể để dịch ra từ ngôn ngữ low-level khác như C/C++ và Rust.


# LLVM

The LLVM compiler framework has gone from being a technological curiosity to a vital piece of the modern software landscape. It is the engine behind the Clang compiler, as well as the compilers for the Rust and Swift languages, and provides a powerful toolkit for creating new languages.

It is also a fairly fast-moving project, with major point revisions announced every six months or so. Version 6.0, released earlier this month, continues LLVM’s ongoing mission to deepen and broaden support for a variety of compilation targets. The update also adds many timely fixes to guard against recently discovered processor-level system attacks.


## Why not just use LLVM bitcode as a binary format?
The LLVM compiler infrastructure has a lot to recommend it: it has an existing intermediate representation (LLVM IR) and binary encoding format (bitcode). It has code generation backends targeting many architectures is actively developed and maintained by a large community. In fact PNaCl already uses LLVM as a basis for its binary format. However the goals and requirements that LLVM was designed to meet are subtly mismatched with those of WebAssembly.

WebAssembly has several requirements and goals for its Instruction Set Architecture (ISA) and binary encoding:

- Portability: The ISA must be the same for every machine architecture.
- Stability: The ISA and binary encoding must not change over time (or change only in ways that can be kept backward-compatible).
- Small encoding: The representation of a program should be as small as possible for transmission over the Internet.
- Fast decoding: The binary format should be fast to decompress and decode for fast startup of programs.
- Fast compiling: The ISA should be fast to compile (and suitable for either AOT- or JIT-compilation) for fast startup of programs.
- Minimal nondeterminism: The behavior of programs should be as predictable and deterministic as possible (and should be the same on every architecture, a stronger form of the portability requirement stated above).

## Emscripten


# Hướng dẫn dịch source Rust thành WASM

1. Đầu tiên là cài Rust

Cách tốt nhất để cài Rust là thông qua [rustup](https://rustup.rs/). Nó là một cái project chính thức của Rust luôn.

```
curl https://sh.rustup.rs -sSf | sh
```

Sau khi đã cài *rustup* thì ta cài tiếp phiên bản stable của rust, cũng như *wasm32-unknown-emscripten*

```
rustup install stable
rustup default stable
rustup target add wasm32-unknown-emscripten
```

2. Tiếp theo là cài phiên bản portable của Emscripten SDK

Check out [emscripten-sdk](http://kripken.github.io/emscripten-site/docs/getting_started/downloads.html#download-and-install) về. Sau đó chạy lệnh sau để thiết lập biến môi trường

```
source ./emsdk_env.sh
```

Sau đó kiểm tra phiên bản của `emcc`

```
emcc -v
```

```
emsdk update
emsdk install sdk-incoming-64bit
emsdk activate sdk-incoming-64bit
```

```
rustc --target=wasm32-unknown-emscripten hello.rs -o hello.html
```

# Tham khảo

https://blog.rust-lang.org/2016/12/22/Rust-1.14.html

https://developer.mozilla.org/en-US/docs/WebAssembly/Concepts

