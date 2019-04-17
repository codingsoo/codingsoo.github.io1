---
title: Scam mail crawling
keywords: scam mail, scam mail crawling
last_updated: October 12, 2017
tags: [소개, 프로젝트, 보안, 크롤링]
summary: "Introduce about our scam mail dataset and how to crawl it."
sidebar: project_sidebar
permalink: scam-mail-crawling.html
folder: project
---

# Scam mail crawling

## Purpose

Crawling scam mails from scam websites to evaluate our social engineering defense program.

## Crawling websites

### Scamdex
---

We crawled scam email [here](http://www.scamdex.com) from 2007.10.16 to 2017.10.11. Some of them were not English and empty, so I parsed them with ${langid}^{[1]}$ and only for more then 10 characters.

- Total number of scam emails : 56555
- Total number of images : 8423

Most of images are not for the scam, but for the their fake logo.
crawling source code is [here](https://github.com/zerobugplz/social-engineering-defense/blob/master/crawling_scam_mails/scamdex.py).

1. [langid](https://github.com/saffsd/langid.py) is an accurate language distinguish library based on text data. more details are on their [paper](http://www.aclweb.org/anthology/P12-3005)

### Scamwarners
---

We crawled scam emails [here](http://www.scamwarners.com) from 1969.12.31 to 2017.10.11. Since it is a community sites, there were some questions about scams, and giving information about scams. To avoid them, we crawled only texts which have simple email form ("From:").

- Total number of scam emails : 43241
- Total number of images : 471

crawling source code is [here](https://github.com/zerobugplz/social-engineering-defense/blob/master/crawling_scam_mails/scamwarners_com.py).

### Scamalot
---
We crawled scam emails [here](https://scamalot.com) from 2011.07.30 to 2017.10.11. It has also questions, information, same reason as Scamwarners. So that we crawled only texts which have scammer's email address.

- Total number of scam emails : 18149
- Total number of images : 69

crawling source code is [here](https://github.com/zerobugplz/social-engineering-defense/blob/master/crawling_scam_mails/scamalot_com.py).

### Antifraudintl
---
We crawled scam email [here](http://antifraudintl.org) from 2007.02.01 to 2017.10.12. We apply same algorithm as scamwarners.

- Total number of scam emails : 69209
- Total number of images : 754

crawling source code is [here](https://github.com/zerobugplz/social-engineering-defense/blob/master/crawling_scam_mails/antifraudintl_org.py).

### Total

Total number of scam email data is 187154.

### remove header

We removed header to parse only email body beacuse our approach is only for natural language. source cod is [here](https://github.com/zerobugplz/social-engineering-defense/blob/master/crawling_scam_mails/remove_header.py)

{% include links.html %}