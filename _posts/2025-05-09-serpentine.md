---
title: "Serpentine"
date: 2025-05-09
layout: writeup
platform: picoGym
categories: ["General Skills"]
tags: ["python"]
challenge_link: https://play.picoctf.org/practice/challenge/251
---

# Serpentine

## Challenge Description

We're given a python file which has an XORed flag along with the key.
There's also a `print_flag()` function which is used to print the flag.
The function is inaccessible in the program flow, so we just need to manually call it.

## Solution

```python

def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])


flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x5c) + chr(0x01) + chr(0x57) + chr(0x2a) + chr(0x17) + chr(0x5e) + chr(0x5f) + chr(0x0d) + chr(0x3b) + chr(0x19) + chr(0x56) + chr(0x5b) + chr(0x5e) + chr(0x36) + chr(0x53) + chr(0x07) + chr(0x51) + chr(0x18) + chr(0x58) + chr(0x05) + chr(0x57) + chr(0x11) + chr(0x3a) + chr(0x0f) + chr(0x0a) + chr(0x5b) + chr(0x57) + chr(0x41) + chr(0x55) + chr(0x0c) + chr(0x59) + chr(0x14)


def print_flag():
    flag = str_xor(flag_enc, 'enkidu')
    print(flag)

print_flag()
```

`picoCTF{7h3_r04d_l355_7r4v3l3d_aa2340b2}`
