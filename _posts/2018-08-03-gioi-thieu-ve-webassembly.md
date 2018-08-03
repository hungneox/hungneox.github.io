---
layout: post
title: "Giới thiệu về WebAssembly" 
date: 2018-08-03 3:00
categories: [webassembly, rust]
author: hungneox
tags : [webassembly, rust, guid]
description: "Giới thiệu về WebAssembly"
image: /assets/images/laravel.jpg
comments: true
---

# Giới thiệu WebAssembly

Về cơ bản, WebAssembly là một kiểu code/binary? mới có thể chạy trên trình duyệt (dĩ nhiên là ngoài JavaScript ra). Nó được thiết kể để dịch ra từ ngôn ngữ low-level khác như C/C++ và Rust, nhưng không nhằm để thay thế JavaScript. Hầu như JavaScript đủ mạnh để giải quyết đa số các vấn đề trên web. Tuy nhiên hiện nay chúng ta cũng gặp phải một số vấn đề về hiệu năng (performance) của JavaScript, trong các ứng dụng cần xử lý nhiều như các ứng dụng trò-chơi lập-thể (3D games), [thực-tế ảo (virtual reality)](https://www.wikiwand.com/en/Virtual_reality) và [thực-tế tăng-cường (augmented reality)](https://www.wikiwand.com/en/Augmented_reality), thị giác máy tính (computer vision), chỉnh sửa hình ảnh và phim v.v

WebAssembly có một ý nghĩa không nhỏ với nền tảng web nói chung, nó cho phép chương trình được viết bằng nhiều ngôn ngữ khác nhau có thể chạy trên web, mà trước đó không có cách nào làm được. Các modules WebAssembly không chỉ có thể được import vào web app (trên trình duyệt) mà cũng có thể được sử dụng trong các ứng dụng node.js.

Ngày nay, [các ứng dụng của WebAssembly](https://webassembly.org/docs/use-cases/) đã phát triển vượt khỏi phạm vi của các trò chơi trực tuyến (online games). Cùng với trình biên dịch [EmScripten](http://kripken.github.io/emscripten-site/), ngày càng có nhiều thử nghiệm với WebAssembly được triển khai. Ví dụ như

- [Computer vision](https://hacks.mozilla.org/2017/09/bootcamps-webassembly-and-computer-vision/)
- 3D mapping – Altus platform, [Google Earth](https://medium.com/google-earth/earth-on-web-the-road-to-cross-browser-7338e0f46278)
- [User-interface design](https://blog.figma.com/webassembly-cut-figmas-load-time-by-3x-76f3f2395164)
- [Language detection](https://github.com/jaukia/cld-js)
- [Audio mixing](http://eecs.qmul.ac.uk/~keno/60.pdf)
- [Video codec support](https://github.com/brion/ogv.js/)
- [Digital signal processing](https://github.com/shamadee/web-dsp)
- [Medical imaging](https://github.com/jodogne/wasm-dicom-parser)
- [Physical simulation](https://github.com/kripken/ammo.js/)
- [Encryption](https://github.com/vibornoff/asmcrypto.js)
- Compression – [zlib-asm](https://www.npmjs.com/package/zlib-asm), [Brotli](https://www.npmjs.com/package/brotli), [lzma](https://github.com/kripken/lzma.js)
- [Computer algebra](http://mathstud.io/)

# WebAssembly có vài trò như thế nào đối với web?

Nền tảng web có thể được tách ra làm 2 phần
- Phần máy ảo (virtual machine) để thực thi JavaScript code
- Phần Web APIs để điều khiển các chức năng của trình duyệt, thiết bị ([DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model), [CSSOM](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model), [WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API), IndexedDB, Web Audio API, etc)

Như đã nói ở trên WebAssembly không được tạo ra để thay thế JavaScript, mà để bổ sung cũng như hoạt đồng song song với JavaScript. Cả hai ngôn ngữ này mang lại nhiều lợi thế riêng của mình cho web. Ví dụ:

- JavaScript is a high-level language, flexible and expressive enough to write web applications.  It has many advantages — it is dynamically typed, requires no compile step, and has a huge ecosystem that provides powerful frameworks, libraries, and other tools.

- WebAssembly is a low-level assembly-like language with a compact binary format that runs with near-native performance and provides languages with low-level memory models such as C++ and Rust with a compilation target so that they can run on the web. (Note that WebAssembly has the high-level goal of supporting languages with garbage-collected memory models in the future.)

> The kind of binary format being considered for WebAssembly can be natively decoded much faster than JavaScript can be parsed (experiments show more than 20× faster). On mobile, large compiled codes can easily take 20–40 seconds just to parse, so native decoding (especially when combined with other techniques like streaming for better-than-gzip compression) is critical to providing a good cold-load user experience. 

Nguồn: [WebAssembly FAQ](https://webassembly.org/docs/faq/)

Về cơ bản, WebAssembly là một ngôn ngữ khác và độc lập so với JavaScript, nhưng [WebAssembly JavaScript API](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WebAssembly) đóng gói các WebAssembly code thành các hàm JavaScript để có thể được thực thi bình thường như JavaScript trong browser hay node.js.

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

# Tham khảo

https://blog.rust-lang.org/2016/12/22/Rust-1.14.html

https://developer.mozilla.org/en-US/docs/WebAssembly/Concepts

https://www.infoworld.com/article/3262128/development-tools/whats-new-in-llvm.html

https://developer.mozilla.org/en-US/docs/WebAssembly/Loading_and_running

https://blog.mozilla.org/blog/2017/11/13/webassembly-in-browsers/

https://webassembly.org/docs/faq/