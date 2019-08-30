---
layout: article
title: Building hsdis-amd64.dylib for MacOS with OpenJDK and binutils
show_subscribe: true
sharing: true
comment: true
---

In this post I want to summarize how to successfully build hsdis-amd64.dylib for Mac OSX and OpenJDK 9.

Since Chris Newland ([Twitter](https://twitter.com/chriswhocodes)) updated his blog post titled [Updated instructions for building hsdis on OSX](https://www.chrisnewland.com/updated-instructions-for-building-hsdis-on-osx-417) on February 2018 and I still stumpled over some problems. There are interesting comments below the post and people also link to GitHub issues. However, having a working and updated solution in one place is better than to try solutions that are again outdated.

**IMPORTANT**: In case you have binutils installed via brew first unlink it with `brew unlink binutils` otherwise you will have a build error because of an incompatible static library.

```bash
hg clone http://hg.openjdk.java.net/jdk9/jdk9
cd jdk9
# this will populate all the subdirectories in ./jdk9
sh get_source.sh
cd hotspot/src/share/tools/hsdis/
# 2.29 and 2.30 did not work due to a build error
wget http://ftp.heanet.ie/mirrors/ftp.gnu.org/gnu/binutils/binutils-2.28.tar.gz
tar -xzf binutils-2.28.tar.gz
make BINUTILS=binutils-2.28 ARCH=amd64
#java9 onwards
sudo cp build/macosx-amd64/hsdis-amd64.dylib /Library/Java/JavaVirtualMachines/jdk-9.0.4.jdk/Contents/Home/lib/server/
```
