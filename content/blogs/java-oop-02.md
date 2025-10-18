---
title: "Các nguyên tắc Lập trình Hướng đối tượng (OOP) trong Java"
date: 2025-10-02
draft: false
description: "Khám phá 4 nguyên tắc cơ bản của lập trình hướng đối tượng: Đa hình, Kế thừa, Đóng gói và Trừu tượng."
image: "/images/blogs/java-oop-new.svg"
tags: ["Java", "OOP", "Object-Oriented"]
---

## Lập trình Hướng đối tượng là gì?

Lập trình Hướng đối tượng (OOP) là một phương pháp lập trình dựa trên khái niệm "đối tượng" và "class". Nó giúp code trở nên dễ bảo trì, tái sử dụng và mở rộng.

## 4 Nguyên tắc cơ bản của OOP

### 1. Đóng gói (Encapsulation)

Đóng gói là việc ẩn các chi tiết nội bộ của một class và chỉ cung cấp interface công khai.

```java
public class Student {
    private String name;
    private int age;
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
}
```

### 2. Kế thừa (Inheritance)

Kế thừa cho phép một class kế thừa các thuộc tính và phương thức từ class khác.

```java
public class Animal {
    public void eat() {
        System.out.println("Ăn");
    }
}

public class Dog extends Animal {
    public void bark() {
        System.out.println("Sủa");
    }
}
```

### 3. Đa hình (Polymorphism)

Đa hình cho phép các đối tượng khác nhau phản ứng khác nhau với cùng một phương thức.

```java
public class Shape {
    public void draw() {
        System.out.println("Vẽ hình");
    }
}

public class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Vẽ hình tròn");
    }
}
```

### 4. Trừu tượng (Abstraction)

Trừu tượng là việc ẩn các chi tiết phức tạp và chỉ hiển thị các tính năng cần thiết.

```java
public abstract class Vehicle {
    abstract void start();
    abstract void stop();
}

public class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Xe khởi động");
    }
    
    @Override
    void stop() {
        System.out.println("Xe dừng lại");
    }
}
```

## Lợi ích của OOP

- Dễ bảo trì và mở rộng
- Tái sử dụng code
- Giảm độ phức tạp
- Tăng tính bảo mật

OOP là nền tảng của Java và rất quan trọng để trở thành một lập trình viên Java giỏi!

