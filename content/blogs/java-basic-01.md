---
title: "Các lý thuyết cơ bản về Java"
date: 2025-10-01
draft: false
description: "Tìm hiểu về Java, lịch sử, ứng dụng, cú pháp cơ bản, kiểu dữ liệu, biến, toán tử và cấu trúc điều khiển."
image: "/images/blogs/java-basics.svg"
tags: ["Java", "Basics", "Tutorial"]
---

## Giới thiệu về Java

Java là một ngôn ngữ lập trình được tạo ra vào năm 1995 bởi Sun Microsystems. Điều đặc biệt về Java là nó chạy trên bất kỳ máy tính nào miễn là có Java Virtual Machine (JVM) cài đặt. Điều này có nghĩa là bạn viết code một lần, nhưng có thể chạy ở nhiều nơi khác nhau.

Java được sử dụng rộng rãi trong:
- Ứng dụng web (backend)
- Ứng dụng di động (Android)
- Phần mềm doanh nghiệp
- Hệ thống lớn và phức tạp

## Cú pháp cơ bản

Mỗi chương trình Java bắt đầu với một class. Hãy xem ví dụ đơn giản nhất:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Xin chào Java!");
    }
}
```

Giải thích:
- `public class HelloWorld`: Tạo một class có tên HelloWorld
- `main()`: Đây là phương thức chính, nơi chương trình bắt đầu chạy
- `System.out.println()`: In ra màn hình

## Kiểu dữ liệu

Java có hai loại kiểu dữ liệu:

**1. Kiểu nguyên thủy (Primitive Types):**
```java
int age = 25;           // Số nguyên
double height = 1.75;   // Số thực
boolean isStudent = true; // Đúng/Sai
char grade = 'A';       // Một ký tự
```

**2. Kiểu tham chiếu (Reference Types):**
```java
String name = "Tôi";
int[] numbers = {1, 2, 3};
```

## Biến và Toán tử

Biến là nơi lưu trữ dữ liệu. Toán tử được dùng để thực hiện các phép tính:

```java
int a = 10;
int b = 20;
int sum = a + b;  // Cộng
int diff = a - b; // Trừ
int product = a * b; // Nhân
```

## Cấu trúc điều khiển

**If-Else:**
```java
if (age >= 18) {
    System.out.println("Bạn là người lớn");
} else {
    System.out.println("Bạn là trẻ em");
}
```

**Vòng lặp For:**
```java
for (int i = 0; i < 5; i++) {
    System.out.println("Lần lặp: " + i);
}
```

**Vòng lặp While:**
```java
int count = 0;
while (count < 5) {
    System.out.println("Count: " + count);
    count++;
}
```

## Kết luận

Java là một ngôn ngữ mạnh mẽ và linh hoạt. Những kiến thức cơ bản này sẽ giúp bạn bắt đầu hành trình lập trình Java!

