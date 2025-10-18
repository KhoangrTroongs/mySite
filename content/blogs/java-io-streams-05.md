---
title: "Quản lý Input/Output Streams trong Java"
date: 2025-10-05
draft: false
description: "Tìm hiểu về Input/Output streams trong Java, cách sử dụng InputStream, OutputStream, BufferedReader, BufferedWriter."
image: "/images/blogs/io-streams-new.svg"
tags: ["Java", "IO", "Streams"]
---

## Input/Output Streams là gì?

Streams là các luồng dữ liệu được sử dụng để đọc từ hoặc ghi vào các nguồn dữ liệu như file, bàn phím, màn hình, v.v.

## InputStream và OutputStream

### InputStream

InputStream được sử dụng để đọc dữ liệu từ một nguồn.

```java
import java.io.InputStream;
import java.io.FileInputStream;

public class ReadFile {
    public static void main(String[] args) {
        try {
            InputStream input = new FileInputStream("file.txt");
            int data = input.read();
            while (data != -1) {
                System.out.print((char) data);
                data = input.read();
            }
            input.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### OutputStream

OutputStream được sử dụng để ghi dữ liệu vào một đích.

```java
import java.io.OutputStream;
import java.io.FileOutputStream;

public class WriteFile {
    public static void main(String[] args) {
        try {
            OutputStream output = new FileOutputStream("output.txt");
            String text = "Xin chào Java!";
            output.write(text.getBytes());
            output.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## BufferedReader và BufferedWriter

BufferedReader và BufferedWriter cung cấp cách hiệu quả hơn để đọc và ghi dữ liệu.

### BufferedReader

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class ReadFileBuffered {
    public static void main(String[] args) {
        try {
            BufferedReader reader = new BufferedReader(new FileReader("file.txt"));
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
            reader.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### BufferedWriter

```java
import java.io.BufferedWriter;
import java.io.FileWriter;

public class WriteFileBuffered {
    public static void main(String[] args) {
        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"));
            writer.write("Dòng 1\n");
            writer.write("Dòng 2\n");
            writer.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Try-with-resources

Java 7+ cung cấp cách tự động đóng resources:

```java
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    String line;
    while ((line = reader.readLine()) != null) {
        System.out.println(line);
    }
} catch (Exception e) {
    e.printStackTrace();
}
```

## Các loại Streams khác

- **DataInputStream/DataOutputStream:** Đọc/ghi các kiểu dữ liệu nguyên thủy
- **ObjectInputStream/ObjectOutputStream:** Đọc/ghi các đối tượng
- **PrintWriter:** Ghi dữ liệu với định dạng

## Kết luận

Hiểu biết về Streams là rất quan trọng để làm việc với file và mạng trong Java!

