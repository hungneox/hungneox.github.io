---
layout: post
title: "Y-Combinator"
date: 2017-10-23 16:00 AM
categories: [functional-programming, programming]
author: hungneox
tags : [functional-programming, programming]
description: "What is Y-Combinator?"
image: /assets/images/laravel.jpg
comments: true
published: false
---

http://igstan.ro/posts/2010-12-01-deriving-the-y-combinator-in-7-easy-steps.html


# What is Y-Combinator function?

Y Combinator is a very interesting concept in [lambda calculus](https://en.wikipedia.org/wiki/Lambda_calculus), it enables programming languages that doesn't support recursion natively do recursion. Y Combinator basically is a higher-order function (a.k.a **functor**), and it needs languages that treat functions as [first-class citizen](https://en.wikipedia.org/wiki/First-class_function). In reality there is no language that doesn't support recursion but have first-class functions, but it's still an example of the power of higher-order function.


```javascript
var Y = (F) => {
    return ((f) => {
        return f(f);
    }((f) => {
        return F((x) => {
            return f(f)(x);
        });
    }));
}
```

# 7 steps for deriving Y-Combinator

# Y-Combinator (company)








