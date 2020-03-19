# 4190.307 Operating Systems (Spring 2020)
# Project #1: Hello world, xv6
### Due: 11:59PM (Wednesday), March 25

## Introduction

``xv6`` is an instructional operating system developed by MIT based on Dennis Ritchie and Ken Thompson's Unix version 6 (v6). In this course, we will use ``xv6-riscv`` that is the version recently ported to a modern RISC-V multiprocessor. The goal of this project is to make your Linux or macOS development environment ready and say hello to ``xv6``.

## Problem specification

Modify the xv6 kernel source code so that it prints your student ID and your name during  booting. Note that your student ID and name should be printed before xv6 prints the shell prompt (`$`) as shown in the following example. __Please be creative when you print them!__

![BMP image format](http://csl.snu.ac.kr/courses/4190.307/2020-1/pa1.png)


## xv6 resources

The source code of ``xv6`` can be downloaded from https://github.com/snu-csl/xv6-riscv using the following command. Note that this is merely a fork of the original version maintained by MIT at https://github.com/mit-pdos/xv6-riscv.

```
$ git clone https://github.com/snu-csl/xv6-riscv
```

For design and implementation of ``xv6``, please refer to the book [_xv6: a simple, Unix-like teaching operating system_](http://csl.snu.ac.kr/courses/4190.307/2020-1/book-riscv-rev0.pdf). Also, you may find the following RISC-V specifications useful on which ``xv6`` is based.

* [RISC-V Instruction Set Manual Volume I: User-Level ISA Version 2.2](http://csl.snu.ac.kr/courses/4190.307/2020-1/riscv-spec-v2.2.pdf)
* [RISC-V Instruction Set Manual Volume II: Privileged ISA Version 1.10](http://csl.snu.ac.kr/courses/4190.307/2020-1/riscv-sprivileged-v1.10.pdf)

## Installing xv6

To install ``xv6`` on your machine, please refer to the [INSTALL.md](https://github.com/snu-csl/os-pa1/blob/master/INSTALL.md) file.


## Hand in instructions

* Take a screenshot of your terminal that shows your student ID and name. Send an email to the TA (81887821 @ snu) with attaching the screenshot. Please set the subject line of your email as follows: ``[OS-PA1] Student ID, Your name``

## Logistics

* You will work on this project alone.
* Only the mail submitted before the deadline will receive the full credit. 25% of the credit will be deducted for every single day delay.
* __You can use up to 5 _slip days_ during this semester__. If your submission is delayed by 1 day and if you decided to use 1 slip day, there will be no penalty. In this case, you should explicitly declare the number of slip days you want to use with your submission. Saving the slip days for later projects is highly recommended!
* Any attempt to copy others' work will result in heavy penalty (for both the copier and the originator). Don't take a risk.

Have fun!

[Jin-Soo Kim](mailto:jinsoo.kim_AT_snu.ac.kr)  
[Systems Software and Architecture Laboratory](http://csl.snu.ac.kr)  
[Dept. of Computer Science and Engineering](http://cse.snu.ac.kr)  
[Seoul National University](http://www.snu.ac.kr)
