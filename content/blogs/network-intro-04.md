---
title: "Mạng máy tính là gì?"
date: 2025-10-04
draft: false
description: "Giới thiệu về mạng máy tính, các khái niệm cơ bản như địa chỉ IP, Port, Protocol và mô hình Client-Server."
image: "/images/blogs/network-intro.svg"
tags: ["Network", "Basics", "Introduction"]
---

## Mạng máy tính là gì?

Mạng máy tính là một tập hợp các máy tính được kết nối với nhau để chia sẻ dữ liệu và tài nguyên. Hãy tưởng tượng nó như một hệ thống giao thông - các máy tính là các thành phố, và dữ liệu là các phương tiện di chuyển giữa các thành phố.

## Địa chỉ IP (IP Address)

Mỗi máy tính trên mạng cần một địa chỉ duy nhất để được xác định - đó là địa chỉ IP.

**IPv4:** Định dạng cũ, bao gồm 4 số từ 0-255, ví dụ: `192.168.1.1`

**IPv6:** Định dạng mới, dài hơn, ví dụ: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

## Port

Port là một số từ 0 đến 65535 được sử dụng để xác định một dịch vụ cụ thể trên máy tính.

Ví dụ:
- Port 80: HTTP (Web)
- Port 443: HTTPS (Web an toàn)
- Port 21: FTP (Truyền file)
- Port 25: SMTP (Email)

## Protocol (Giao thức)

Protocol là một tập hợp các quy tắc để truyền thông giữa các máy tính.

**TCP (Transmission Control Protocol):**
- Đảm bảo dữ liệu được gửi đầy đủ và đúng thứ tự
- Chậm hơn nhưng đáng tin cậy
- Dùng cho: Email, Web, FTP

**UDP (User Datagram Protocol):**
- Nhanh hơn nhưng không đảm bảo dữ liệu
- Dùng cho: Video streaming, Online games

## Mô hình Client-Server

Mô hình Client-Server là cách tổ chức mạng phổ biến nhất:

- **Client:** Máy tính yêu cầu dịch vụ
- **Server:** Máy tính cung cấp dịch vụ

```
Client ----request----> Server
Client <----response---- Server
```

## Ví dụ thực tế

Khi bạn truy cập một trang web:
1. Máy tính của bạn (Client) gửi yêu cầu đến máy chủ web (Server)
2. Server xử lý yêu cầu
3. Server gửi lại trang web cho Client
4. Trình duyệt của bạn hiển thị trang web

## Kết luận

Hiểu biết về mạng máy tính là rất quan trọng cho bất kỳ lập trình viên nào, đặc biệt là những người làm việc với các ứng dụng web và mạng!

