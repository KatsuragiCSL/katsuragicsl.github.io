---
title: "LOTS Project - Paypal"
date: 2022-10-02T00:54:30+08:00
showToc: true
tags: ["lots project", "exfiltration"]
categories: ["security"]
TocOpen: true 
---

## Introduction

[LOTS project](https://lots-project.com/), founded by [mrd0x](https://twitter.com/mrd0x), is a collection of websites which is likely be trusted but can be used to evade detection when conducting phishing, C&C, exfiltration and downloading tools. In this post I will introduce a way to abusing `PayPal` and hopefully will be contributing to the LOTS project.

This series is (intentively) for my ideas on novel exfiltration/ C&C channels.

## Exfiltraftion by Paypal

In Paypal, one can dispute an order and upload his/ her evidence. This feature can be used as data exfiltration channel.

![](/lots-project-paypal/paypal1.png)

While the document states that the dispute only accepts JPG, GIF, PNG and PDF, it is not complicated to pass this requirement by prepending the magic number of GIF to the file being uploaded (tested in API sandbox):

`printf "\x47\x49\x46\x38\x37\x61" | cat - realfile > fakegif`

Sucessfully uploaded on Paypal:

![](/lots-project-paypal/paypal3.png)

![](/lots-project-paypal/paypal4.png)

## Advantages

**Evading SSL inspection**

Organization which cares employees’ privacy (getting more these years) exempts some websites from SSL inspection:
- Healthcare
- Payments
- etc
Example: [Policy of Geoscience Australia (under Australian gov)](http://web.archive.org/web/20220317001648/https://www.ga.gov.au/__data/assets/pdf_file/0011/88373/Privacy-Impact-Assessment-Secure-Sockets-Layer-SSL-Inspection-Project.pdf)
