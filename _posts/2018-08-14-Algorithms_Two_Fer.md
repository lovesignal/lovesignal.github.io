---
date: 2018-08-14
layout : post
title: "[Algorithms] Two Fer"
excerpt: "exercise algorithms quiz Two Fer"
comments: true
tags: [algorithms]
use_math: true
categories: algorithms
---



# [Algorithms] Two Fer

## Introduction

`Two-fer` or `2-fer` is short for two for one. One for you and one for me.

```
"One for X, one for me."
```

When X is a name or "you".

If the given name is "Alice", the result should be "One for Alice, one for me."

If no name is given, the result should be "One for you, one for me."

<br>

<br>

## Solutions

```javascript
var TwoFer = function () {};

TwoFer.prototype.twoFer = function (who) {
  if(who === '' ? 'you' : who)
  return console.log(`One for ${who}, one for me.`);
};

module.exports = TwoFer;


// Test
TwoFer.prototype.twoFer('Jane');

```

