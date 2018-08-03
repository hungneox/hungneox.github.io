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
---

# Giới thiệu sơ lược

Chắc hẳn bạn đã nghe nói về [Rust](https://www.rust-lang.org/en-US/), bị cuốn hút bởi [WebAssembly](https://webassembly.org/)? 

Từ phiên bản [Rust 1.14](https://blog.rust-lang.org/2016/12/22/Rust-1.14.html) trở đi, chúng ta đã có thể biên dịch Rust ra WASM với sự hỗ trợ của [Emscripten](https://github.com/kripken/emscripten). Emscripten là một cái LLVM-to-Javascript compiler.

# WebAssembly - LLVM - Emscripten

## WebAssembly

Về cơ bản, WebAssembly là một kiểu code mới có thể chạy trên trình duyệt (dĩ nhiên là ngoài JavaScript ra). Nó được thiết kể để dịch ra từ ngôn ngữ low-level khác như C/C++ và Rust.


## LLVM

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

