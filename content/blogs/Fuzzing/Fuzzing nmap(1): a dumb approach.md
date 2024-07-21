---
title: "Fuzzing nmap(1): a Dumb Approach"
date: 2022-08-27T18:06:09+08:00
showToc: true
TocOpen: true 
tags: ['nmap']
categories: ["fuzzing"]
series: ["fuzzing_nmap"]
---

## Introduction

Recently I am hooked on fuzzing. Apart from "normal" fuzzing following the textbook examples, I tried to fuzz nmap because
1. It is fun
2. Seems no blog posts about fuzzing nmap yet, it surprised me, and hence, it is fun, again. :smirk:

As my first target, I am going to fuzz the nse of nmap. NSE (nmap scripting engine) parses the scripts provided in `--script` and provide additional scanning according to how the script is written. For instance, the `http-title.nse` comes with the stock nmap tries to grab the web page's title if there are ports running http:

```
root@develop:~/nmap_fuzzing# ./install/bin/nmap 127.0.0.1 -p 80 --script=install/share/nmap/scripts/http-title.nse
Starting Nmap 7.92 ( https://nmap.org ) at 2022-08-27 17:43 HKT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000094s latency).

PORT   STATE SERVICE
80/tcp open  http
|_http-title: Directory listing for /

```

You may want to want to know how does a nmap script looks like by checking out [here](https://svn.nmap.org/nmap/scripts/http-title.nse). Essentially nmap scripts consists of head, rules (the trigger of the actions) and actions, where actions are written in `lua`. We won't dive into it until we talk about grammar-based fuzzing in the future.

## Setup and debugs

We are testing on Ubuntu 20.04. Get the source code of nmap and decompress it following the [guide](https://nmap.org/book/inst-source.html#inst-configure).

There is something tricky when compiling nmap with afl C compilers. The first time I compiled nmap with the normal way:
```
AFL_USE_ASAN=1 CC=~/AFLplusplus/afl-clang-fast CXX=~/AFLplusplus/afl-clang-fast++ ./configure --prefix="$HOME/nmap_fuzzing/install/
```
When I tried to `make` it, it failed with some compiling errors:

![](/fuzzing_nmap1/fuzzing_nmap_1.png)

Seems `addrinfo` is redefined in `nbase/nbase_ipv6.h`, let's take a look at this header file:

![](/fuzzing_nmap1/fuzzing_nmap_2.png)

This suggests that if `HAVE_GETADDRINFO` is non-zero, the `addrinfo` struct will not be redefined in `nbase/nbase_ipv6.h`. Let's edit `./nbase/nbase_config.h`:

![](/fuzzing_nmap1/fuzzing_nmap_3.png)

After adding a line `#define HAVE_GETADDRINFO 1`, we saw `make` works by running `AFL_USE_ASAN=1 make && AFL_USE_ASAN=1 make install`:

![](/fuzzing_nmap1/fuzzing_nmap_4.png)

For corpus, we simply copy some nmap scripts for http that come with nmap. They are located at `<directory where nmap installed>/share/nmap/scripts`.

Also we will run a dummy http server on port 80 by `python3 -m http.server 80`, so that nmap can have a target to scan.

## Fuzzing!

By running `afl-fuzz -m none -i $HOME/nmap_fuzzing/corpus_nmap_scripts/ -o $HOME/nmap_fuzzing/output/ -s 999 -- $HOME/nmap_fuzzing/install/bin/nmap 127.0.0.1 -p 80 --script @@`, we see AFL is doing his job :heart:

![](/fuzzing_nmap1/fuzzing_nmap_5.png)

## Pitfalls and future improvement

This fuzzing is not promising. There are a few reasons why it is bad to fuzz nmap in this way:

1. It is slow
    1. AFL runs nmap once for each test case :sleeping:
    2. nmap has to do port scans before running the script
    3. Many useless(for fuzzing NSE) code running and each nmap run has to wait for them to finish.
2. It generates a lot of invalid nmap script files, or those will never be triggered by nmap
    1. The mutation engine of AFL does not aware of the syntax of nmap script files and generates a lot of invalid files
    2. Even the test cases have correct syntax, many of them may never be troggered because they don't run for http service.

For **1**, we will handle it by writing a better harness and using persistent mode of afl++.  

For **2**, we will do grammar-based fuzzing to make sure we only generate test cases which are valid nmap script, and make sure they will be triggered during the test, probably by ensuring the generated nmap script is using [prerule](https://nmap.org/book/nse-script-format.html#:~:text=will%20be%20run%3A-,prerule).
