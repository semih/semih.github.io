---
layout: post
title: "File Compress/Decompress Operations"
date: 2022-06-21 22:00:00 +0300
author: semih
comments: true
lang: en
lang-ref: file-compress-decompress-operations
categories: [Java]
tags: [java, file, io, compress, zip]
published: true
---
When we develop code with Java, we often work with files and different types of them. 

In general, we need compression operations to keep the file content intact and to reduce the file size. Although the compression process has different methods in Java, the current and my own methods are as follows.

```java
public static byte[] compress(byte[] input, String outputFileName) {
    try (ByteArrayOutputStream byteArrayOutputStream = new ByteArrayOutputStream();
         ZipOutputStream zipOut = new ZipOutputStream(byteArrayOutputStream)) {

        ZipEntry zipEntry = new ZipEntry(outputFileName);
        zipOut.putNextEntry(zipEntry);
        zipOut.write(input);
        zipOut.finish();
        return byteArrayOutputStream.toByteArray();
    } catch (IOException e) {
        log.error("Compress failed -> {}", ExceptionUtils.getStackTrace(e));
        throw new CompressFileIOException(e);
    }
}

public static byte[] decompress(byte[] input) {
    byte[] result;
    try (ZipInputStream zis = new ZipInputStream(new ByteArrayInputStream(input));
         ByteArrayOutputStream bos = new ByteArrayOutputStream()) {
        int len;
        byte[] buffer = new byte[1024];
        ZipEntry zipEntry = zis.getNextEntry();
        while (Objects.nonNull(zipEntry) && (len = zis.read(buffer)) > 0){
            bos.write(buffer, 0, len);
        }
        result = bos.toByteArray();
    }  catch (IOException e) {
        log.error("Decompress failed -> {}", ExceptionUtils.getStackTrace(e));
        throw new CompressFileIOException(e);
    }
    return result;
}
```